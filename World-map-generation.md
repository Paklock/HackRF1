The Release package includes a map, however you can create your own following simple rules:

* `world_map.jpg` should be square (i.e. 32768 x 32768 px)
* The projection of the map is Mercator based on the World Geodetic System (WGS) 1984 geographic coordinate system (datum)
* Longitude and latitude cover the map from -180 to 180 and -85 to 85, respectively. Note that latitude does not go up to 90 (since most available maps do not include the 5 initial degrees)

With those conditions fulfilled, place the input map in: `sdcard/ADSB/world_map.jpg` and then run `firmware/tools/generate_world_map.bin.py`. Your map will be generated on: `sdcard/ADSB/world_map.bin`

