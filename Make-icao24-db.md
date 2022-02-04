This tool creates [icao24.db](https://github.com/eried/portapack-mayhem/blob/next/sdcard/ADSB/icao24.db).
 
This database is used to find aircraft-related information based on the 24-bit ICAO transponder code.
This database is currently only used by ADS-B receiver application. 

Source for this database is:
https://opensky-network.org/datasets/metadata/aircraftDatabase.csv

## Build database
 * Copy file from: https://opensky-network.org/datasets/metadata/aircraftDatabase.csv
 * Run Python 3 script: `./make_icao24_db.py` 
 * Copy file to /ADSB folder on SDCARD
