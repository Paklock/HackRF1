For converting back and forth between the image and source you can use `xxd`. In a Windows environment you can use this command in the Linux Subsystem installing one of the versions available (i.e. [Ubuntu](https://ubuntu.com/tutorials/tutorial-ubuntu-on-windows#1-overview)). 

### From .bmp to .hpp
`xxd -i input_image.bmp output.hpp`

### From .hpp to .bmp
`xxd -r -p input.hpp output_image.bmp `