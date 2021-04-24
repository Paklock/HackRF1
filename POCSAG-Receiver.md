With this app you can receive pager messages using the POCSAG protocol.

This protocol operates in the VHF/UHF bands using FSK modulation. More technical details can be found by following the links in the References section.

# Display summary

[[img/screenshots/Receive_POCSAG.png]]

Description of displayed information, starting from top-left:

- Receiver frequency, RF amplifier, LNA, VGA, RSSI and Channel indicators
- Phase, Bit/baud rate, Log checkbox
- Ignore address checkbox and address
- The lower area of the display will show the latest received messages.

## Settings

- **Frequency**: Sets the frequency to receive pager messages on. Can be adjusted with the [encoder thumb wheel](Hardware-overview), on-screen numpad, or loaded from frequencies saved on an SD card.
- **RF amplifier**: (0 or 1): Enables/disables the internal RF amplifier.
- **LNA gain** (0, 8, 16, 24, 32, 40): Sets the LNA gain. Further information: [Description of the gain settings](Help!-Im-not-receiving-anything!---Receive-Quality-Issues#description-of-the-gain-settings)
- **VGA gain** (0 to 62): Sets the VGA gain. Further information: [Description of the gain settings](Help!-Im-not-receiving-anything!---Receive-Quality-Issues#description-of-the-gain-settings)
- **Phase** (Positive or Negative): Usually set to positive. Typically the FSK lower frequency designates a high bit. Setting the phase polarity to negative will invert this, so the FSK lower frequency now designates a low bit.
- **Data rate** (512pbs, 1200bps, 2400bps): Sets the baud rate (bits per second) of the received data. Typically older paging systems use 512bps, while newer systems use 1200bps or 2400bps.
- **Log checkbox**: Enable/disable logging of received messages to an SD card. This log can be found on the SD card root directory, filename: `pocsag.txt`.
- **Ignore address checkbox**: Used to ignore messages sent to the address set.

## Message display

Typical received message:

```plaintext
12:34 1200bps ADDR:432123 F2
This is a test message
```

Description (from top-left):

- `12:34` - **Time**: The time that the message was received (time from PortaPack).
- `1200bps` - **Data rate**: The data rate used to receive the message.
- `ADDR:432123` - **Address**: The address of the intended pager recipient.
- `F2` - **Function**: (0 to 3) Indicates the type or source of message sent (can be used to provide a category of sorts).
- `This is a test message` - **Message**: The message data displayed as ASCII.

# References

The following resources provide more technical information about the POCSAG protocol:

- [POCSAG - Signal Identification Wiki](https://www.sigidwiki.com/wiki/POCSAG) - Provides frequencies commonly used in different countries and regions
- [POCSAG - WikiPedia](https://en.wikipedia.org/wiki/POCSAG)
