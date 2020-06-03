For converting back and forth between the image and source you can use `xxd`. In a Windows environment you can use this command in the Linux Subsystem installing one of the versions available (i.e. [Ubuntu](https://ubuntu.com/tutorials/tutorial-ubuntu-on-windows#1-overview)). 

### From .bmp to .hpp
`xxd -i input_image.bmp output.hpp`

### From .hpp to .bmp
`xxd -r -p input.hpp output_image.bmp `

# Firmware icons

There is a special file that contains all the firmware icons `firmware\application\bitmap.hpp` but this file should not be edited directly, instead, new icons should be created in `firmware\graphics` and then run `firmware\tools\make_bitmap.py <DIRECTORY>` to create `bitmap.hpp`.

For operating that Python3 script, `Pillow` library is required: `pip install pillow`

From bash, the command that creates and moves the bitmap file is:

`python3 make_bitmap.py ../graphics/ && mv bitmap.hpp ../application/bitmap.hpp`
