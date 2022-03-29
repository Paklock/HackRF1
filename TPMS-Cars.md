[Tire Pressure Monitoring System (TPMS)](https://en.wikipedia.org/wiki/Tire-pressure_monitoring_system) operate in the ISM Licence free bands. In USA and most of the world they use 315mHz, in Europe the frequency is 433.92mHz. The TPMS App work well with many common standards used in the automotive industry particularly from [Schrader TPMS sensors.](https://www.schradertpms.com), and this seems a common standard used in the automotive industry.

The TPMS App display is configured to display the decoded data received from the tire pressure sensors. The interval of the data being sent by each tire is variable from every few seconds to minutes depending on the car and sensors.

The Key Items on the App that can be selected with the cursor and changed with the encoder knob are:
Title bar: The usual Items may be changed and displayed.
* **Frequency:**  Either 315mHz or 433.92mHz
* **KPa/PSI :**  By highlighting this item it can be changed between the different value type of pressure that are displayed.
* **Gain:** Setting are shown in order of Amp 0=0db or 1=14dB, LNA(IF) (0-40) and VGA (Baseband Gain) (0-62). 

## Data fields are:
* **Tp:** This is the type of the tire sensor decoded the following are coded in the App.
    * 0 = None
    * 1= FLM_64
    * 2= FLM_72
    * 3= FLM_80
    * 4= Schrader
    * 5= GMC_96
* **ID:** The ID of the tire sensor being 8 hexadecimal characters.
* **kPa:** This is the pressure in kilo Pascals.
* **PSI:** This is the pressure in Pounds Per squre Inch.
* **C:** The temperature of the tire (Deg. C). Note Spurious data has been seen and may be due to failed temperature sensors giving readings like 128 or -32.
* **Cnt:** This is the count of messages received from each sensor.
* **Flags:** Information on the type of sensor is only for Schrader and have decode for: fsk_19k, ook_8k192, ook_8k4.

If a FAT-formatted micro SD card is present when this mode is entered, the receiver will log received packets to a file named "TPMS.TXT". The log file contains one line per packet received. Each line consists of a timestamp in sortable "YYYYMMDDHHMMSS" format, receiver frequency, modulation, deviation, symbol rate, and data. The data field consists of Manchester-decoded data bits, a "/", and a per-bit Manchester coding error indicator ("1" if the data bit is in error).