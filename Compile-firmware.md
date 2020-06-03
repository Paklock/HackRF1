The easiest way is to use Docker. After you install Docker in your machine, if you are inclined for using the command line, you can try the following:

* For building:
`docker build -t portapackccache -f dockerfile-nogit .`

* For running (in the root of the repo):
`docker run -it -v ${PWD}:/havoc portapackccache`

You have to create a `build` folder before running the image.

# Using Docker Hub and Kitematic
The required Docker image is also in Docker Hub, browse for it in [Kitematic](https://github.com/docker/kitematic):

[[img/Kitematic_MChWCyp6g1.png]]

You need to configure the path to the source code from the Volumes of the container as show in the image below. Everytime you run this container, it will compile the source and (if successful) leave the results in `build/firmware/`

[[img/Kitematic_VL5an8rufV.png]]

In Windows, the line endings may produce some errors. If you get some `python/r` not found messages, then the easiest way to fix this is to configure git to not manipulate the line endings with:

`git config --global core.autocrlf false`

And subsequently, download another copy of the repository. 

# Using Buddy.Works (and other CI platforms)

You can use the following _yml _as your template for your CI platform (pipeline export from [buddy.works](https://buddy.works/)):

```
- pipeline: "Build firmware"`
  `trigger_mode: "ON_EVERY_PUSH"`
  `ref_name: "master"`
  `ref_type: "BRANCH"`
  `auto_clear_cache: true`
  `trigger_condition: "ALWAYS"`
  `actions:`
  `- action: "Build Docker image"`
    `type: "DOCKERFILE"`
    `dockerfile_path: "dockerfile-nogit"`
    `do_not_prune_images: true`
    `trigger_condition: "ALWAYS"`
  `- action: "Execute: mkdir build"`
    `type: "BUILD"`
    `working_directory: "/buddy/portapack-havoc"`
    `docker_image_name: "library/ubuntu"`
    `docker_image_tag: "18.04"`
    `execute_commands:`
    `- "mkdir -p build"`
    `volume_mappings:`
    `- "/:/buddy/portapack-havoc"`
    `trigger_condition: "ALWAYS"`
    `shell: "BASH"`
  `- action: "Run Docker Image"`
    `type: "RUN_DOCKER_CONTAINER"`
    `use_image_from_action: true`
    `volume_mappings:`
    `- "/:/havoc"`
    `trigger_condition: "ALWAYS"`
    `shell: "SH"
```