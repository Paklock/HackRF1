With this app you can receive real-time ADS-B used for air traffic control.

# Functionality
Select a received aircraft and more detail will be shown. Select "Show on map" to see the aircraft location. ADS-B operates on 978 to 1090 MHz. Even a short antenna attached directly to the Portapack will receive ADS-B when the receive preamp is enabled ("1" displayed).

## Map
For map functionality a world map must be loaded on the SD card. The map image and other SD card content is available from the portapack-mayhem github download page.

## Airlines

### Log into microSD
The ADSB RX app will log each frame including the following columns:

* **(YEAR MONTH DAY HOUR MIN SEC)**
* **(RAW PACKET IN HEX)**
* ICAO: **(ICAO)**
* **(CALLSIGN)**
* Alt: **(ALTITUDE)**
* Lat: **(LATITUDE)**
* Lon: **(LONGITUDE)**

Example:

`20171103100227 8DADBEEFDEADBEEFDEADBEEFDEADBEEF ICAO:nnnnnn callsign Alt:nnnnnn Latnnn.nn Lonnnn.nn`