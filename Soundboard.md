The soundboard app will play whatever sound (in the wav/ directory of the SD card) is selected when the START button is hit, or it will play a random sound if the "Random" box is checked. Sound is transmitted as FM with the bandwidth set in the black and yellow TX box. 

![Transmit_Soundbrd](https://user-images.githubusercontent.com/164560/153706837-e95b3371-f90b-4866-bdcb-7e7f9706f8ac.png)

'Key' allows the transmitted carrier to be encoded with a CTCSS subaudiable tone, or a pilot tone for compatibility with various cordless mic systems listed below
* Axient 28kHz
* Sennheiser 32.768kHz
* Sennheiser 32.000kHz
* Sony 32.382kHz
* Shure 19kHz

Sounds should be 8-bit unsigned mono .wav files between 24000 and 48000 Hz. This can be done in Audacity by first making sure the track is Mono by going to Tracks>Mix>Mix Stereo Down to Mono and then choose "Other Uncompressed Files" in the export dialog and set Header to "WAV (Microsoft)" and Encoding to "Unsigned 8-bit PCM".

The bandwidth setting should be the sample rate in which the wav file was recorded. The provides sample wav files are sampled at 48000 Hz (48kHz). If you record your own wav source and it is sampled at a different rate, this setting should be changed to match the source sample rate.

The frequency step setting is used in tuning through the possible frequencies of a given band. In the AM band, stations have a maximum bandwidth of 10kHz, with 5kHz above and below the frequency. 