# ZX-SDC
Hardware version of z-controller (SD Card)

My motivation on creation this design was to avoid usage of CPLD and show that it's possible to design such controller with ICs.

This controller is intended to connect your ZX Spectrum / Clone with SD Card. That gives ability to copy files between SD Card with FAT16/32 to TRDOS (Beta Drive Interface), Nemo IDE and etc.

As an example, you can use FATALL file manager that runs from TRD.

## Technical information

This controller is almost fully compatible with original z-controller. There are couple of differences:
 - SD Card is always connected to power supply, besides it has power led connected to trigger to show state;
 - When /CS=1, means SD Card not selected, sending byte to data port is overwritten with 0xFF. It's a fix, because some SD Cards continue receiving input even after /CS becomes 1;

Control Port: 0x77
 - Bit 0: SD Card power On=1, Off=0;
 - Bit 1: SD Card /CS selected=0, deselected=1;
 - Rest bits are undefined;
   
Data Port: 0x57
 - Bit 0..7: Data byte to read/write; 

## Connection to ZX Spectrum Clones

Because current board design was done for ZXBUS, if you want to connect to your ZX Spectrum clone then you will need to solder adapter based on documentation for your computer.
Carefully check all signals, they are all important! As an example: /WAIT.

## Schematic preview
![Schematic, Rev 0.3](/zx-sdc-sch-rev0.3.png)

## Board preview
![Board, Rev 0.3](/zx-sdc-3d-rev0.3.png)

