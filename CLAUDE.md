# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

`gpxtools` is a Go CLI that manipulates GPX (GPS Exchange Format) files, targeting Garmin-specific extensions. It is pre-1.0 with no database layer.

## Commands

Once `go.mod` is initialized (`go mod init github.com/c0dev0id/gpxtools`):

```sh
go build ./...          # build all packages
go test ./...           # run all tests
go test ./pkg/gpx/...   # run tests for a single package
go run . <subcommand>   # run without building
```

## Architecture

The intended layout follows standard Go project structure:

- `main.go` — entry point; dispatches subcommands
- `pkg/gpx/` — GPX parsing and data model (XML unmarshaling)
- `pkg/garmin/` — Garmin-specific extension types
- `cmd/` — one file per subcommand, each implementing the business logic

## Subcommands

Three subcommands are planned:

| Subcommand | Description |
|---|---|
| `add-track-from-route-point-extension <file.gpx>` | Creates tracks from Garmin RoutePoint extension data on routes; skips if a track with the same name already exists |
| `delete-garmin-routes <file.gpx>` | Removes routes named "RoutePoint Extension" or "Garmin Trip Extension" |
| `deduplicate-waypoints <file.gpx>` | Removes waypoints at identical coordinates, keeping the one with the most populated fields |

## GPX / Garmin Notes

- GPX is XML; use `encoding/xml` with struct tags — no external XML library needed.
- Garmin extensions live inside `<extensions>` elements; their namespaces must be preserved on round-trip serialization.
- All file mutations should be done on an in-memory parsed struct and written atomically (write to temp file, rename).
