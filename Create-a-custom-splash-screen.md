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

----------------------
Someone asked whether it would be possible to just load a .PNG or .JPG image into the device.

A quick solution to this would be to use the [ImageMagick](https://imagemagick.org/script/download.php) ```convert``` function which would take an image, resize it to fit the screen and change the filetype to a 4 bit RLE .BMP image in one step, meaning you just create a suitable image, save it as a .JPG or .PNG (or whatever type you prefer).

If the file is already the correct resolution:
```convert filename.jpg -type Palette -compress RLE -colors 16 BMP3:splash.bmp
xxd -i splash.bmp bmp_splash.hpp```

If the file needs resizing to fit:
```convert -resize 240x304 filename.jpg -type Palette -compress RLE -colors 16 BMP3:splash.bmp
xxd -i splash.bmp bmp_splash.hpp```

Note that the ```-resize 240x304``` part of the line will not necessarily resize the new image to exactly 240x304px, it will keep the aspect ratio so that one of the sides will be correct and the other one will scale properly.
