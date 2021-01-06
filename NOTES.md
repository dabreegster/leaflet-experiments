# Notes

Basic webdev questions:

- What's the CLI tool to autoformat HTML+CSS+JS? tidy with default options flattens everything

Leaflet questions:

- What's the coordinate system? How do I know what tile will be requested?
	- https://leafletjs.com/examples/crs-simple/crs-simple.html maybe helps
	- https://en.wikipedia.org/wiki/Tiled_web_map

Raster vs vector:

- One big geojson file with lots of polygons for everything, labelled with a color. Send that through some geojson tiler?
- Dynamically generate lane markings or include them?
- For raster, have to figure out how to render directly to a buffer without using screenshots. Need multiple zoom layers.
- Could just export a GeomBatch to SVG or even pipe through some software rendering (like tiny-skia?)

## Raster magic

Use combine.sh (super slow)

Then `convert full.gif -crop 256x256 -set filename:tile "%[fx:page.x/256+2048]_%[fx:page.y/256+2048]" +adjoin +repage 'tiled_%[filename:tile].gif'`

Or turn the geojson into rasters. Maybe https://github.com/protomaps/protomaps2d

Or just do it manually, maybe with tiny-skia? https://wiki.openstreetmap.org/wiki/Slippy_map_tilenames
https://github.com/dfyz/osm-renderer/blob/master/src/tile.rs

## Vector

Tangram renders the giant .geojson reasonably. How can we make it smaller?

- Make it read mbtile (1.1MB) on web?
	- nope: https://github.com/tangrams/tangram/issues/628
- Transform the geojson into MVT?

tippecanoe -e mvt -z 20 -pC rendered_map.json



Try:
- https://github.com/brandonxiang/leaflet-geojson-vt/tree/leaflet1.0.0/test
- https://github.com/protomaps/cobble
- https://flatgeobuf.org/ but no indexing?
- https://github.com/maplibre/maplibre-gl-js
