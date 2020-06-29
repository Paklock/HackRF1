This application calculates the optimal antenna length for any specific frequency you may input, displaying the result in both **Metric** and **Imperial** units. 

You can also change the wave type from a preset list of divisors including full, half, quarter waves (and other divisors) which is handy for choosing an appropriate antenna (if not the best one -a.k.a full wave one-).

**NEWBIE NOTE**: The need for selecting the right, ("tuned" or "matched") antenna for each frequency is of paramount importance, otherwise the RX or TX will be less than optimal, and under some circumstances (such as grossly mismatched antenna under high power TX) you could even  end up damaging your equipment (this is true for all radio TX equipment).

## Adding your own antennas

This Antenna calculator app goes a step further, by calculating and displaying in simple terms how much you should extend any pre-defined telescopic antenna you may own, which is of great help while doing some field work and having to resource to whatever Antennas you included on your kit.

For this to work, you will need a microSD card inserted on your Portapack. A simple text file with the antennas you use needs to be present under /WHIPCALC/ANTENNAS.TXT

### ANTENNAS.TXT example

```
#antenna label,elements length in mm, separated by a commas
ANT700,95,134,175,206,230,245
ANT500,185,315,450,586,724,862
TELESCOPIC,118,183,253,326,399,476
Cheap 11cm,118,183,253,326,399,476
```

The txt file syntax is self-explanatory with the included comment on top of it.

## Telescopic
* ANT500 
* ANT700
* Generic Telescopic H2 (12 cm)
* Generic Telescopic H1 

## Fixed
* Magnetic fixed 
* [GPS](https://www.aliexpress.com/item/32962871982.html): 1575.42 MHz
* Baofeng

# References
Episode 44: telescopic antenna of the HackRF (The RF Noob)
https://www.youtube.com/watch?v=MzbAEBghcPM