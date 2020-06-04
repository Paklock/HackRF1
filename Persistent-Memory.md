This is part of the **RTC (Real Time Clock) subsystem**, inside the LPC43xx chip on the Portapack hardware.

# RTC Subsystem

The RTC subsystem keeps the actual clock (date / time) running, powered by a CR2032 battery, (which needs to be installed on the portapack board!), even when the unit is not connected to an USB power source. 

The persistent memory map is defined at `/firmware/chibios-portapack/os/hal/platforms/LPC43xx/lpc43xx.inc`:

```
 **LPC_RTC_DOMAIN_BASE**       (0x40040000)
 **LPC_ALARM_TIMER_BASE**      (LPC_RTC_DOMAIN_BASE + 0x0000)
 **LPC_BACKUP_REG_BASE**       (LPC_RTC_DOMAIN_BASE + 0x1000)  <- backup_ram region!
 **LPC_POWER_MODE_CTRL_BASE**  (LPC_RTC_DOMAIN_BASE + 0x2000)
 **LPC_CREG_BASE**             (LPC_RTC_DOMAIN_BASE + 0x3000)
 **LPC_EVENT_ROUTER_BASE**     (LPC_RTC_DOMAIN_BASE + 0x4000)
 **LPC_OTP_CTRL_BASE**         (LPC_RTC_DOMAIN_BASE + 0x5000)
 **LPC_RTC_BASE**              (LPC_RTC_DOMAIN_BASE + 0x6000)
```

## backup_ram region

The **backup_ram region** is a small amount of ram (only 256 bytes), defined in `/firmware/common/memory_map.hpp` and labeled as **LPC_BACKUP_REG_BASE** starting at address **0x40041000**
### data_t struct

The Portapack firmware uses the backup_ram region to store several uint32_t (and one uint64_t) variables, inside a struct, called "data_t", declared on /firmware/common/portapack_persistent_memory.cpp

### Variables stored in persistent memory

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

### Using this two new booleans

They can be reached from anywhere by adding (if not already there) this include:

`#include "portapack_persistent_memory.hpp"`

and then you can check the configuration status for each parameter with:

`portapack::persistent_memory::config_backbutton()`

and

`portapack::persistent_memory::config_speaker()`

They return either TRUE or FALSE, depending on how they've been configured.