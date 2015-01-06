pct-search.py
=============
The `pct-search.py` file is a simple python script that returns the closest
Pacific Crest Trail (PCT) mile marker waypoint for a supplied latitude and
longitude. It depends on the `2014_PCT.kml` file which is zipped within the
[halfmiles_pct_tracks_waypoints.kmz](http://www.pctmap.net/google/) file.

To run, just supply a latitude and longitude coordinates (e.g. received from a
device like the SPOT Satellite Messenger) and you'll get back the mile marker
waypoint (note: half-mile markers are written in the format `0156-5`), the
latitude and longitude of the mile marker, and the distance between the
supplied coordinate and the mile marker as calculated by the haversine equation
(as the crow files).

A sample usage is:
```
./pct-search.py 33.59556,-116.57129
0156 33.59643,-116.57026 0.1mi
```

Typically the latitude and longitude coordinates, and the mile marker values
are then manually inserted into the Google docs Daily Mileage spreadsheet.

Note: By internally uncommenting lines in pct-search.py, it can also generate
either pctMileMarkers for script.js or mile_markers for index.php mentioned
below.

pct-search/index.php
====================
Alternatively to the pct-search.py is the `pct-search/index.php` web-site PHP
file which provides a web interface to convert a latitude and longitude
(typically sent by a SPOT Satellite Messenger) to the nearest PCT mile. The
latitude and longitude coordinates, and the mile marker values are then
manually inserted into the Google docs Daily Mileage spreadsheet.

script/Code.gs
==============
The `script/Code.gs` file is a Google docs script file which when run
(typically using an hourly cron job) converts the Google docs Daily Mileage
spreadsheet to a day-points.js file used by the Google map web-site described
below. 

A sample cron job entry is:
```
@hourly wget -q https://script.google.com/macros/s/AKfycbzbbKNCY1tLJrxwRPWXpmlEOaT2blKHBeAsBATn7mfQVPxTsALxukk/exec?jsonp=plotDayPoints -O - > /home/jwatt/justinsomnia.org/pct/day-points.js
```

pct/index.html, pct/script.js, pct/pct-logo.png, and pct/day-points.js
======================================================================
The `pct/index.html, pct/script.js, pct/pct-logo.png, and pct/day-points.js`
web-site files plot a Google map with the Halfmile PCT trail in red and the
day-by-day hiker locations (as defined in day-points.js) using a PCT trail
marker icon.
