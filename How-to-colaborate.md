# Write documentation

There is a lot of missing documentation about all the features, so it is really important to write clean and detailed instructions for them. In this current wiki, you can modify or add new content with a normal Github account. 

1. Select a topic you think you can master. It can be an specific app, function of an app or feature or procedure related with your PortaPack
2. Check the following sources:
    * https://github.com/mossmann/hackrf/wiki
    * https://github.com/furrtek/portapack-havoc/wiki
    * https://github.com/sharebrained/portapack-hackrf/wiki
3. To create a new section, you have to edit the sidebar and then edit the page. To modify any actual section, just do it directly. Try to follow the same language and style used in the other articles of the Wiki.

For learning about the text formatting, check the [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

# Coding new stuff or fixing bugs

The easiest way to get a bug fixed or a new feature is to code it yourself. I know what are you thinking: "I am not an expert, I do not know C++, I am not capable, etc", but nobody really is until they do. 

So, setup the environment and compile the code as instructed below. Modify something dumb: the title bar of an app, some button, ... compile again and test. Try to understand how things works; this is exactly how everyone gets involved. 

## Environment setup

### Fork the repository
1. Download and install [Github desktop](https://desktop.github.com/)
2. Log to Github, open the [repository](https://github.com/eried/portapack-mayhem) and click **Fork** on the top right
3. In your Fork, Click **Clone** and **Open in Desktop**
4. Follow the rest of instructions in Github desktop

### Prepare for compilation
1. Install [Docker Desktop](https://www.docker.com/products/docker-desktop)
2. Install [Kitematic](https://github.com/docker/kitematic/releases)
3. In Kitematic, search for PortaPack and Create an instance
4. Inside of the PortaPack instance, set up the volume to point to the root of your local copy of the fork

For more details, check https://github.com/eried/portapack-mayhem/wiki/Compile-firmware

5. In the local copy of the fork, create an empty `Build` folder (in root path)
6. Run the image from Kitematic, the first time _it might_ take a long time to finish. The result will be left on that `Build` folder

### Work on the code
1. Install [Visual Studio Code](https://code.visualstudio.com/download)
2. Open the root directory of your local copy of the Fork
3. Change something and Run the image from Kitematic to compile