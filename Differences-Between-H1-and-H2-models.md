# Audio

At a glance, hardware-side, both models feature a **headphone connector** and the same **AK4951 AUDIO / CODEC IC** (You can get the datasheet [following this link](https://www.akm.com/content/dam/documents/products/audio/audio-codec/ak4951aen/ak4951aen-en-datasheet.pdf)).

Upon close inspection, several differences arise:

## Audio in H2 model
Portapack H2 circuitboard includes a connector header for easily adding an internal speaker. 

The **AK4951 IC** is rotated 180º and placed more into the middle of the circuit board, allowing for the addition of an extra IC: The **CS8122S** ultra-low EMI, filter-free, class-D amplifier, for driving the speaker output with up to 3W. 
The speaker audio header is switched on/off by the headphone female connector, which includes the usual switch, detecting the insertion of a male plug in it.

## Audio in H1 model

The soldering pads for an internal speaker connector header are present. The speaker +/GND signals on the pad are routed into AK4951 pins 20 (SPP) and 19 (SPN) which are labeled as SPeaker Positive and SPeaker Negative.

**NOTE:** _There is no extra amplifier IC in the middle._

