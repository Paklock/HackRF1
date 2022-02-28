The following is based on extracts from HackRF Documentation that can be found [here.](https://hackrf.readthedocs.io/en/latest/)

## What is the minimum signal power level that can be detected by HackRF?
This isn’t a question that can be easily answered for a general purpose SDR platform such as HackRF. Any answer would be very specific to a particular application, and is determined by many factors including:


* **Modulation:** The Modulation Depth and type used (M)
* **Frequency:** That is used (F).
* **Software:** that is designed (S). 
* **Configuration:**  of the App (C ).
* **Bit error rate:** The % error experienced (E).

Changing any of those variables (M, F, S, C, or E) would change the answer to the question. Even a seemingly minor software update might result in a significantly different answer. To learn the exact answer for a specific application, you would have to measure it yourself.
The Receivers Apps have a variable sensitivity to radio signals, and it should be considered that The HackRF has a much weaker performance compared to an optimised radio system designed to operate at set frequencies. In addition, it will be open to interference and spurious signals as it does not have any RF filtering. This would need to be provided by the addition of External filters. There are many relatively cheap ones available to purchase with good performance.

These specifications can be used to roughly determine the suitability of HackRF for a given application. Testing is required to finely measure performance in an application. Performance can typically be enhanced significantly by selecting an appropriate antenna, external amplifier, and/or external filter for the application.

## What is the Receive Power of HackRF?
The maximum RX power of HackRF One is -5 dBm. Exceeding -5 dBm can result in permanent damage! This is often seen, see notes on [Preamplifier IC replacement](https://github.com/eried/portapack-mayhem/wiki/Preamplifier-IC-replacement)

In theory, HackRF One can safely accept up to 10 dBm with the front-end RX amplifier disabled. **However, a simple software or user error could enable the amplifier, resulting in permanent damage.** It is better to use an external attenuator than to risk damage.




