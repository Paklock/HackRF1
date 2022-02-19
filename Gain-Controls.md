# Gain Controls 
**The Gain Controls are  critical to the best use of the PortaPack / HackRf.**  HackRF provides three different analogue gain controls on RX and two on TX. The three RX gain controls are  RF “amp”, 0bB or +14 dB),”IF“ 0 to 40 dB in 8 dB steps), and baseband Vga ( 0 to 62 dB in 2 dB steps). The two TX gain controls are at the RF (0 or 14 dB) and IF (0 to 47 dB in 1 dB steps) stages.
 
HackRF has two RF amplifiers close to the antenna port, one for TX and one for RX. These amplifiers have two settings: on or off. In the off state, the amps are completely bypassed. They nominally provide 14 dB of gain when on, but the actual amount of gain varies by frequency. In general, expect less gain at higher frequencies. For fine control of gain, use the IF and/or baseband gain options.
 
It should be noted in the PortaPack, **the RF settings are call  either “Amp”  or not labelled**, and may be shown next to the IF / Baseband setting as a “0” or “1”  for RX or in the case of Audio App it appears when you select either IF/ Baseband gain as "Amp" on the line below. For the TX then its shown as “0” or “14" this adds 14dB of gain to the output signal. 

A good default setting for RX is to start with is RF (Amp=1) i.e. RF amp is off, IF=16, Baseband=16. Increase or decrease the IF and baseband gain controls roughly equally to find the best settings for your situation. Turn on the RF amp if you need help picking up weak signals. If your gain settings are too low, your signal may be buried in the noise. If one or more of your gain settings is too high, you may see distortion (look for unexpected frequencies that pop up when you increase the gain) or the noise floor may be amplified more than your signal is.