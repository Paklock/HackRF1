## About
The App can transmit various forms of noise to cause a denial of service in radio devices. This includes cell phones, cordless phones, Wi-Fi, remote controls, and other devices. A number of people have tested the jamming capability and found it to work though very dependent on the configuration the interference source, and the power of the signal. The jamming range of the system due to the low transmit power will be in the range of a few meters. Good antennas and power amplifiers can increase the strength of the jamming signal.

The App has three tabs for Range 1, Range 2, Range 3. These can be separately enabled and work in a sequential way moving from range 1,2,3. This will limit the scan time in each range and of the interfering signal that is generated. The total for the interference range is a maximum limit of 24Mhz.
The movement of the jamming signal across the band is carried out in 1MHz chunks (Hops) and the hop time is set to move to the next band segment in sequential order.

The output power of the Jammer is set at the maximum level posible, typicall 5-10dBm.
 
## Settings
The items described below are applicable to each of the 3 Range Tabs. Key Items on each of the Range App tabs, that can be selected with the cursor and changed with the encoder knob are:

* **Title bar:** The usual items may be changed and displayed.
* **Enable range:** This tick box enables this range.
* **Load Range:** This brings up the frequency ranges stored in FREQMAN directory in the SD card. Each category can be selected and then the individual ranges selected. It is good to select ranges with in the Jammer category and that you make sure they are less than 24MHz for the start to end range.
* **Start:** This set the start range. It can be manually completed or load as  part of the load Range
* **Centre:** This set the centre of the range. It can be manually completed or load as  part of the load Range
* **Stop:** This set the stop range. It can be manually completed or load as  part of the load Range 
* **Range:** This sets the range (Max 24MHz).It can be manually completed or loaded as  part of the load range
* **Type:** This is the type of jamming signal of: Random CW, SW sweep, FM tone, Random FSK. 
* **Speed:** This is the speed  the jamming signal is moved across the hop segment selected.
* **Hop:** This is the hopping interval between the 1MHz segment that the jamming signal  is transmitted . There are 6 values from 10ms to 10s. The information next to Type: (see above) e.g. 1/ 4 indicates that is the jamming signal is in the first 1MHz Hop and there are 4 hops. If the frequency is a fraction of a Hop then it will generate the Jamming signal in that Hop for the same time as other Hops
* **TX:** The Time the Jammer App is Transmitting
* **Sle3p:** The sleep time between Transmission. The mis-spelling has been placed as an expression of thanks to sponsor of a bounty to improve this App.
* **Jitter:** This setting alters the deviation from true periodicity of the signal and is used to increase the spectral density of the jamming signal. It can be set between 1 and 60.
* **Start:** This enables the start of the jamming signal an after the TX time, it will pause for the Sleep time, and then restart. If the button is pressed it will stop the transmission.

## USE 
The jamming effect is very dependent on the configuration of the above settings. It is recommended that you start with a small frequency range, if possible.  But let take Wi-Fi  in the 2.4GHz range channels 1,6 or 11. As an example as we  can generate more than 24Mhz wide the start  frequency of  2.400GHz start to 2.424GHz.  We can set:
* Type: Rand CW, 
* Speed: 10Hz, 
* Hop 10ms, 
* TX: 10Secs, 
* Sle3p: 2Secs 
* Jitter: 20/60. 

This signal unless very is very close to the device will not jam the signals even though the average power across the band is +7dBm. If the target in a narrower frequency range, then it has a greater affect, in terms of jamming due to the increase of Spectral density of thre jamming signal.
