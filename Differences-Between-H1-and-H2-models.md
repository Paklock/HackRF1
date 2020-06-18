# Audio

At a glance, hardware-side, both models feature a **headphone connector** and the same **AK4951 AUDIO / CODEC IC** (You can get the datasheet [following this link](https://www.akm.com/content/dam/documents/products/audio/audio-codec/ak4951aen/ak4951aen-en-datasheet.pdf)).

The AK4951 includes separate pins for speaker and headphone output:

*  Pins 20 (**SPP**) and 19 (**SPN**) labeled as **SP**eaker **P**ositive and **SP**eaker **N**egative (1W 8 ohm)
* Pins 22 (**HPL**) and 23 (**HPR**) as in (**H**ead**P**hones **L**eft, **H**ead**P**ones **R**ight) (16 ohm)

Upon close inspection, several differences arise:

## Audio in H2 model
Portapack H2 circuitboard includes a connector header for easily adding an internal speaker. 

The **AK4951 IC** is rotated 180º and placed more into the middle of the circuit board, allowing for the addition of an extra IC: The ChipStar brand **CS8122S** ultra-low EMI, filter-free, class-D amplifier, for driving the speaker output with up to 3W. 

The speaker audio header is switched on/off by the headphone female connector, which includes the usual switch, detecting the insertion of a male plug in it.

## Audio in H1 model

The soldering pads for an internal speaker connector header are present. The speaker +/GND signals on the pad are routed directly into AK4951 pins.

**NOTE:** _There is no extra amplifier IC between the speaker pad and the AK4951. The AK4951 includes a speaker amplifier capable of 1W, when powered @5v._

