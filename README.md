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

Typically the latitude and longitude coordinates, and the mile marker waypoint
values are then manually inserted into the Google docs Mileage Log spreadsheet.

Note: By internally uncommenting lines in pct-search.py, it can also generate
either `mile_markers` for `index.php` or `pctMileMarkers` for `script.js`
mentioned below.

pct-search/index.php
====================
Alternatively to the `pct-search.py` is the `pct-search/index.php` web-site
PHP file which provides a web interface to convert a latitude and longitude
(typically sent by a SPOT Satellite Messenger) to the nearest PCT mile. The
latitude and longitude coordinates, and the mile marker waypoint values are
then manually inserted into the Google docs Mileage Log spreadsheet.

`spreadsheet/Dad's PCT Mileage Log.ods`
=======================================
The `spreadsheet/Dad's PCT Mileage Log.ods` is the Google docs Mileage Log
spreadsheet in OpenDocument spreadsheet format for Brian "Tartan" Watt's 2014
PCT Thru-Hike. It can be used as a template for a new Mileage Log. To create
a new spreadsheet based upon this, deleted all entries in the Date, Location, 
Mile Marker, Notes, and E-mail columns then import and upload it to Google
docs.

script/Code.gs
==============
The `script/Code.gs` file is a Google docs script file which when run
(typically using an hourly cron job) converts the Google docs Mileage Log
spreadsheet to a `day-points.js` file used by the Google map web-site described
below. It can be used as a template for a new Google docs script file. To
create a new script based upon this, update the SPREADSHEET_ID, and SHEET_NAME
to the new Google docs spreadsheet that was based upon the template above. You
must also update the cron job entry to refer to this new Google docs script
file.

A sample cron job entry is:
```
@hourly wget -q https://script.google.com/macros/s/AKfycbzbbKNCY1tLJrxwRPWXpmlEOaT2blKHBeAsBATn7mfQVPxTsALxukk/exec?jsonp=plotDayPoints -O - > /home/jwatt/justinsomnia.org/pct/day-points.js
```

pct/index.html, pct/script.js, pct/pct-logo.png, and pct/day-points.js
======================================================================
The `pct/index.html`, `pct/script.js`, `pct/pct-logo.png`, and
`pct/day-points.js` web-site files plot a Google map with the Halfmile PCT
trail in red and the day-by-day hiker locations (as defined in `day-points.js`)
using a PCT trail marker icon.
