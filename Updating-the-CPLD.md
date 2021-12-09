You can update the CPLD manually:

First get the original HackRF project into your computer:

`git clone https://github.com/mossmann/hackrf.git`

Then, connect your portapack into your machine, put it into HackRF mode and use the following command in order to update the CPLD:

`hackrf_cpldjtag -x hackrf/firmware/cpld/sgpio_if/default.xsvf`

**LED1/2/3 blinking means CPLD program success.**
LED3/RED steady means error.
Wait for the message 'Write finished' and power OFF / Disconnect your portapack from your machine.
