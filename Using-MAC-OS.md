> This guide is a temporal entry.

1. Navigate into **github.com** (Create account if not have already) get your own fork of **eried/portapack-mayhem**

1. Download and install Github Desktop  **https://desktop.github.com**

1. Next, start github desktop, get into your account and clone forked eried/portapack-mayhem into local folder (i.e. **/Users/enrique/Documents/GitHub/portapack-mayhem**)

1. Download and install Docker Desktop for Mac **https://hub.docker.com/editions/community/docker-ce-desktop-mac/**

1. Start docker dashboard (from docker icon on top right in MAC desktop)

1. Log into docker hub  (or first **Create an account on hub.docker.com**) 

1. Open a shell window and on your command line and get into the folder where the cloned github is... (i.e. `cd /Users/enrique/Documents/GitHub/portapack-mayhem` )

1. execute: `docker pull eried/portapack`
1. Create a build folder `mkdir build`

## And now for the nice steps:

### TO BUILD
(still on command line): `docker build -t portapackccache -f dockerfile-nogit .`

(took in my machine about 2 minutes, i7 2.6mhz quad, with tons of verbose about the building process. Finally: )

`Step 13/13 : CMD cd .. && cd build &&     cmake .. && make firmware`
 `---> Running in d68ff9843634`
`Removing intermediate container d68ff9843634`
 `---> f6387073737a`
`Successfully built f6387073737a`
`Successfully tagged portapackccache:latest`

### TO COMPILE

Also check: https://github.com/sharebrained/portapack-hackrf/issues/160#issuecomment-640237943

`docker run -it -v ${PWD}:/havoc portapackccache`

In my case it took about 25 minutes. At the end, after even more tons of verbosities and warnings you should get something like this:

`Scanning dependencies of target hackrf_usb_dfu.elf`
`[100%] Linking C executable hackrf_usb_dfu.elf`
`[100%] Built target hackrf_usb_dfu.elf`
`Scanning dependencies of target hackrf_usb_dfu.bin`
`[100%] Built target hackrf_usb_dfu.bin`
`Scanning dependencies of target hackrf_usb.dfu`
`dfu-suffix (dfu-util) 0.8`

`Copyright 2011-2012 Stefan Schmidt, 2013-2014 Tormod Volden`
`This program is Free Software and has ABSOLUTELY NO WARRANTY`
`Please report bugs to dfu-util@lists.gnumonks.org`

`Suffix successfully added to file`
`[100%] Built target hackrf_usb.dfu`
`Scanning dependencies of target firmware`
`[100%] Generating portapack-h1_h2-mayhem.bin`
`[100%] Built target firmware`