This app allows you to broadcast GPS baseband signal data streams. 

## Generator
You can use [gps-sdr-sim](https://github.com/osqzss/gps-sdr-sim) to generate data for this app.  

`gps-sdr-sim -e RINEX_NAVIGATION_FILE -l LAT,LONG,HEIGHT -o SOMENAME.C8`

That will create `SOMENAME.C8`, but note that you also need to specify its sample rate and frequency in another file, as explained below.

### RINEX navigation file for GPS ephemerides
Download the latest file for this parameter directly from Nasa: https://cddis.nasa.gov/archive/gnss/data/daily/

### Sample rate and frequency specification
Create `SOMENAME.TXT` with:
```
sample_rate=2600000
center_frequency=1575420000
```
This file should use the same filename as the .C8 file but with .TXT extension. It contains the sample rate and center frequency for the .C8 file. Copy the files to your PortaPack MicroSD and open the .C8 file in the GPS Sim app.

## Example
We can create a realistic movement using a NMEA GGA stream generator like https://nmeagen.org/. In this website create several multi point lines with the positions you want. Download the NMEA file clicking "Generate NMEA file".

`gps-sdr-sim.exe -e brdc3540.14n -g OUTPUT.nmea -d DURATION -o MYGPSWALK.C8`

You also need to create `MYGPSWALK.TXT` as specified above.

## Compatibility
Depending on several factors, results may vary. A modern device will use several sources and methods to validate the current position, so spoofing positions may not be possible in all situations. To improve your chances to receive simulated GPS data, try:
* Turn off Wifi/BT/Cellular (airplane mode)
* Go inside, where the device loses GPS signal
* Reboot the device after doing the previous two steps

If the device runs Android, follow your attempts with [GPS Test](https://play.google.com/store/apps/details?id=com.chartcross.gpstest).

### Known results
| Type       | Make    | Model       | Locks on spoofed GPS? | GPS acts "jammed"? | Comments                   |
|------------|---------|-------------|-----------------------|--------------------|----------------------------|
| Tablet     | Samsung | Note 7      | No                    | Yes                |                            |
| Phone      | Huawei  | P30 lite    | No                    | Yes                |                            |
| Phone      | Huawei  | Mate 10 Pro | No                    | Yes                |                            |
| Smartwatch | Huawei  | Amazfit Bip | No                    | No                 |                            |
| Phone      | Apple   | iPhone 6    | **Yes**               | No                 | Works with WIFI on         |

## References
https://blog.csdn.net/shukebeta008/article/details/103270214