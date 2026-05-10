# GPXtools

GPXtools is a set of command line tools that can modify gpx files.

GPXtools are written in GOlang.

Tools:

$ gpxtools add-track-from-route-point-extension <file.gpx>

This tool will read all routes, and will create a track with the same name, that's created from the routes garmin route point extension data. A track will only be ccreated if there is no track with this exact name already.

$ gpxtools delte-garmin-routes <file.gpx>

This tool will remove routes with the name "RoutePoint Extension" and "Garmin Trip Extension"

$ gpxtools deduplicate-waypoints <file.gpx>

This tool removes duplicate waypoints that point to the exact same coordinates. The waypoint with the most filled in data elements will be kept.
