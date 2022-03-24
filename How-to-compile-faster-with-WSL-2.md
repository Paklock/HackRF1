_**Note: This is for Windows only**_

The steps on the [Compile-firmware](https://github.com/eried/portapack-mayhem/wiki/Compile-firmware#step-3-prepare-the-docker-container) page work fine for compiling, but you may find it takes around 35 minutes each time.
In this guide I will show you how to get that time down to 2 seconds - 1 minute depending on your hardware.



**Step 1)** Download Ubuntu from the windows store
![image](https://user-images.githubusercontent.com/4393979/159869511-93a97a3c-ca7b-46a7-b3f9-447561b1ebc9.png)

**Step 2)** once its opened open up a windows terminal and run ```wsl -l -v```
![image](https://user-images.githubusercontent.com/4393979/159869583-e649c494-c1e0-4e34-a5b1-c428cb4db763.png)

check it says version 2

If it does not, then run: ```wsl --set-default-version 2``` followed by running ```wsl --set-version Ubuntu 2```

**Step 3)** Once that is done, open the Ubuntu app again (make sure you have set it up so you get to the console in it)

**Step 4)** Go to docker on windows and go to settings -> resources -> WSL Integration

**Step 5)** Toggle Ubuntu on (if its not there, click refresh)

**Step 6)** Open up your windows file explorer ang in the address bar go to ``\\wsl$\``

**Step 7)** navigate to Ubuntu/home/{username}/

**Step 8)** copy your portapack-mayhem folder into your dir above

**Step 9)** Confirm your Ubuntu WSL instance can see it by going  ```cd ~/portapack-mayhem```

**Step 10)** If its there then you are good to go. Time to run docker ```docker run -it -v ~/portapack-mayhem:/havoc portapack-dev```

**Step 11)** Profit! It should be compiling super fast now!

You can then set a network share up to your ```\\wsl$\Ubuntu\home\{username}\portapack-mayhem``` folder and continue to edit the files from within windows.

_(This guide is a WIP, so I may have missed some steps that I will need to add. Let me know jLynx#7987)_