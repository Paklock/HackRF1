This is to discover the MAC address of Bluetooth Low Energy device around you.
It's not perfect because decoded data can't pass CRC, hence there will be 1~2 bit error in result.

You don't need to change the frequency, since all Bluetooth device will broadcast on the pre-set frequency.
You might need to adjust gain though.

Theoretically, it's possible to decode some data in the ble packets, like temperature, but it doesn't make sense if there is bit error. 