On–off keying (OOK) denotes the simplest form of amplitude-shift keying (ASK) modulation that represents digital data as the presence or absence of a carrier wave. OOK system often have a coding sequence. OOK is often used in remote garage and gate keys, often operating at  315 MHz or 433.92 MHz.  Most modern systems though use a rolling code system to prevent Replay attacks.

The App has a number of Pre-configured Device types such as 2260,2262,16 Bit, 1527, 526E, T12E, 5026, UM3750, BA5104,145026, HT6***, TC9148.

There are 2 Tabs. Key Items on each of the App tabs, that can be selected with the cursor and changed with the encoder knob are:

### Common to all TABs

* **Title bar:** The usual items may be changed and displayed.
* **Frequency:** At the lower part of the App is the Frequency setting. This is stored in persistent memory 
* **Step size:** This is next to the frequency and allows the selection of the standard step sizes.
* **Gain:** The gain setting are below the frequency and marked (0-47) LNA(IF) and AMP 0=0db or 1=14dB.
* **Start:** This button starts the transmission and if pressed again can stop the transmission.

### Config Tab

* **Type:** This is the selection of a pre-Configured Encoder/ decoder chip Type.
* **Clk:** Selects the frequency of the OOK switching rate. This is interlinked to  the frame rate for example 1kHz clock is 36000 10^6 s frame rate. Range of clock is 1-500KHz.
* **Frame:** This can be selected but as stated above sets the clock and frame rate. The settings go from 30 10^6s to 36000 10^6s.
* **Symbols:** This is the pattern of the symbol message sent. The 0/1 can be change to alter the OOK pattern. Note the pattern is made  up as shown  in the letters line of A for Address,  D for DATA,  S for Sync .
* **Waveform:** This shows the diagrammatic view of the waveform sent.
* **Progress Bar:** When the transmission is started it shows the progress of the transmission while sending. Not many of the transmission are very short and looks like they are not sent.

### Scan Tab

This is not implemented.
