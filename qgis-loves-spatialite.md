# Working with Spatialite in QGIS

QGIS works wonderfully with Spatialite (.sqlite) databases for larger OSM datasets.

Spatialite databases are nice because they don't requiere a real database program, but does offer a lot of of database functionality. You don't need it, but if you like to play with it, [Spatialite GUI](https://www.gaia-gis.it/fossil/spatialite_gui/index) is your friend.

They are easy to make.


## Install OsGeo

You can download a version here:
https://trac.osgeo.org/osgeo4w/

You need GDAL and QGIS.


## Get and convert data

The most efficient way to get a lot of OSM data is to download a .osm.pbf file.

An example: http://download.geofabrik.de/europe/belgium.html

Activate the OsGeo Shell application. There's a shortcut on your desktop or in your Start Menu

Navigate to the folder you put the .osm.pbf in. Just type something like this:

``` cd C:\temp\ ```

Then you need to tell the software what to do, which is convert the osm.bpf file into a sqlite file.

``` ogr2ogr -f SQLITE -dsco  SPATIALITE=yes belgium.sqlite belgium-latest.osm.pbf ```


## Use the data

Open QGIS and click on the feather icon. First connect to your database. Then you can start making layers. Use "Set filter" to create a layer with only stuff that interests you.

For example, this query will give you all the "slow roads":

``` "highway" = 'bridleway'  OR "highway" = 'cycleway'  OR "highway" = 'footway'  OR "highway" = 'path'  OR "highway" = 'pedestrian'  OR "highway" = 'track' ```

Tags that aren't made available as a column are in "other tags". You can use them like this:

``` "natural"="water"  OR "landuse"="reservoir" OR "other_tags" LIKE '%"water"%' OR "other_tags" LIKE '%"waterway"%' ```

What is defined is not a law of nature. Below a very short explanation as to how you can adapt this.
  
## Control the data

You can define how exactly data is converted from the PBF file to the SQLITE database in a simple script which is used in the background. More info here:
http://www.gdal.org/drv_osm.html


## Alternative: a selection of data for a larger area

You can use Overpass Turbo to make a selection of data from a very large area. This approach is explained in the "Retreat to QGIS" section in [this article](http://www.openstreetmap.org/user/joost%20schouppe/diary/38103).


## I want a background

You can very easily add a background map without a need to do a lot of rendering yourself. You can do this, for example, with the Web>Open Layers plugin.
