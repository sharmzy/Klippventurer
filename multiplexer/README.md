Here's a diagram of the pinout of Adventurer 3's multiplexer chip. There aren't enough serial UART ports on the STM32 to communicate with all 4 motor drivers while also communicating with the host.
Thankfully, the board is equipped with a multiplexer that solves this problem in a simple and elegant fashion.
What this chip does is act like a gate, allowing only one driver to talk to the controller at a time.
When you go to home the machine or initialize motors, the controller tells the multiplexer which chip it would like to communicate with, and the multiplexer connects that chip to the serial port.
Once this driver chip is configured, it moves onto the next until all 4 are configured and the chips no longer need a serial link to the MCU (microcontroller unit)
I've attached a diagram of how this group of chips is wired as well as the datasheet of the multiplexer used.
There's not much documentation regarding how many variations of Adventurer 3 and Voxel boards there are, but to my knowledge some use TMC2208 stepper drivers, and some use the HK32 clone of the STM32, which functions and programs identically and will not effect any of this process.
I'm unaware of any using a different multiplexer, but this is possible too. If its muxing table is different than this one, you'll need to check its datasheet and change the "[tmc220x stepper_] sections of your printer.cfg file (Adventurer-3.cfg in the repo) where it says "select_pins:" to tell your multiplexer which driver you'd like to talk to.
Here's the datasheet for the Texas Instruments CD4051B multiplexer chip used in my Adventurer 3 Pro: https://www.ti.com/lit/ds/symlink/cd4051b.pdf?ts=1652595308320