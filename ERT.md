[Encoder receiver transmitter](https://en.wikipedia.org/wiki/Encoder_receiver_transmitter) (ERT) is a packet radio protocol developed by Itron for automatic meter reading of water, gas and electricity. The system uses OOK short range radio which is transmitted in the unlicensed 900-920 MHz band, so that meters can be read from a passing vehicle. This is mainly used in USA. The data is not encrypted, and does not have functions to enable full control. The system is not as advanced as a smart meter and lacks the control or  security in the data transfered.
ERT

The Key Items on the App that can be selected with the cursor and changed with the encoder knob are:

* **Title bar:** The usual Items may be changed and displayed.
* **Gain:** Setting are shown in order of AMP 0=0db or 1=14dB, LNA(IF) (0-40) and VGA (Baseband Gain) (0-62).
* **ID:** this is the meter ID.
* **Tp:** This is the type of meter. 0=Unknown,1 =IDM, 2=SCM.
* **Consumpt:** The Meter reading value.
* **Cnt:** The count of the number of readings.

The PortaPack ERT receiver monitors approximately 2.5 MHz centered around 911.6 MHz. It does not implement channel filters, so sensitivity is reduced in exchange for monitoring more simultaneous "channels".

If a FAT-formatted micro SD card is present when this mode is entered, the receiver will log received packets to a file named "ERT.TXT". The log file contains one line per packet received. Each line consists of a timestamp in sortable "YYYYMMDDHHMMSS" format, the Manchester-decoded data bits, a "/", and a per-bit Manchester coding error indicator ("1" if the data bit is in error). 



 
