[Tire Pressure Monitoring System (TPMS)](https://en.wikipedia.org/wiki/Tire-pressure_monitoring_system) operate in the ISM Licence free bands. In USA and most of the world they use 315mHz, in Europe the frequency is 433.92mHz. The TPMS App work well with many common standards used in the automotive industry particularly from [Schrader TPMS sensors.](https://www.schradertpms.com), and this seems a common standard used in the automotive industry.

The TPMS App display is configured to display the decoded data received from the tire pressure sensors. The interval of the data being sent by each tire is variable from every few seconds to minutes depending on the car and sensors.

## Data fields are:
* **Tp:** This is the type of the tire sensor decoded the following are coded in the App.
    * 0 = None
    * 1= FLM_64
    * 2= FLM_72
    * 3= FLM_80
    * 4= Schrader
    * 5= GMC_96
* **ID:** The ID of the tire sensor being 8 hexadecimal characters.
* **kPa:** This is the Pressure in kilo Pascals. 
* **C:** The temperature of the tire (Deg. C). Note Spurious data has been seen and may be due to failed temperature sensors giving readings like 128 or -32.
* **Cnt:** This is the count of messages received from each sensor.
* **Flags:** Information on the type of sensor is only for Schrader and have decode for: fsk_19k, ook_8k192, ook_8k4.


