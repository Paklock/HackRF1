This tool creates [icao.db](https://github.com/eried/portapack-mayhem/blob/next/sdcard/ADSB/icao25.db).
 
This database is used to find aircraft-related information based on the 24-bit ICAO transponder code.
This database is currently only used by ADS-B receiver application. 

Source for this database is:
https://raw.githubusercontent.com/kx1t/planefence-airlinecodes/main/airlinecodes.txt

## Build database
* Download the latest version from location above.
* Download script [make_airlines_db.py](https://github.com/eried/portapack-mayhem/blob/next/firmware/tools/make_airlines_db/make_airlines_db.py).
* Put them in the same folder and run script. Note: Python 3 required.
* Copy database to /ADSB folder on sdcard.
