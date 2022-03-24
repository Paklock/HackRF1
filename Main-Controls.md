## Step size
The step size when changing frequency can be changed as a secondary function when the frequency is selected. The range of settings are: 10M,1M,500k,250(N2),100k(FM2),50k(FM1),25k(EU NFM),12k5(EU NFM),10k(US AM),9k(EU AM),8.33k(AIR),6k3 (EU DIG),5k(SA AM),3k,1k, and 100Hz.

## Bandwidth
It is often the case that the PortaPack user does not know the filter bandwidth to use or what they have selected. The system uses: Finite  Impulse Response (FIR) Filters and the settings are held in the dsp_fir_tap_hpp file, and are selected from the use interface.  They can be selected for different modulation modes.

* **NFM:** It should be noted for the NFM, there are 3 emission types 16KF3E (16k),11KF3E (11k)and 8K5F3E (8k5) .The 16k option should be selected when the channel spacing is 25kHz. For 12.5kHz then normally 8.5kHz should be used, but some over modulated system may benefit with using the 11kHz bandwidth filter. 

* **WFM:** This is emission types 200KF8E emission type. The Wide Band filter is limited to 96kHz stereo signal and then combined to a 48Khz mono signal.


* **AM:**  The AM emission types supported are:

* _6K00A3E for AM double sideband 6kHz._
* _2K80J3E for AM Lower Side Band LSB -3 - 0kHz._
* _2K80J3E for AM Lower Side Band USB 0 - 3kHz._
* _150HA1A / 150HJ2A for AM Continuous Wave. The filter is 200 Hz wide and centred around 700Hz._

* **TPMS:** This is a non standard specialized shaped filter that is 200kHz wide. 

## Gain Controls 
**The Gain Controls are  critical to the best use of the PortaPack / HackRf.**  HackRF provides three different analogue gain controls on RX and two on TX. The three RX gain controls are  RF “amp”, 0bB or +14 dB),”IF“ 0 to 40 dB in 8 dB steps), and baseband Vga ( 0 to 62 dB in 2 dB steps). The two TX gain controls are at the RF (0 or 14 dB) and IF (0 to 47 dB in 1 dB steps) stages.
 
HackRF has two RF amplifiers close to the antenna port, one for TX and one for RX. These amplifiers have two settings: on or off. In the off state, the amps are completely bypassed. They nominally provide 14 dB of gain when on, but the actual amount of gain varies by frequency. In general, expect less gain at higher frequencies. For fine control of gain, use the IF and/or baseband gain options.
 
It should be noted in the PortaPack, **the RF settings are called either “Amp” or not labelled**, and may be shown next to the IF / Baseband setting as a “0” or “1”  for RX or in the case of Audio App it appears when you select either IF/ Baseband gain as "Amp" on the line below. For the TX then its shown as “0” or “14" this adds 14dB of gain to the output signal. 

A good default setting for RX is to start with is RF (Amp=1) i.e. RF amp is off, IF=16, Baseband=16. Increase or decrease the IF and baseband gain controls roughly equally to find the best settings for your situation. Turn on the RF amp if you need help picking up weak signals. If your gain settings are too low, your signal may be buried in the noise. If one or more of your gain settings is too high, you may see distortion (look for unexpected frequencies that pop up when you increase the gain) or the noise floor may be amplified more than your signal.


