These are miscellaneous useful notes about how ChibiOS functions.

### Stacks Configuration

From ChibiOS crt0.c:

Two stacks available for Cortex-M, main stack or process stack.

* **Thread mode**: Used to execute application software. The processor enters Thread mode when it comes out of reset.
* **Handler mode**: Used to handle exceptions. The processor returns to Thread mode when it has finished all exception processing.

ChibiOS configures the Cortex-M in dual-stack mode. (CONTROL[1]=1)
When CONTROL[1]=1, PSP is used when the processor is in Thread mode.

MSP is always used when the processor is in Handler mode.

* **__main_stack_size__**: Used for exception handlers. Yes, really.
* **__process_stack_size__**: Used by main().

After chSysInit(), the current instructions stream (usually main())
becomes the main thread.


##
Original Wiki by sharebrained at [Operating System Notes](https://github.com/sharebrained/portapack-hackrf/wiki/Operating-System-Notes)