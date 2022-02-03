This tool creates [airlines.db](https://github.com/eried/portapack-mayhem/blob/next/sdcard/ADSB/airlines.db). This database can be used to find the airline name and country based on the three-letter ICAO code.
This database is currently only used by ADS-B receiver application. 

Source for this database is:
https://raw.githubusercontent.com/kx1t/planefence-airlinecodes/main/airlinecodes.txt

## Build database
* Download the latest version from location above.
* Download script [make_airlines_db.py](https://github.com/eried/portapack-mayhem/blob/next/firmware/tools/make_airlines_db/make_airlines_db.py).
* Put them in the same folder and run script.
* Copy database to /ADSB folder on sdcard.
