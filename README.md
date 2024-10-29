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

## Prototype
![Prototype board](/zx-sdc-prototype-board.JPG)

![FATALL running](/zx-sdc-prototype-work.JPG)

## Assembled and working board

![Assembled board](/zx-sdc-assembled-board-1.jpeg)

![Assembled board](/zx-sdc-assembled-board-2.jpeg)

![Assembled board](/zx-sdc-assembled-board-3.jpeg)

![FATALL running](/zx-sdc-working-board-1.jpeg)

![FATALL running](/zx-sdc-working-board-2.jpeg)

## Note on assembling board

U11 and J4 has been added to the board for debugging purpose. Since board has been tested and doesn't need to be tuned if assembled correct, you can skip soldering U11 or use socket for it.
J4: 1-2 SD Card, 2-3 U11 Test IC connection

In case you decided to make sure that board assembled right and works correct, follow this checklist:
 1. Switch off computer
 2. Connect controller to ZXBUS Edge
 3. Remove SD Card if it was inserted at any slots
 4. Put jumper on J4 to 2-3
 5. Switch on computer - there are no leds should be ON
 6. Run commands from Basic:
    + "PRINT IN 87", expected result: 0
    + "PRINT IN 87", expected result: 255
    + "OUT 119,1", both leds must switch ON
    + "OUT 87,85"
    + "PRINT IN 87", expected result: 85
 7. Switch off computer
 8. Put jumper on J4 to 1-2
 9. Insert SD Card at any slot
 10. Switch on computer
 11. Run FATALL from ROM or from BDI
 12. SD Card should be detected and content will be shown on right panel

NOTE: SD Card must be formatted in FAT32/16!!!

