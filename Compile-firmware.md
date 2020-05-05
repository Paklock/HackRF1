The easiest way is to use Docker. After you install Docker in your machine, if you are inclined for using the command line, you can try the following:

For building:

`docker build -t portapackccache -f dockerfile-nogit .`

For running (in the root of the repo):

`docker run -it -v ${PWD}:/havoc portapackccache`

# Using Docker Hub and Kitematic
The required Docker image is also in Docker Hub, browse for it in [Kitematic](https://github.com/docker/kitematic):

[[img/Kitematic_MChWCyp6g1.png]]

You need to configure the path to the source code from the Volumes of the container as show in the image below. Everytime you run this container, it will compile the source and (if successful) leave the results in `build/firmware/`

[[img/Kitematic_VL5an8rufV.png]]