Capture App is designed to capture I/Q data. This is  is stored as pairs of 16-bit signed values in a .C16 file (Complex 16 bit) and are stored in little-endian format.The Metadata (“Center frequency” and Bandwidth) is stored in a .TXT file with the same name.In GRC, the "file source" and "ishort to complex" blocks can be used to process the data.

The Sampling rate used may not be supported by some MicroSD cards, it is best to use high speed class SD cards. The HackRF PortaPack Capture/Replay functionalityis  based on Havoc firmware version.

The Key Items on the App that can be selected with the cursor and changed with the encoder knob are:

* **Title bar:** The usual Items may be changed and displayed.
* **Frequency:** The setting of the frequency using the keypad can be completed and is stored in persistant memory so can be returned to when the App is used again.
* **Step Size:** The selected step size of frequency adjustment carried out by the Rotary encoder. 
* **Gain:**  Amp  (0dB or 14dB), LNA(IF) (0-40),VGA(Baseband)(0-62)
* **Rate:** The sample rate, which by its nature set the set bandwidth of capture. This is shown in the markers around the centre line of the waterfall display. The sample rate is variable from 8k5 to 2750K in 13 steps. You need to ensure that the sample rate is more than twice the bandwidth of the signal  you want to capture see [(Nyquist Principle / also called Shannon’s Law)  ](https://en.wikipedia.org/wiki/Nyquist%E2%80%93Shannon_sampling_theorem)
* **Record Button:** The red button shows as Rec or Stop. If record is selected then it will record the I/Q file. To the side of the Record Button is additional information that is shown for the recording file. 
  
     * File Name
     * % of the Storge capacity available
     * Total time left 


Please check the video below for HackRF PortaPack Capture/Replay functionality.  [![HackRF PortaPack Capture/Replay functionality](http://img.youtube.com/vi/Pe30Jvyhmzk/0.jpg)](http://www.youtube.com/watch?v=Pe30Jvyhmzk "HackRF PortaPack Capture/Replay functionality")