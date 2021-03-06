# Identify your device

There are basically two versions of the PortaPack. If you have one that looks like the one below, you have the H1.

[[img/device_h1_genuine.png]] [[img/device_h1.png]]

The H2 is a slightly improved version, but the people making this copy never published the source, hence breaking the license terms. It looks like this:

[[img/device_h2.png]]

The main difference are the controls and the screen, but the H2 usually has extra circuitry to manage the battery charging and powering on/off. In this document, there is a brief description about the details. Check a more technical comparison [here](Differences-Between-H1-and-H2-models).

# Power on/off
The original H1 powers instantly when you plug a power supply to the USB port. To turn it off, just unplug it. Similar to the issues with some USB cables while [upgrading the firmware](Update-firmware), the quality of your cable might affect the performance. 

To power on/off the H2, you need to hold the middle button (knob or pushbutton) for few seconds. See more details [here](https://github.com/eried/portapack-mayhem/wiki/Powering-the-PortaPack).

# Extra functionality (H2 and H2+)
## Charging
This version can charge the internal lipo battery via the USB. There is a led indicator that turns off when the charging is done, but it might flicker.On some models (H2+) there are 4 leds below the knob that represent the state of the battery charge 25%,50%,75%,100%.When charging one will flash dependant on the current charge state of the battery. See more details [here](https://github.com/eried/portapack-mayhem/wiki/Powering-the-PortaPack). 

## Battery life
An internal battery between 1000 and 2500 mAh should last several hours of use, depending App use. The standby consumption is [very low](https://github.com/eried/Research/blob/master/HackRF/PortaPack/h2_standby_consumption.jpg), around 52 µA, so you do not need to worry to remove/disconnect the battery in normal circumstances.
