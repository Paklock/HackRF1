# Brief History about the Temperature Logger

Some subsystems inside the Portapack would benefit from some sort of temperature compensation being added into the code, as discussed [in the original Portapack Github repository](https://github.com/sharebrained/portapack-hackrf/issues/8) with it's developer.

Such need gave birth to the Portapack temperature logger, accessible from **DEBUG->Temperature** menu options.

Temperature data is provided by the **MAX2837 On-Chip Digital Temperature Sensor**. MAX2837 Datasheet can be [found here](https://datasheets.maximintegrated.com/en/ds/MAX2837.pdf).

But, if you read the discussion about it on the earlier Github link, the temperature precision on the MAX2837 is too coarse (about +/- 5ºC) to be really useful. 

This is why jboone, the Portapack creator, finally decided this value had no real use and thus the temperature widget further development / refinement and usage enhancement was dropped.

## MAX2837 Temperature Sensor
Monitoring MAX2837 temperature is important because it's **VCO** (Voltage Controlled Oscillator) is able to maintain lock only while inside +/- 40ºC variation from ambient temperature. 

_**NOTE:** The MAX 2837 operating temperature range goes from -40ºC to +85ºC._

This sensor can be activated and read through the SPI interface. By accessing the **TEMP_SENSE** register we can read the ADC output with a precision of **5 bits**.

The datasheet provides the following reference values:

* `TA = +25ºC  -> 01111  (DEC 15)`
* `TA = +85ºC  -> 11101  (DEC 29)`
* `TA = -40ºC  -> 00001  (DEC 1)`

In short, the temp sensor inside MAX2837 returns a decimal number between 1 and 29 for a -40ºC to +85ºC temperature range, which would put the **precision on about 4.33ºC per each value**. 

_**NOTE:** As Jboone stated on the Github link provided above, this is definitely a **coarse precision** value._

### Temperature Reading
This is accomplished on `/firmware/application/hw/max2837.cpp` with the following code:

```
reg_t MAX2837::temp_sense() {
	if( !_map.r.rx_top.ts_en ) {
		_map.r.rx_top.ts_en = 1;
		flush_one(Register::RX_TOP);

		chThdSleepMilliseconds(1);
	}

	_map.r.rx_top.ts_adc_trigger = 1;
	flush_one(Register::RX_TOP);

	halPolledDelay(ticks_for_temperature_sense_adc_conversion);

	const auto value = read(Register::TEMP_SENSE);

	_map.r.rx_top.ts_adc_trigger = 0;
	flush_one(Register::RX_TOP);

	return value;
}
```

The above code follows the max2837 datasheet's **Temperature Sensor Readout Through DOUT Pin** procedure, which includes the following steps:

* Enable on-chip temperature sensor by setting address 9 (**RX_TOP**), register 1 (**ts_en**) with value 1.

* Wait a while ( suggested 100us to 1ms, Portapack code waits 1ms) for the sensor to stabilize and settle within 5 to 1 ºC precision.

* Trigger the ADC conversion by setting **RX_TOP** register 0 (**ts_adc_trigger**) with value 1

* According to the max2837 datasheet, the ADC will acquire the temperature value in 2us time (but as we follow the definition of **ticks_for_temperature_sense_adc_conversion** we find a comment in Portapack's code stating a wait of 25 us -shrug-).

* Get the temperature by reading address 7  (**TEMP_SENSE**)

* Finally, turn off the ADC converter by setting address **RX_TOP**, register **ts_adc_trigger** with value 0

## Temperature Logging
The logging code functions can be found at `/firmware/application/temperature_logger.cpp`.

There is an array **uint8_t samples** dimensioned for 128 temperature values. The sample_interval is set at 5 seconds between each read_sample().

The m0 events dispatcher **handle_rtc_tick** located at `/fimrware/application/event_m0.cpp` taps periodically into the function second_tick(). When the number of seconds defined by **sample_interval** is reached, the temperature is measured and pushed into the **samples** array. 

## Temperature Graphic
The temperature graph widget is defined on `/firmware/application/apps/ui_debug.cpp`.

It should graph the 128 temperature values, stored on the samples arrray. On the botton right side o te graph, it shows the most recent logged value.

### Our first Analysis

_**Warning:** Here is when things get weird (for me at least)._ The Temperature Widget **seems** to be wrong ("Spoiler": Later I learn it is ok):

* First, the temperature graph had the y axis going from 0ºC to 60ºC (which at first glance is not aligned with MAX2837 temp data output, going from -40ºC to 85ºC).

* Secondly, when plotting each temperature value, the original sensor value is processed through the following function: `return -45 + sensor_value * 5;` which seems a bit off, particularly when tested against the Ambient Reference sensor value of 15 (for 25ºC) according to the MAX2837 Datasheet. 

## Testing the Temperature graph

For our tests, we bypass the ºC conversion functionality in order to watch the **raw decimal value** being returned by the MAX2837 On-Chip Digital Temperature Sensor.

### First test
With our Portapack on, in iddle mode, the sensor **returns a value of 9** . If converted into ºC, such value should correspond to a temperature of about 0 / 1 ºC, which **seems to be wrong** (test room temperature is about 20ºC, and Portapack aluminium case is at about 26.7ºC). 

### Second test
I placed my Portapack in transmit mode, loop-playing a random earlier captured radio sample for about 30 minutes. The exterior aluminium case is at about 31.4ºC. 

Right after stopping the transmission, the sensor value is 10. We give it about 10 seconds and the value drops to 9. But Portapacks aluminium case is still about 31.4ºC.

### Third test
I placed my Portapack outside, where it cooled down for about 30 minutes (Temperature outside is about 15ºC).

Back inside, when powered up I got a first sensor value of 7, which would correspond to -10ºC. Room temperature is about 22ºC

About a minute later the sensor value increased by one, returning 8, which should correspond to -5ºC. Portapack's case temp was about 20ºC

### Our second analysis

My observation indicates that MAX2832 temperature sensor is NOT giving out an absolute temp value (It reflects neither the ambient temperature inside the Portapack, nor an on-chip temperature). 

At first glance, this sensor value **might** be the relative temperature change (increase) between ambient temperature (Which goes up when Portapack is transmitting, as evidenced on the aluminium case external measurement) and the MAX2837 temperature itself.

So what could be wrong ? We consider the following:

* MAX2837 Datasheet may be wrong
* We are not correctly interpreting the MAX2837 description for the On-Chip Digital Temperature Sensor
* Portapack's code might have a bug and reading are wrong

After more code delving, a conclusion is reached: MAX2837 documentation is failing to correctly explain the On-Chip Digital Temperature Sensor values.

## MAX2837 Temperature Sensor "redefined"

Apparently, the sensor returns the temperature difference between ambient temperature and MAX2837 temperature!

* Which could only be positive. 
* Which would be **at most**, 60ºC over ambient temperature (all things considered).
* Which would satisfactorily explain why the Widget presents a chart ranging from **0ºC to 60ºC**.
