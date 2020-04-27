Version 1.0 First 5 prototypes. (TEC1EV18.PCB)
J14 mislabeled as disable? Should be enable? NEEDS to be jumpered to work.




Version 1.1 fixes (TEC1EV19.PCB)
BC457 corrected to BC547
+5V and 0V logic probe pads corrected to 35mil
0V logic probe pads moved further away from 5V pads
Via through + on keyboard moved
Via through AD on keyboard moved
Vias through RESET on keyboard moved
Via through SHIFT on keyboard moved
Via through ALT on keyboard moved
Rotated EXPANSION word on solderside
Page0DEC error NOT fixed.








Switches on the TEC-1E

RAM PROTECT
SW5
This disable the write line from the RAM occupying addresss 2000 to 3FFF

The following switches are accessed by reading inport 01. Default behavior under software control is explained below. As their actions are processed via software, it is possible that their settings may not be reflected by what the computer is doing.

ROM SELECT
MS bit SW6 (Bit 4. LOW = OFF/left)
LS bit  SW7 (Bit 3. LOW = OFF/left)
Two switches are used to select one of four monitor programs from ROM1 and place it at address 0000
00 = MON3 (proposed new monitor. 2k at 0000 contains boot code. Main monitor occupies 8k at C000
01 = MON1 (original TEC-1 monitor, 1B version, with modified stack)
10 = MON2 (second TEC-1 monitor, with modified stack)
11 = JMON (third TEC-1 monitor, partial implementation with no single step due to different hardware.)

LOWRAM
SW8 (Bit 5. LOW = OFF/left)
This switch disables the lowest 2k of ROM, replacing it with RAM. Specifically, the block from 1000-17FF is moved to 0000-0FFF and a hidden block of 2k is switched into 1000-17FF. If LOWRAM is off, this spare block of memory is not part of the memory map.
The switching is done this way, so that replacement boot code can be programmed into the block while it is located at 1000 before it is switched to 0000. This allows the testing of new boot code or operation as a system with RAM located at 0000 through to 1FFF.
Again, the switch does NOT directly act on the memory. Rather, it instructs the monitor code do to the swap. There is nothing to stop a piece of software from activating and deactivating the mode as required, to access the hidden block of 2k.

CLOCK
SW9 (Bit 2. LOW = OFF/left)
SW10 (Bit 1. LOW = OFF/left)
SW11 (Bit 0. LOW = OFF/left)
These three switches select the clock speed at which the TEC-1E will run. As each monitor was written for a different clock rate, these switches allow an appropriate speed to be selected.
Recommended operating frequency depends on the maximum speed of the processor chosen. Maximum recommended frequency is 8.00MHz.
000 selects the direct output of the crystal oscillator.
001 Xtal output divided by 2
010 Xtal output divided by 4
011 Xtal output divided by 8
100 Xtal output divided by 16
101 Xtal output divided by 32
110 Xtal output divided by 64
111 selects a VCO for use with MON1/MON2 software.

IO MAPPING
OUTDEC1
Active LOW
OP00 CONTREG Control Register
OP01 CATLATCH Cathode latch, LED display
OP02 SEGLATCH Segment latch, LED display
OP03 PAGEREG Memory page register (selects lower 48k pages)
OP04 LCD
OP05 J4 (IO) pin 4
OP06 J4 (IO) pin 5
OP07 O7 (free pin)

INDEC1
Active LOW
IP00 Keyboard
IP01
IP02 J4 (IO) pin 1
IP03
IP04 LCD
IP05 J4 (IO) pin 2
IP06 J4 (IO) pin 3
IP07 I7 (free pin)

Combined input/output user strobe line. If this is used, I7 and O7 must not be used, as this would result in conflict.
Active LOW
IO7 (free pin)








Memory pages correspond
to a socket on the expansion
board. Each board can contain
RAM, ROM, or neither.
The ROM would sit at 0000
and contain code/drivers needed
to drive the expansion board.
This way, 3rd party boards
could be "plug and play".

Plans are for 7 expansion sockets,
giving a total of 8 pages including
that on the base TEC-1E board.



