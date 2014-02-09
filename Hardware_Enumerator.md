HARDWARE ENUMERATOR
==========================
Version 0.3a (WIP) 

Embed device in the motherboard that negotiates with expansion devices what address blocks they will use and allow to user software know what hardware is attached and what address blocks are using

Resources Used
--------------

- Address 0x110000-0x110003 (**CMD** register). To write a 16 bit value / read a 32 bit value in *Little Endian*. 
- Address 0x110004-0x110007 (**BUILDID** register). To read a 32 bit value in *Little Endian*. Returns a
	unique ID of the motherboard. 

Commands
--------
Write a value at **CMD** register to:


    | VALUE |    NAME     | BEHAVIOUR                                                |  
    |-------+-------------+----------------------------------------------------------|
    |0x0000 | GET-NUMBER  | Reading CMD, returns the number of devices attached from |
    |       |             | 0 to 32.                                                 |
    |-------+-------------+----------------------------------------------------------|
    |0x01xx | GET-CLASS   | Reading CMD, returns the Hardware class of the device xx |
    |       |             | attached. Value 0 is xx correspond to a not attached     |
    |       |             | device.                                                  |
    |-------+-------------+----------------------------------------------------------|
    |0x02xx | GET-BUILDER | Reading CMD, returns the Hardware Builder of the device  |
    |       |             | xx attached.                                             |
    |-------+-------------+----------------------------------------------------------|
    |0x03xx | GET-ID      | Reading CMD, returns the Hardware ID of the device xx    |
    |       |             | attached. Value 0 is xx correspond to a not attached     |
    |       |             | device.                                                  |
    |-------+-------------+----------------------------------------------------------|
    |0x04xx | GET-VERSION | Reading CMD, returns the Hardware Version of the device  |
    |       |             | xx attached.                                             |
    |-------+-------------+----------------------------------------------------------|
    |0x05xx | GET-BLQ     | Reading CMD, returns the begin of the address block used |
    |       |             | by the device xx.                                        |
    |-------+-------------+----------------------------------------------------------|
    |0x06xx | GET-BLQS    | Reading CMD, returns the size of the address block used  |
    |       |             | by the device xx.                                        |
    |-------+-------------+----------------------------------------------------------|
    |0x07xx | GET-NINT    | Reading CMD, returns the number of interrupt message     |
    |       |             | used by the device xx. Valid values from 0 to 4          |
    |-------+-------------+----------------------------------------------------------|
    |0x1yxx | GET-INTMSG  | Reading CMD, returns the interrupt message y used by the |
    |       |             | device xx. The return order is the same that are listed  |
    |       |             | in device specs.                                         |
    |-------+-------------+----------------------------------------------------------|
        
           
The quadruple of {Class, Builder, ID, Version}, identify a **single specific hardware device**. A device with the same {Class, ID} but different Version, is expect to share some kind of compatibility. 
 
Class is a 8 bit value, Builder and ID are 32 bit value, Version are 16 bit values.

Device Class values
-------------------

- 0x01 : Audio devices (Sound Cards)
- 0x02 : Communications devices
- 0x03 : HID (Human Interface Device)
- 0x06 : Image/Video Input Devices
- 0x07 : Printer (2D and 3D) Devices
- 0x08 : Mass Storage Device (Floppy drives, Microdrives, Hard disks, Tape recorders)
- 0x0E : Graphics Devices (Graphics card)
- 0x0F : HoloGraphics Devices
- 0x10 : Ship Sensors (DRADIS, Air, Hull integrity, etc...)
- 0x11 : Power Management Systems (control of Generators)
- 0x12 : Hydraulic/Pneumatic Actuators (control of doors, air-locks, landing gears)
- 0x13 : Electric Engines (control of wheels and steering)
- 0x1A : Defensive Systems (control of shields)
- 0x1B : Offensive Systems (control of weapons)
- 0x1C : Sub-FTL Navigational and Engine Systems (control of thrusters and engines)
- 0x1D : FTL Navigational Systems (control of warp engines)
- 0xFF : Multifunction devices.

Know Builder values
-------------------

- 0x00000000 -> Unknown builder
- 0x1C6C8B36 -> Nya Elektriska
- 0x1EB37E91 -> Mackapar Media
- 0x21544948 -> Harold Innovation Technologies (Harold I.T.)
- 0x0CA0FE84 -> Investronics
- 0x75FB5FCC -> Admiral Systems


