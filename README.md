# Room controller

Initially planned for controlling a radiator, this mutated into a generic
room controller schematic, featuring

* ATmega 168 controller
* two 1wire slave interfaces
* one I²C interface
* two 24V outputs
  * low-side switched
  * diode protected
  * PWM capable
* four binary I/O wires
  * with ADC, if required
* on-board programming interface
  * 6-pin version, accessible with pogo-pin adapter
* optional XTAL for 20 MHz operation
* WAGO connectors for the bus wires

The board fits standard round wall outlets. Its height is nominally 13mm
(determined by the WAGO 243 connectors).

## Who needs two 1wire interfaces?

The idea is that one is used for "slow" operations (parasitic-powered
thermometers, firmware updates (yes, I plan to do that)), while the other
bus does the "fast" stuff (run a CONDITIONAL SEARCH ten times a second).

## No 1wire master? Why?

Timing. You cannot run a 1wire master and slave at the same time.
Not reliably in software on one MCU, anyway.

If you want a master, you have I²C, connect an I²C-to-1wire interface.
(No, I didn't reserve space on the board for this.)

## Why 5V instead of 3.3V?

That would require me to run 1wire on 3.3V. It's possible, but you have
much less noise resistance. Also, the ATmega168 won't do 20 MHz on 3.3V.

That being said, running just the I²C on 3.3V isn't too difficult,
I'll add that if and when somebody actually needs it.

## How about software support?

The board will be fully supported by OWFS and the library at
https://github.com/M-o-a-T/owslave .

