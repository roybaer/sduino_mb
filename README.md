# sduino MB

The __sduino MB__ is an attempt at creating a mechanically and electrically Arduino-MEGA-compatible development board based on the __STM8S208MB__ microcontroller.
Both, mechanical and electrical design are to a notable degree based on the [Arduino MEGA board](https://store.arduino.cc/arduino-mega-2560-rev3).

## Pin mapping

See [pin mapping documentation](docs/pinmapping.md) for details.

## Differences

The following paragraphs highlight the most important differences between Arduino MEGA and sduino MB.

### Electrical

Most importantly, the sduino MB can be switched between 5V and 3.3V operating voltage.
The RX and TX LEDs are connected to the RX and TX lines (IO pin 0 and 1, respectively) via 1k resistors, rather than to the USB interface chip.

### Mechanical

The gap between the upper socket strips has been reduced from 0.06 to 0.05 inches.
This should not significantly impact mechanical compatibility with Arduino shields and increases the available radius around the center of the upper left M3 mounting hole from 2.286 to 2.54 millimeters, which should be just enough to fit in a standard M3 spacer (5mm wrench).
The voltage jumper might get in the way of cases built for the Arduino MEGA.
Drilling a matching 10 mm hole in their top cover should make them compatible.

### Functional

The STM8S208MBT6B only has 128 KiB of Flash, 6 KiB of RAM and 2 KiB of EEPROM, has four IO pins less than would be desirable, two instead of four UARTs, no analog comparator and no external memory interface.
In exchange, it has positive _and negative_ reference voltages for its ADC, a CAN interface, switchable I²C lines and can run at up to 24 MHz.
It can also run code from all its addressable memory, i.e. FLASH, RAM and EEPROM and should therefore be able to load and run code from an SD card.

Like many Arduino MEGA clones, the sduino MB uses a CH340G USB to serial converter instead of an Atmega16U2 for communication with the host PC.
The USB interface Chip therefore cannot be repurposed as a coprocessor or keyboard/mouse simulator.

### Software

Unfortunately, there is no free C++ compiler available for the STM8 platform, yet.
The Arduino language along with the large pool of existing Arduino sketches can therefore not be used without modifications.

Fortunately, there is the C-based [sduino library](https://github.com/tenbaht/sduino) that this board borrows its name from.
By using the sduino library, the changes required to run many exsting Arduino sketches on an STM8 platform can be kept within manageable bounds.

Furthermore, there are ongoing efforts to create an Arduino port for the STM8 based on an improved version of the [LLVM+SDCC toolchain](http://www.colecovision.eu/llvm+sdcc/) that uses C as intermediate language.

## Copying

Even though the sduino MB CAD files have been created from scratch and the design is not identical, to avoid legal ambiguity, the CAD files for the sduino MB board are released under the same creative commons license as those of the Arduino MEGA board:

This work is licensed under the Creative Commons Attribution-ShareAlike 2.5 Generic License. To view a copy of this license, visit http://creativecommons.org/licenses/by-sa/2.5/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.
