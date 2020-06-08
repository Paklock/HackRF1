# HackRF
The **original HackRF** code can be found at `/hackrf`, it is a subproject inside the source code. It points to https://github.com/mossmann/hackrf

# Portapack
The rest of the code, including the **portapack** and **havoc/mayhem** extras can be found at `/firmware`

The portapack <--> HackRF interface functions are located in `/firmware/baseband`

There is an underlying OS framework, the **CHIBIOS/RT**, which is located at `/firmware/chibios` for the abstract functionality, and `/firmware/chibios-portapack` for the specific portapack board hardware drivers and configurations.

## Application folder

The portapack application software, can be found at `/firmware/application`

User interface: `/firmware/application/ui`

Apps (options in each menu): `/firmware/application/apps`

IC / hardware components interface: `/firmware/application/hw`

Common protocols functionality: `/firmware/application/protocols`

# User Interface

## Menus and Widgets

**MOST menus** (excluding OPTIONS and DEBUG, which are actually apps) and **pop-up boxes** (yes/no, yes/cancel, ok) are defined in `/firmware/application/ui_navigation.cpp`

The **Options menu** is actually an "app" defined at `/firmware/application/apps/ui_settings.cpp`

The **Debug menu** (also an app) is defined at `/firmware/application/apps/ui_debug.cpp`

The widgets used in the UI, as **buttons, texts, checkboxes, input fields**, etc. are to be found at `/firmware/common/ui_widget.cpp`

