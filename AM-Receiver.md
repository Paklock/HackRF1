# High Level Description
The AM Receiver is a Sub-Application of the Audio Receiver Application.
Its purpose is to Demodulate and Record RF Signals modulated using the [Amplitude Modulation](https://en.wikipedia.org/wiki/Amplitude_modulation) scheme. It can demodulate Double-Sideband AM (ITU Designation: A3E) and both Lower-Sideband and Upper-Sideband Single-Sideband AM (ITU Classification: R2E, H3E, J3E) signals.

# User Interface 
The AM Receiver uses the Standard UI Layout, which has the following features (in UI order). Some features only become available when the Parent item is selected.
* Switch Sub-Application (AM, WFM, NFM, SPEC)
  * Switch Modulation type (DSB/USB/LBS/CW)
* Change Frequency
  * Change tuning step-size
* Increase/Decrease Baseband Gain
  * Enable Amplifier
* Increase/Decrease IF Amplifier Gain
* Increase/Decrease Audio Volume Level
* Commence Recording
