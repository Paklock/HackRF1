## **This is a potentially dangerous App, if the HackRF is used to generate valid ADS-B messages and these radiated then it could affect both how aircraft and navigation systems see each other. Therefore, it should only be used in a closed RF environment or when there is no direct transmission.**

The Key Items on the App that can be selected with the cursor and changed with the encoder knob are:

* **Title bar:** The usual Items may be changed and displayed.
* **Tab pages:** The Tab pages for the settings that are can be selected are **Position, Callsign, Speed, Squark**. This data is not held in persistent memory except for the frequency.

## Position Tab
**ICAO24:**  This code is selected with rotary encoder to enter the 6 digit numeric  number. This is sometimes called the Mode S code and is a 24-bit unique number that is assigned to each vehicle or object that can transmit ADS-B messages. It is usually transmitted by aircraft but some airport ground vehicles and multi-lateration towers also have ICAO24 codes assigned to them.
Transmit position: this is a tick box to enable the transmission of Alt. Lat. Lon
* **Alt:** Sets height in feet.
* **Lat:**  Setting of Latitude is in Degrees Minutes and Second and set with encoder knob. The numeric value is given to the right hand side 
* **Lon:** Setting of Longitude is in Degrees Minutes and Second and set with encoder knob. The numeric value is given to the righthand side.
* **Set from Map:** the Lat and long can be set form the map view and using the touch screen if desired. Note to save the value is a “OK” button but this is hidden behind the Digital values of the Lat and Lon. But if you touch this, are it will appear.

## Callsign Tab
* **Transmit callsign:** This is a tick box to turn on the transmission of the [Callsign](https://en.wikipedia.org/wiki/Aviation_call_signs). The callsign is entered in the text pad and is 8 characters long. 

## Speed Tab
* **Transmit speed:** This is a tick box to turn on the transmission of the speed. 
* **Speed: ** The value is selected and the rotary encoder is used to select the value 0-999km.
* **Bearing:** The value is selected and the rotary encoder is used to select the value 0-999km. 0-359 Degrees.

## Squark Tab 
* **Transmit squark:** This is a tick box to turn on the transmission of the [Squark](https://en.wikipedia.org/wiki/List_of_transponder_codes) code. 
* **Squark:** This can be selected with rotary encoder and has specific meanings. The code is from 0-9999.   https://en.wikipedia.org/wiki/List_of_transponder_codes

## Common to all Tabs 
* **Frequency:** At the lower part of the App is the Frequency setting. This is stored in persistent memory 
* **Step size:** This is next to the frequency and allows the selection of the standard step sizes.
* **Gain:** The gain setting are below the frequency and marked (0-47) LNA(IF) and AMP 0=0db or 1=14dB.
* **Start:** This button starts the transmission and if pressed again can stop the transmission.
