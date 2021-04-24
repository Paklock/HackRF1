The soundboard app will play whatever sound (in the wav/ directory of the SD card) is selected when the START button is hit, or it will play a random sound if the "Random" box is checked. Sound is transmitted as FM with the bandwidth set in the black and yellow TX box. 

[[img/screenshots/Transmit_Soundbrd.png]]

'Key' allows the transmitted carrier to be encoded with a CTCSS subaudiable tone, or a pilot tone for compatibility with various cordless mic systems listed below
* Axient 28kHz
* Sennheiser 32.768kHz
* Sennheiser 32.000kHz
* Sony 32.382kHz
* Shure 19kHz

Sounds should be 8-bit unsigned mono .wav files between 24000 and 48000 Hz. This can be done in Audacity by first making sure the track is Mono by going to Tracks>Mix>Mix Stereo Down to Mono and then choose "Other Uncompressed Files" in the export dialog and set Header to "WAV (Microsoft)" and Encoding to "Unsigned 8-bit PCM".