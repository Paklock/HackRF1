# Looking Glass
This App Provides a view of the spectrum over a set range of frequencies. The waterfall display is updated with each full scan. It should be noted that for wide scan frequency ranges the scanning time is very long and the display can look like it has frozen. The key is to keep the band scanned as small as possible. While the HackRF is in RF terms a poor receiver in terms of sensitivity, the Portapack/ HackRF can provide a very useful to scan for local Radio signals Using the appropriate antenna. The Looking glass is an excellent tool to visualise the spectrum and if set to a narrow scanning range can see the on/off patterns of the radio transmission.

The frequency ranges are held in the SD card >LOOKINGGLASS>PRESETS.TXT. It should be noted that the size of the frequencies should be keep small to limit the memory use.

# Key Controls 
* MIN / MAX: Place the cursor on the “MIN” or “MAX” fields and use the rotary encode to select the frequencies for the MIN and MAX frequencies in increments of 240mHz. The Label “RANGE” shows the scan range set.
* Gain: Gain Setting:  Cursor can be used to select and adjust the LNS(IF) (0-40), VGA(0-62) and RF AMP “0” (off)  and 1 (14dB).
* FILTER: Move the cursor to the FILTER field and select either OFF, MED, HIGH. These setting adjust the display  to show differing views ( that do change depending on the Speed of scan and  Gain settings.  Use the One that give the best contrast of the detected signals.
* PRESET: Move the cursor to the “PRESET:” field to select one of the pre-set frequency ranges set in the SD Card.
* MARKER: If you place cursor over the field and turn the rotary encoder a red marker arrow will appear on top of the cascade so you can see approximate idea of the frequency for each pixel. The interval of the marker that is changed by the encoder knob, is shown and is based on the scan range. If you press the encoder know or Button then it will take you to the Audio App for more detailed view of the signal with setting of 1mHz Steps and a 10mHz view. Unfortunately, on return to the LOOKINGGLASS App the display goes to default settings.

* RESOLUTION: The field can be changed by the rotary encoder to select the resolution (FFT Trigger point) (2-128). The default setting is 32.  This allows the display to show better the Signals received and should be adjusted in conjunction with “Gain:” and “FILTER:” 
