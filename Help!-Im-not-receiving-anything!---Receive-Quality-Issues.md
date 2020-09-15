# Not able to receive any signal/Noisy waterfall
 
## Antennas
Are you using the correct antenna? Is it plugged in correctly? this sounds silly, but It could be as simple as that
## Gain settings
The gain settings are always arranged the same, VGA gain on the right and LNA on the left (both with value "40" in the image below).

[[img/screenshots/Receive_Audio.png]]

### Description of the gain settings
The VGA or **V**ariable **G**ain **A**mplifier can be set to any number between 0-62. It amplifies pretty much everything and is basically a fine-tuning adjustment, I find it works best between 8-16.

The LNA, or **L**ow **N**oise **A**mplifier, can only be set to six settings: 0, 8, 16, 24, 32, 40. the LNA will try it's best to increase the signal-to-noise ratio. 24 or 32 work pretty well most of the time.

### TX amp
The TX amplifier _can_ be used to help increase receive quality, but it is delicate and discouraged most of the time.

## Nearby Transmitters
Nearby, High-Powered transmitters, such as FM stations and trunking stations, can overload your HackRF and create a lot of noise (think of it like clipping in audio). You could consider getting a band block/pass filter to block out common overloading sources like FM stations, rtl-sdr.com sells a nice 88-108 block filter for FM.

## Local Noise Sources
There are many devices that can cause wideband noise: Screens, USB hubs, poorly designed cables, power supplies, faulty wiring, etc.. You can go around unplugging things or flipping breakers to figure out what might be the source of noise. Simply walking outside might help as well.
### Power Banks
Many power banks can be a local noise source, try different power banks if you can.
### H2 Internal Battery Charger
A few people have reported that the internal battery charger on some H2 models can cause noise when plugged in. There isn't really a fix for this unless you want to go about putting another charger. Please report as an issue if you find this issue, with detailed photos of the PCB of your H2. Check the following [video](https://www.youtube.com/watch?v=a_7Xc1_6-l4) to see how a normal functioning H2 does not produce extra noise related to the battery charger.
## Broken RF Chain
It may be entirely possible that something in the RF front end is broken, commonly the TX amp. The best way to go about troubleshooting this is to open up an issue on the [HackRF Github](https://github.com/mossmann/hackrf) explaining the issue, they'll try their best to guide you through it, and if you have a genuine GSG HackRF you might be able to get it replaced.



# Intermittent Signal Loss/Noise
## Loose Cable Connections
As stated before, check you cable connections and antenna. Wiggle things around and see if any dramatic change is reflected in the waterfall.
## Nearby Transmitters
Nearby transmitter can also cause intermittent signal loss, the culprit is almost always pager traffic as those signals can be very strong and transmit intermittently. A nearby trunking repeater could also be to blame.
## H2 Internal Battery Charger
The H2 Internal Battery Charger can also intermittently cause noise when plugged in. Check [this](#h2-internal-battery-charger).
## Local Noise Sources
There are many devices that can cause intermittent wideband noise: Screens, USB hubs, poorly designed cables, power supplies, faulty wiring, etc.. You can go around unplugging things or flipping breakers to figure out what might be the source of noise. Simply walking outside might help as well.