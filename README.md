```
  _____             __   _____             
 / ____|  /\       /_ | |  __ \            
| (___   /  \ ______| | | |  | | ___   ___ 
 \___ \ / /\ \______| | | |  | |/ _ \ / __|
 ____) / ____ \     | | | |__| | (_) | (__ 
|_____/_/    \_\    |_| |_____/ \___/ \___|
     Version 0.10        by Vitor Vilela
```

*This is a work in progress document.*

Date: 2019-04-15 (April 15, 2019)

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
