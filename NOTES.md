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
