Are you bored of the standard power on screen?
Do you want your own image at power up to personalise your device?
You can!

Prerequisites:
Some form of linux command line such as WSL or a bash/sh prompt
A graphics program such as GIMP (Gnu Image Manipulation Program)
xxd (available from your packet manager, in Debian-based systems sudo apt install xxd)

Create (or load) an image

Resize (or crop) it to width 240 height 304 (the LCD is 320x240, rotated 90 degrees so 240x320, with 16 pixels deducted for the top line)

If you want to add text, do it after the next step so the text looks as clear as possible.

Change the image to an optimised 256 colours (8 bit) or 16 colours (4 bit) palette. Consider also greyscale 8 bits, it can make a so-so image look brilliant.
As mentioned, any text you wish to overlay should be added now.

Export the image as Windows bitmap, RLE (run length encoded) if possible. RLE means that any colours the same get merged into one making the filesize much smaller.
Save it as splash.bmp to a directory such as ~/Pictures

Open a terminal window

Change directory to where the image was saved (for example ~/Pictures):
cd ~/Pictures
Convert the image to a c++ header file:
xxd -i splash.bmp bmp_splash.hpp

Make a backup of the existing splash screen
Change directory to the path to where you downloaded the Mayhem source eg ~/src/portapack_mayhem
cd ~/src/portapack_mayhem
mv firmware/application/bitmaps/bmp_splash.hpp firmware/application/bitmaps/bmp_splash.hpp.backup

Copy the new splash screen to here
cp ~/Pictures/bmp_splash.hpp firmware/application/bitmaps/bmp_splash.hpp

Finally, rebuild the source and flash the HackRF One and PortaPack.

