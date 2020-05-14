In theory, it is impossible to brick the device, since you can always try the DFU recovery procedure. However, the updating might become fiddly in certain conditions.

# Normal procedure

1. Connect the device via USB
2. Switch to HackRF mode via the on-screen option (in the PortaPack)
3. Double click `flash_portapack_mayhem.bat` and follow the instructions
4. Reboot the device

# Troubleshooting

One of the main sources of problems is the quality of the USB cable. Try with several ones just to be sure before trying any other solution.

## DFU

This is a special mode to update the firmware in case of problems. To enable this, you should reset your device holding the RESET and DFU buttons at the same time, while doing this, release RESET, and then release DFU. The leds should be ON and the screen wont show anything.

If you are in Windows, from the release package double click `dfu_hackrf_one.bat` and follow the instructions. Do not disconnect or reset your PortaPack after that procedure, continue in the step 3 of the [normal procedure](Update-firmware#normal-procedure).

## Alternative environment

You may be able to try in a virtual environment, completely isolated from your current OS:
1. Download http://eu2-dist.gnuradio.org/ and burn the ISO and boot from it, select the LIVE Image
2. Once in the environment, Open a Command Prompt and type: `sudo apt-get install dfu-util`
3. Connect your device to your computer
4. Press RESET and DFU buttons at the same time, and while doing this, release RESET, and then release DFU
5. Open a terminal and type `dfu-util --device 1fc9:000c --download hackrf_one_usb.dfu --reset`
6. After that, without disconnecting it, you can upload the firmware with `hackrf_spiflash -w new_firmware_file.bin`

## Video
The following video explains all possible outcomes while trying to update the firmware and possible mitigations:
https://www.youtube.com/watch?v=_zx4ZvurgOs

# Still stuck?
If you still experience problems after reading this and checking the video, submit an [issue](https://github.com/eried/portapack-havoc/issues/new?assignees=&labels=&template=problem-upgrading-the-firmware.md&title=Problem+upgrading+the+firmware).

Also, there is a lot more details on the [HackRF wiki](https://github.com/mossmann/hackrf/wiki/Updating-Firmware).