Your HackRF (the board under the PortaPack) has the ability to send or receive radio waves in a broad frequency range. Some of its specs are:

*	Transceiver: Half-duplex
*	Operating frequency: 1 MHz to 6 GHz
*	Supported sample rates: 2 to 20 Msps (quadrature)
*	Resolution: 8 bits
*	Max TX power (you can also check an [empirical measurement](https://www.reddit.com/r/hackrf/comments/hi8275/measurement_of_the_hackrf_one_output_power/)):
    *	10 to 2150 MHz: 5 to 15 dBm, increasing as frequency decreases
    *	2150 to 2750 MHz: 13 to 15 dBm
    *	2750 to 4000 MHz: 0 to 5 dBm, increasing as frequency decreases
    *	4000 to 6000 MHz: -10 to 0 dBm, increasing as frequency decreases
*	Max RX power: -5 dBm. Exceeding -5 dBm can result in permanent damage! Can safely accept up to 10 dBm with the front-end RX amplifier disabled
*	CLKOUT/CLKIN: 10 MHz square wave (0V to 3V for a high impedance load)

From that list that might be confusing for the first user, we could extract few interesting points:

* Half-duplex: Means that it can send OR receive, but not send AND receive in a particular instant.
* Operating frequency: goes from 1 MHz to 6 GHz, that means that the device is able to send and receive signals from almost all the common sources you can imagine. You can see the range with more details [here](https://en.wikipedia.org/wiki/Frequency_allocation). 
