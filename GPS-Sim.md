This app allows you to broadcast GPS baseband signal data streams. You can use [gps-sdr-sim](https://github.com/osqzss/gps-sdr-sim) to generate data for this app.  

## Example
`gps-sdr-sim -e brdc3540.14n -l 30.286502,120.032669,100 -b 8`

That will create a `gpssim.bin` file that you rename to `BBD_NNNN.C8` and then create `BBD_NNNN.TXT` with:
```
sample_rate=2600000
center_frequency=1575420000
```

Copy to your PortaPack MicroSD and open the file from the GPS Sim app.

## References
https://blog.csdn.net/shukebeta008/article/details/103270214