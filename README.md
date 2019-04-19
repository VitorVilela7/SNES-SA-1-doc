```
  _____             __   _____             
 / ____|  /\       /_ | |  __ \            
| (___   /  \ ______| | | |  | | ___   ___ 
 \___ \ / /\ \______| | | |  | |/ _ \ / __|
 ____) / ____ \     | | | |__| | (_) | (__ 
|_____/_/    \_\    |_| |_____/ \___/ \___|
     Version 0.11        by Vitor Vilela
```

*This is a work in progress document.*

Date: 2019-04-19 (April 19, 2019)

Presentation
============

This document is a result from many years researchment and testing. I'm continously updating this document with more information and experiments. The information here is accurate but may be subject to revision.

There is not much information available on how the SA-1 chip works, other than the official Nintendo docs which does not very explain much the chip in details but rather focuses on the functionalities and features available. Therefore there is not much information available over undefined behavior or design details. This document attempts in covering it.

If you find any potential issue and/or have any question about this document, feel free to contact me or contribute though GitHub at https://github.com/VitorVilela7/SNES-SA-1-doc/

Memory Map
==========

## S-CPU Side

Banks $00-$3F; $80-$BF
* $2200-$23FF : with exception of $2300, all open bus when reading. $2200-$22FF are write-only registers.
* $3000-$37FF : I-RAM
* $6000-$7FFF : BW-RAM Mirror
* $8000-$FFFF : ROM ($00-$1F: CXB, $20-$3F: DXB, $80-$9F: EXB, $A0-$BF: FXB)

Banks $40-$4F : BW-RAM
* The SA-1 chip has enough pins for mapping 256 KB (256 * 1024 bytes) of BW-RAM. The rest is mirror.

Banks $C0-$CF : ROM (CXB)

Banks $D0-$DF : ROM (DXB)

Banks $E0-$EF : ROM (EXB)

Banks $F0-$FF : ROM (FXB)

## SA-1 Side

Banks $00-$3F; $80-$BF
* $2200-$23FF : with exception of $2300, all open bus when reading. $2200-$22FF are write-only registers.
* $3000-$37FF : I-RAM
* $6000-$7FFF : BW-RAM Mirror
* $8000-$FFFF : ROM ($00-$1F: CXB, $20-$3F: DXB, $80-$9F: EXB, $A0-$BF: FXB)

Banks $40-$5F : BW-RAM
* The SA-1 chip has enough pins for mapping 256 KB (256 * 1024 bytes) of BW-RAM. The rest is mirror.

Banks $60-$7F : BW-RAM Virtual Memory
* Allows for packing and unpacking BW-RAM by two or four bits (register $223F)
* Allows mapping up to 1 MB (4 bit mode) or 512 KB (2 bit mode)

Banks $C0-$CF : ROM (CXB)

Banks $D0-$DF : ROM (DXB)

Banks $E0-$EF : ROM (EXB)

Banks $F0-$FF : ROM (FXB)

ROM
===

* Data bus: 16-bit
* Max size: 64 Mbit (8 MB)
* Base speed: 5.37 MHz

I-RAM
=====
Bultin SA-1 RAM chip.

* Data bus: unknown, probably 8-bit.
* Max size: 16 kbit (2 kB)
* Base speed: 10.74 MHz

BW-RAM
======
Static memory.

* Data bus: 8-bit
* Max size: 2 Mbit (256 KB)
* Base speed: 5.37 MHz
