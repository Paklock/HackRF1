The boot process is a bit of madness, but justifiable madness.

### Overview

The LPC4320 bootloader initializes the Cortex-M4F core to boot from the start of external SPI flash. The M0 core stays in reset. The [bootstrap code](https://github.com/sharebrained/portapack-hackrf/blob/master/firmware/bootstrap/bootstrap.c) runs from SPI flash, on the Cortex-M4F. The bootstrap initializes the Cortex-M0 to execute the application code from SPI flash, then sleeps. The application code copies the baseband code into RAM, configures the Cortex-M4F to run from RAM, then resets the Cortex-M4F to begin baseband execution.

(TODO: A diagram would be helpful, showing the M4F and M0 activities vs. time.)

### Bootstrap

In the PortaPack image, the Cortex-M4F "bootstrap" image is located at the start of SPI flash. It's executed by the LPC4320 built-in bootloader. The M4 clock is already set to 96MHz. The bootstrap code configures SPIFI to run at (approximately) maximum speed. Then, it initializes the Cortex-M0's memory map to point at the "application" image in SPI flash, and releases the Cortex-M0 from reset. The bootstrap then sleeps the Cortex-M4 until the M0 application needs to run baseband firmware on it.

### Application

On the Cortex-M0 core, boot time looks like this:

    ResetHandler:
        Initialize process stack pointer
        Initialize stack RAM regions (fill with pattern)
        __early_init()
            Enable extra processor exceptions for debugging
        Init data segment (copy SPI flash -> data region in RAM)
        Initialize BSS (fill RAM region with 0)
        __late_init()
            reset()
                Reset most peripherals -- not SCU, SPIFI, or M0APP
            halInit()
                hal_lld_init()
                    Init timer 3 as cycle counter (no DWT on M0)
                    Init RIT as SysTick (no SysTick on M0)
                palInit()
                gptInit()
                i2cInit()
                sdcInit()
                spiInit()
                rtcInit()
                boardInit()
            chSysInit()
                port_init()
                _scheduler_init()
                _vt_init()
                _core_init()
                _heap_init()
                chSysEnable()
                chThdCreateStatic(_idle_thread_wa, ...)
        Constructors
        main()
        Destructors
        _default_exit()
            while(1);

### Baseband

On the Cortex-M4F core, these are the stages a baseband image moves through:

    ResetHandler:
        Initialize process stack pointer
        Initialize FPU
        Initialize stack RAM regions (fill with pattern)
        __early_init()
            Enable extra processor exceptions for debugging
        Init data segment (copy SPI flash -> data region in RAM)
        Initialize BSS (fill RAM region with 0)
        __late_init()
            halInit()
                hal_lld_init()
                    Init SysTick
                    Init DWT as cycle counter
                # Baseband controls no hardware, so no hardware init here.
                boardInit()
            chSysInit()
                port_init()
                _scheduler_init()
                _vt_init()
                _core_init()
                _heap_init()
                chSysEnable()
                chThdCreateStatic(_idle_thread_wa, ...)
        Constructors
        main()
        Destructors
        _default_exit()
            while(1);

##
Original Wiki by sharebrained at [Boot Process](https://github.com/sharebrained/portapack-hackrf/wiki/Boot-Process)