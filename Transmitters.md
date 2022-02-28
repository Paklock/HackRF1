The following are Extracts from HackRF Documentation that can be found [here.](https://hackrf.readthedocs.io/en/latest/). This applies to all Transmissions using  the HackRF/ PortaPack.


## What is the Transmit Power of HackRF?
HackRF One’s absolute maximum TX power varies by operating frequency:
* 1 MHz to 10 MHz: 5 dBm to 15 dBm, generally increasing as frequency increases.
* 10 MHz to 2150 MHz: 5 dBm to 15 dBm, generally decreasing as frequency increases.
* 2150 MHz to 2750 MHz: 13 dBm to 15 dBm.
* 2750 MHz to 4000 MHz: 0 dBm to 5 dBm, decreasing as frequency increases.
* 4000 MHz to 6000 MHz: -10 dBm to 0 dBm, generally decreasing as frequency increases.
Through most of the frequency range up to 4 GHz, the maximum TX power is between 0 and 10 dBm. The frequency range with best performance is 2150 MHz to 2750 MHz.

## What gain controls are provided by HackRF?
HackRF  provides two TX gain controls are  LNA (I)  (0 to 47 dB in 1 dB steps) and RF AMP (0 or 14 dB)

## Use of HackRF 
Overall, the output power is enough to perform over-the-air experiments at close range or to drive an external amplifier. If you connect an external amplifier, you should also use an external bandpass filter for your operating frequency.

## WARNING
**_Before you transmit, know your laws. HackRF One has not been tested for compliance with regulations governing transmission of radio signals. You are responsible for using your HackRF One legally._**

