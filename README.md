# Nu2031 

This adapter allows one to utilize a Commodore 1541 disk drive as both a serial disk drive for the serial IEC-based Commodore computers (VIC-20, C64, +4, C16, C128, etc.) and also an IEEE-488 drive for the PET/CBM line of computer systems.

## Introduction

Nu2031 ("New" 2031, with new in quotes because it's not really new :-)) comprises a two part hardware modification for the Commodore 1541 disk drive.  The first part is a 6522 Versatile Interface Adapter (VIA) daughterboard that dynamically switches specific VIA signals between the existing 1541 serial IEC port and an on-board IEEE-488 interface. The second part is a special multi-bank ROM-el replacement ROM that contains both the original 1541 DOS and a patched DOS that will enable the 1541 drive to function as a IEEE-488 CBM 2031 workalike drive. Using a single switch, connected to both adapter boards, the system can be quickly switched from one interface to the other.

This design is a refinement of many previous conversion projects, listed below:

The original (and largest, in my opinion) effort was included in an old 64'er magazine article.  Andre Fachat, who built the original interface, re-created the schematic and re-typed in the DOS patching utility, which are available at  http://www.6502.org/users/andre/cbmhw/ieee488/index.html. 

Dirk Wouters improved on the design by allowing the conversion to be "switched off", allowing continued use of the 1541 as a 1541 drive while supporting the IEEE-488 functionality.  Though his plans are no longer available, the project is discussed at https://www.lemon64.com/forum/viewtopic.php?t=71124 and at https://www.forum64.de/index.php?thread/91569-1541-to-ieee488-trimod-adapter/ (German).

Nu2031 was started before Dirk's project was presented, so it does not borrow from that design, though the two projects share a common set of functionality.

## Technical Details

The heart of the unit is the main adapter PCB (the ROM board is just a simple multi-bank ROM). The PCB contains both the 75160 and 75161 IEEE-488 interface ICs, as well as a Xilinx XC9572XL Complex Programmable Logic Device (CPLD).  Unlike the initial 64'er/Andre Fachat project, which simply wired the VIC to the interface ICs, or Dirk Wouter's interface, which uses banks of quad bilateral CMOS 4066 bilateral switches to connect or disconnect the various VIA signals to the 1541 motherboard or the IEEE 488 bus transceivers, this design implements the various IEEE-488 signal directions, as noted on page 2 of the 75161B datasheet (https://www.ti.com/lit/gpn/sn75161b). For reference, DC is always 'H' (5V), so the truth table can be somewhat simplified. The  ROM select signal noth only chooses which ROM bank to use, but is also used by the design to select which interface to enable.  The deselected interface is configured to allow other devices to continue to function on the de-selected bus.

If the system sees the ROM select signal change state, the interface immediately reconfigures the interface connects and resets the drive so the correct ROM will be initialized.

## Future Directions:

- Support method to "softswitch" the interface from one bus to another.

## License
Copyright (C) 2019-20  RETRO Innovations

These files are free designs; you can redistribute them and/or modify
them under the terms of the Creative Commons Attribution-ShareAlike 
4.0 International License.

You should have received a copy of the license along with this
work. If not, see <http://creativecommons.org/licenses/by-sa/4.0/>.

These files are distributed in the hope that they will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
license for more details.


