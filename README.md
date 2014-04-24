pct-search.py
=============
`pct-search.php` is a simple python script that returns the closest Pacific Crest
Trail (PCT) mile marker waypoint to a supplied latitude and longitude. It depends
on the `2014_PCT.kml` file which is zipped within the
[halfmiles_pct_tracks_waypoints.kmz](http://www.pctmap.net/google/) file.

To run, just supply a latitude+longitude coordinate (e.g. recieved from a device
like the SPOT Satellite Messenger) and you'll get back the mile marker waypoint
(note: half-mile markers are written in the format `0156-5`), the latitude and
longitude of the mile marker, and the distance between the supplied coordinate
and the mile marker as calculated by the haversine equation (as the crow files).

```
./pct-search.py 33.59556,-116.57129
0156 33.59643,-116.57026 0.1mi
```
