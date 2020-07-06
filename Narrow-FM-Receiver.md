# High Level Description
The Narrow FM Receiver is a Sub-Application of the Audio Receiver Application.
Its purpose is to Demodulate and Record RF Signals modulated using the [Frequency Modulation](https://en.wikipedia.org/wiki/Frequency_modulation) scheme. It can demodulate mono Narrow FM signals with bandwidths from 8.5KHz to 16KHz.Such signals are commonly used for two-way communication.

# User Interface 
The NFM Receiver uses the Standard UI Layout, which has the following features (in UI order). Some features only become available when the Parent item is selected.
* Switch Sub-Application (AM, WFM, NFM, SPEC)
  * Switch FM Bandwidth (8.5KHz, 11KHz, 16KHz)
  * Configure Squelch level
* Change Frequency
  * Change Step-size
* Increase/Decrease Baseband Gain
  * Enable Amplifier
* Increase/Decrease IF Amplifier Gain
* Increase/Decrease Audio Volume Level
* Commence Recording