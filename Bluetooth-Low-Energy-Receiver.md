This is to discover the MAC address of Bluetooth Low Energy device around you.
It's not perfect because decoded data can't pass CRC, hence there will be 1~2 bit error in result.

![Result of bluetooth hardware(hcitool lescan)](https://user-images.githubusercontent.com/17997195/77241595-5693a200-6c2f-11ea-94fb-2e8ff8a780aa.jpeg)
![Result of portapack btle search](https://user-images.githubusercontent.com/17997195/77241602-75923400-6c2f-11ea-98a2-1ad0a1c09aba.jpeg)

You don't need to change the frequency, since all Bluetooth device will broadcast on the pre-set frequency.
You might need to adjust gain though.

Theoretically, it's possible to decode some data in the ble packets, like temperature, but it doesn't make sense if there is bit error. 

## References:

https://blog.csdn.net/shukebeta008/article/details/105024278