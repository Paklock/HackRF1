# Persistent config data

All configuration parameters are stored as uint32_t and int64_t variables inside **data_t Struct** declared on `/firmware/common/portapack_persistent_memory.cpp`

## data_t struct

The data_t struct persists inside a **backup_ram region** defined in `/firmware/common/memory_map.hpp`

Found in **original portapack**, but only carrying a few configuration variables, it was later expanded by furrtek's **HAVOC** version, incorporating several new configuration parameters. 

Among those new variables, there is a `uint32_t config_t` used as storage for a few boolean flags.

On MAYHEM's version, we've added two new boolean configuration parameters, particularly useful for H1 users including "**Speaker is present**" and "**Back Buttons on menues**".

You can find them implemented as two new configuration checkboxes inside OPTIONS->UI.

These two new boolean parameters have been added into the `uint32_t ui_config` variable, Which now it is mapped as following:

### ui_config Bit position / Description
* 31 (HAVOC)Splash screen
* 30 (HAVOC)Login
* 29 (HAVOC)Start in stealth mode
* 28 (**MAYHEM H1 Branch**)Place a back ("..") button in each menu
* 27 (**MAYHEM H1 Branch**)Use speaker output (H1 model accepts a speaker)