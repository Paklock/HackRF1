# Persistent config data

All configuration parameters can be found at `/firmware/common/portapack_persistent_memory.cpp`

Configuration parameters are stored as uint32_t and int64_t variables inside **data_t Struct**.

## data_t struct

The data_t struct persists inside a **backup_ram region** defined in `/firmware/common/memory_map.hpp`

Found in original portapack, but only carrying a few configuration variables, it was expanded by furrtek HAVOC's version, incorporating several new configuration parameters, and even further expanded now for (a branch for...) MAYHEM version; including config parameters for "Speaker is present" and "Back Buttons on menues" configuration checkboxes.

In particular, and as an example, the `uint32_t ui_config` variable was created in HAVOC's version for boolean storage options, but now also includes some new options added recently for mayhem firmware:

### ui_config Bit position / Description
* 31 (HAVOC)Splash screen
* 30 (HAVOC)Login
* 29 (HAVOC)Start in stealth mode
* 28 (MAYHEM)Place a back ("..") button in each menu
* 27 (MAYHEM)Use speaker output (H1 model accepts a speaker)