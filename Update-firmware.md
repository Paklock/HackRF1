In theory, it is impossible to brick the device, since you can always try the DFU recovery procedure. However, the updating might become fiddly in certain conditions.

# Normal procedure

## Firmware

Get the latest firmware from the [![GitHub release (latest by date)](https://img.shields.io/github/v/release/eried/portapack-mayhem?label=Releases&style=social)](https://github.com/eried/portapack-mayhem/releases/latest) page. Please check the [FAQ](https://github.com/eried/portapack-mayhem#frequently-asked-questions) if you have any additional question.

### Windows

1. Connect the device via USB
2. Switch to HackRF mode via the on-screen option (in the PortaPack)
3. Double click `flash_portapack_mayhem.bat` and follow the instructions
4. Reboot the device

### Linux

1. Connect the device via USB
2. Switch to HackRF mode via the on-screen option (in the PortaPack)
3. Upload the firmware with `hackrf_spiflash -w new_firmware_file.bin` (eg. portapack-h1_h2-mayhem.bin for mayhem firmware or hackrf_one_usb.bin for stock hackrf firmware)
4. Reboot the device

### MacOS

_HackRF CLI tools for MacOS available through MacPorts or Homebrew_

1. If necessary, install the HackRF tools: `brew install hackrf`
2. Connect the device via USB
3. Switch to HackRF mode via the on-screen option (in the PortaPack)
4. Upload the firmware with `hackrf_spiflash -w new_firmware_file.bin` 
5. Reboot the device

## MicroSD card files

Your PortaPack has a slot for a memory card. You need to provide a MicroSD with enough space (16GB is recommended, over 32GB will be omitted due the limits of the FAT32). This is necessary for certain functionality, like the world map, GPS simulator, and others. 

Get the latest files from the [![GitHub release (latest by date)](https://img.shields.io/github/v/release/eried/portapack-mayhem?label=Releases&style=social)](https://github.com/eried/portapack-mayhem/releases/latest) page. You need to uncompress (using [7-zip](https://www.7-zip.org/download.html)) the files from `mayhem_vX.Y.Z_COPY_TO_SDCARD.7z` to a FAT32 formatted MicroSD card. 

# Troubleshooting

Please check [this guide](Update-firmware-troubleshooting).