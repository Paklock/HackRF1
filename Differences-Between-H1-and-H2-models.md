Portapack H1 hardware represents the original design, which is well documented, placed in the public domain. 

Portapack H2 hardware is a custom modification of the original design, made by unknown fans (which at this time are keeping their design notes / documents for themselves) including some upgrades:

* Bigger screen
* Different navigation buttons
* Internal battery
* Battery charging circuitry
* Better internal Speaker integration

Note: _There is also an hybrid H1 / H2 model, called the 2020 H1 Model, which is an H1 but with a bigger screen._

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

Only the soldering pads for an internal speaker connector header are present. The speaker +/GND signals on the pad are routed directly into AK4951 pins.

**NOTE:** _There is no extra amplifier IC between the speaker pad and the AK4951. The AK4951 includes a speaker amplifier capable of 1W, when powered @5v._

You can solder a laptop / tablet speaker in H1 speaker pads. In order to enable it, you will need to install MAYHEM firmware, where you can also configure under **OPTIONS -> INTERFACE** the addition of a SPEAKER button on your top status bar.

### Audio devil is in the Details
Since the firmware is shared between H1 and H2, on Portapack H2 you end up powering up TWO speaker amplifiers: The one inside AK4951 IC, and the extra CS8122S one.


