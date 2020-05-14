In theory, it is impossible to brick the device, since you can always try the DFU recovery procedure. However, the updating might become fiddly in certain conditions.

# Normal procedure

1. Connect the device
2. Switch to HackRF mode via the on-screen option
3. Use `hackrf_update new_firmware_file.bin`
4. Reboot the device

# Troubleshooting

One of the main sources of problems is the quality of the USB cable. Try with several ones just to be sure before trying any other solution.

## DFU

This is a special mode to update the firmware in case of problems. To enable this, you should reset your device holding the RESET and DFU buttons at the same time, while doing this, release RESET, and then release DFU. Now you are able to use `dfu-util`. The leds should be ON and the screen wont show anything.

You may use the following:

`dfu-util --device 1fc9:000c --download hackrf_one_usb.dfu --reset`

And after that, without disconnecting it, you can upload the firmware:

`hackrf_spiflash -w new_firmware_file.bin`

## Alternative environment

You may be able to try in a virtual environment, completely isolated from your current OS:
1. Download http://eu2-dist.gnuradio.org/ and burn the ISO and boot from it, select the LIVE Image
2. Once in the environment, Open a Command Prompt and type: `sudo apt-get install dfu-util`
3. Connect your device to your computer and follow the DFU instructions above

## Video
The following video explains all possible outcomes while trying to update the firmware and possible mitigations:
https://www.youtube.com/watch?v=_zx4ZvurgOs

# Still stuck?
If you still experience problems after reading this and checking the video, submit an [issue](https://github.com/eried/portapack-havoc/issues/new?assignees=&labels=&template=problem-upgrading-the-firmware.md&title=Problem+upgrading+the+firmware).

Also, there is a lot more details on the [HackRF wiki](https://github.com/mossmann/hackrf/wiki/Updating-Firmware).