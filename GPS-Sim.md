This app allows you to broadcast GPS baseband signal data streams. 

## Generator
You can use [gps-sdr-sim](https://github.com/osqzss/gps-sdr-sim) to generate data for this app.  

`gps-sdr-sim -e brdc3540.14n -l LAT,LONG,HEIGHT -o BBD_NNNN.C8`
That will create `BBD_NNNN.C8`, but note that you also need to specify its sample rate and frequency in another file, as explained below.

### Sample rate and frequency specification
Create `BBD_NNNN.TXT` with:
```
sample_rate=2600000
center_frequency=1575420000
```

Copy to your PortaPack MicroSD and open the file from the GPS Sim app.

## Example
We can create a realistic movement using a NMEA GGA stream generator like https://nmeagen.org/. In this website create several multi point lines with the positions you want. Download the NMEA file clicking "Generate NMEA file".

`gps-sdr-sim.exe -e brdc3540.14n -g OUTPUT.nmea -d DURATION -o BBD_NNNN.C8`

You also need to `BBD_NNNN.TXT` as specified above.

## References
https://blog.csdn.net/shukebeta008/article/details/103270214