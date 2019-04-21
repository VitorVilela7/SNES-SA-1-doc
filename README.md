```
  _____             __   _____             
 / ____|  /\       /_ | |  __ \            
| (___   /  \ ______| | | |  | | ___   ___ 
 \___ \ / /\ \______| | | |  | |/ _ \ / __|
 ____) / ____ \     | | | |__| | (_) | (__ 
|_____/_/    \_\    |_| |_____/ \___/ \___|
     Version 0.20        by Vitor Vilela
```

*This is a work in progress document.*

Date: 2019-04-21 (April 21, 2019)

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

Schematics and pin-outs
=======================

This is the schematic of the SA-1 cart, based on the SHVC-1L8B-10 board using a
customized EPROM board for custom programming. Most of the information here is not
complete, however verified with oscilloscope and with a custom ROM for making sure the
descriptions are correct.

I have tracked some of the capacitors and resistors as well, however since it is not the
main focus of the research nor I have the proper tools for testing them, they are not
complete nor accurate and are listed because they had something to do with some of the
main pins.

## SRAM
### CXK581000AM-70LL (SONY)
Orientation: "ball marking" (left->right)

| Pin number | Connection | Pin name   | Note                                                                                             |
|------------|------------|------------|--------------------------------------------------------------------------------------------------|
| --         | --         | --         | South side                                                                                       |
| 1          | CHIP.104   | SRAM.NC    | SRAM.A17 on CXK582000 @ 256 KB                                                                   |
| 2          | CHIP.86    | SRAM.A16   |                                                                                                  |
| 3          | CHIP.87    | SRAM.A14   |                                                                                                  |
| 4          | CHIP.88    | SRAM.A12   |                                                                                                  |
| 5          | CHIP.89    | SRAM.A7    |                                                                                                  |
| 6          | CHIP.90    | SRAM.A6    |                                                                                                  |
| 7          | CHIP.91    | SRAM.A5    |                                                                                                  |
| 8          | CHIP.92    | SRAM.A4    |                                                                                                  |
| 9          | CHIP.93    | SRAM.A3    |                                                                                                  |
| 10         | CHIP.94    | SRAM.A2    |                                                                                                  |
| 11         | CHIP.95    | SRAM.A1    |                                                                                                  |
| 12         | CHIP.96    | SRAM.A0    |                                                                                                  |
| 13         | CHIP.117   | SRAM.D0    |                                                                                                  |
| 14         | CHIP.116   | SRAM.D1    |                                                                                                  |
| 15         | CHIP.115   | SRAM.D2    |                                                                                                  |
| 16         | GND        | SRAM.GND   |                                                                                                  |
| --         | --         | --         | North side                                                                                       |
| 17         | CHIP.114   | SRAM.D3    |                                                                                                  |
| 18         | CHIP.113   | SRAM.D4    |                                                                                                  |
| 19         | CHIP.112   | SRAM.D5    |                                                                                                  |
| 20         | CHIP.111   | SRAM.D6    |                                                                                                  |
| 21         | CHIP.110   | SRAM.D7    |                                                                                                  |
| 22         | MM1026     | SRAM.CE1_N | MM1026 is a circuit responsible for protecting SRAM data and switching power source when needed. |
| 23         | CHIP.97    | SRAM.A10   |                                                                                                  |
| 24         | CHIP.108   | SRAM.OE_N  |                                                                                                  |
| 25         | CHIP.98    | SRAM.A11   |                                                                                                  |
| 26         | CHIP.99    | SRAM.A9    |                                                                                                  |
| 27         | CHIP.102   | SRAM.A8    |                                                                                                  |
| 28         | CHIP.103   | SRAM.A13   |                                                                                                  |
| 29         | CHIP.109   | SRAM.WE_N  |                                                                                                  |
| 30         | WEAK_VBA   | SRAM.CE2   | Seems to pass though some resistors and MM1026.                                                  |
| 31         | CHIP.105   | SRAM.A15   |                                                                                                  |
| 32         | VBA        | SRAM.VCC   | +3V from battery.                                                                                |


## ROM
### M27C322 EPROM (ST)
| Pin number | Connection | Pin name |            |
|------------|------------|----------|------------|
| --         | --         | --       | South side |
| 1          | CHIP.77    | ROM.A18  |            |
| 2          | CHIP.76    | ROM.A17  |            |
| 3          | CHIP.66    | ROM.A7   |            |
| 4          | CHIP.65    | ROM.A6   |            |
| 5          | CHIP.64    | ROM.A5   |            |
| 6          | CHIP.63    | ROM.A4   |            |
| 7          | CHIP.62    | ROM.A3   |            |
| 8          | CHIP.61    | ROM.A2   |            |
| 9          | CHIP.60    | ROM.A1   |            |
| 10         | CHIP.59    | ROM.A0   |            |
| 11         | GND        | ROM.EN_N |            |
| 12         | GND        | ROM.GND  |            |
| 13         | GND        | ROM.PRG  |            |
| 14         | CHIP.58    | ROM.Q0   |            |
| 15         | CHIP.57    | ROM.Q8   |            |
| 16         | CHIP.56    | ROM.Q1   |            |
| 17         | CHIP.55    | ROM.Q9   |            |
| 18         | CHIP.54    | ROM.Q2   |            |
| 19         | CHIP.53    | ROM.Q10  |            |
| 20         | CHIP.52    | ROM.Q3   |            |
| 21         | CHIP.51    | ROM.Q11  |            |
| --         | --         | --       | North side |
| 22         | VCC        | ROM.VCC  |            |
| 23         | CHIP.50    | ROM.Q4   |            |
| 24         | CHIP.49    | ROM.Q12  |            |
| 25         | CHIP.48    | ROM.Q5   |            |
| 26         | CHIP.47    | ROM.Q13  |            |
| 27         | CHIP.46    | ROM.Q6   |            |
| 28         | CHIP.45    | ROM.Q14  |            |
| 29         | CHIP.44    | ROM.Q7   |            |
| 30         | CHIP.43    | ROM.Q15  |            |
| 31         | GND        | ROM.GND  |            |
| 32         | CHIP.79    | ROM.A20  |            |
| 33         | CHIP.75    | ROM.A16  |            |
| 34         | CHIP.74    | ROM.A15  |            |
| 35         | CHIP.73    | ROM.A14  |            |
| 36         | CHIP.72    | ROM.A13  |            |
| 37         | CHIP.71    | ROM.A12  |            |
| 38         | CHIP.70    | ROM.A11  |            |
| 39         | CHIP.69    | ROM.A10  |            |
| 40         | CHIP.68    | ROM.A9   |            |
| 41         | CHIP.67    | ROM.A8   |            |
| 42         | CHIP.78    | ROM.A19  |            |


## SA-1 cart
| Pin number | Connection   | Pin name  |
|------------|--------------|-----------|
| 1          | C12+         | 21477_CLK |
| 2          | OPEN         | EXPAND    |
| 3          | OPEN         | PA6       |
| 4          | OPEN         | /PARD     |
| --         | --           | --        |
| 5          | GND          | GND       |
| 6          | CHIP.35      | A11       |
| 7          | CHIP.33      | A10       |
| 8          | CHIP.31      | A9        |
| 9          | CHIP.29      | A8        |
| 10         | CHIP.27      | A7        |
| 11         | CHIP.25      | A6        |
| 12         | CHIP.23      | A5        |
| 13         | CHIP.21      | A4        |
| 14         | CHIP.19      | A3        |
| 15         | CHIP.17      | A2        |
| 16         | CHIP.15      | A1        |
| 17         | CHIP.13      | A0        |
| 18         | CHIP.1       | /IRQ      |
| 19         | CHIP.9       | D0        |
| 20         | CHIP.7       | D1        |
| 21         | CHIP.5       | D2        |
| 22         | CHIP.3       | D3        |
| 23         | R6->CHIP.128 | /RD       |
| 24         | CHIP.125     | CIC_OUT_1 |
| 25         | CHIP.123     | CIC_IN    |
| 26         | CHIP.120     | /RESET    |
| 27         | VCC          | VCC       |
| --         | --           | --        |
| 28         | OPEN         | PA0       |
| 29         | OPEN         | PA2       |
| 30         | OPEN         | PA4       |
| 31         | OPEN         | AUDIO_L   |
| ==         | ==           | ==        |
| 62         | OPEN         | AUDIO_R   |
| 61         | OPEN         | PA5       |
| 60         | OPEN         | PA3       |
| 59         | OPEN         | PA1       |
| --         | --           | --        |
| 58         | VCC          | VCC       |
| 57         | CHIP.121     | CPU_CLK   |
| 56         | R5->CHIP.122 | CIC_CLK   |
| 55         | CHIP.124     | CIC_OUT_2 |
| 54         | CHIP.126     | WR_N      |
| 53         | CHIP.2       | D7        |
| 52         | CHIP.4       | D6        |
| 51         | CHIP.6       | D5        |
| 50         | CHIP.8       | D4        |
| 49         | OPEN         | CART_N    |
| 48         | CHIP.12      | A23       |
| 47         | CHIP.14      | A22       |
| 46         | CHIP.16      | A21       |
| 45         | CHIP.18      | A20       |
| 44         | CHIP.20      | A19       |
| 43         | CHIP.22      | A18       |
| 42         | CHIP.24      | A17       |
| 41         | CHIP.26      | A16       |
| 40         | CHIP.28      | A15       |
| 39         | CHIP.30      | A14       |
| 38         | CHIP.32      | A13       |
| 37         | CHIP.34      | A12       |
| 36         | GND          | GND       |
| --         | --           | --        |
| 35         | OPEN         | PAWR_N    |
| 34         | OPEN         | PA7       |
| 33         | CHIP.38, C14 | REFRESH   |
| 32         | OPEN         | WRAM_N    |

## SA-1 chip
### RF5A123 (NINTENDO)
38:26 pin ratio, total 128 pins.

| Number | Connection  | Description          | Note                                                           |
|--------|-------------|----------------------|----------------------------------------------------------------|
| --     | --          | --                   | South side                                                     |
| 1      | CART.18     | IRQ_N                |                                                                |
| 2      | CART.53     | D7                   |                                                                |
| 3      | CART.22     | D3                   |                                                                |
| 4      | CART.52     | D6                   |                                                                |
| 5      | CART.21     | D2                   |                                                                |
| 6      | CART.51     | D5                   |                                                                |
| 7      | CART.20     | D1                   |                                                                |
| 8      | CART.50     | D4                   |                                                                |
| 9      | CART.19     | D0                   |                                                                |
| 10     | C7+         | ?                    |                                                                |
| 11     | C7- // GND  | ?                    |                                                                |
| 12     | CART.48     | A23                  |                                                                |
| 13     | CART.17     | A0                   |                                                                |
| 14     | CART.47     | A22                  |                                                                |
| 15     | CART.16     | A1                   |                                                                |
| 16     | CART.46     | A21                  |                                                                |
| 17     | CART.15     | A2                   |                                                                |
| 18     | CART.45     | A20                  |                                                                |
| 19     | CART.14     | A3                   |                                                                |
| 20     | CART.44     | A19                  |                                                                |
| 21     | CART.13     | A4                   |                                                                |
| 22     | CART.43     | A18                  |                                                                |
| 23     | CART.12     | A5                   |                                                                |
| 24     | CART.42     | A17                  |                                                                |
| 25     | CART.11     | A6                   |                                                                |
| 26     | CART.41     | A16                  |                                                                |
| 27     | CART.10     | A7                   |                                                                |
| 28     | CART.40     | A15                  |                                                                |
| 29     | CART.9      | A8                   |                                                                |
| 30     | CART.39     | A14                  |                                                                |
| 31     | CART.8      | A9                   |                                                                |
| 32     | CART.38     | A13                  |                                                                |
| 33     | CART.7      | A10                  |                                                                |
| 34     | CART.37     | A12                  |                                                                |
| 35     | CART.6      | A11                  |                                                                |
| 36     | C8+         | VCC                  |                                                                |
| 37     | C8-         | GND                  |                                                                |
| 38     | CART.33     | C14+                 | REFRESH                                                        |
| --     | --          | --                   | East side                                                      |
| 39     | GND         |                      |                                                                |
| 40     | R3-         | ?                    | Goes though master clock.                                      |
| 41     | R2-         | ?                    | Goes though master clock.                                      |
| 42     | GND         |                      |                                                                |
| 43     | ROM.Q15     |                      |                                                                |
| 44     | ROM.Q7      |                      |                                                                |
| 45     | ROM.Q14     |                      |                                                                |
| 46     | ROM.Q6      |                      |                                                                |
| 47     | ROM.Q13     |                      |                                                                |
| 48     | ROM.Q5      |                      |                                                                |
| 49     | ROM.Q12     |                      |                                                                |
| 50     | ROM.Q4      |                      |                                                                |
| 51     | ROM.Q11     |                      |                                                                |
| 52     | ROM.Q3      |                      |                                                                |
| 53     | ROM.Q10     |                      |                                                                |
| 54     | ROM.Q2      |                      |                                                                |
| 55     | ROM.Q9      |                      |                                                                |
| 56     | ROM.Q1      |                      |                                                                |
| 57     | ROM.Q8      |                      |                                                                |
| 58     | ROM.Q0      |                      |                                                                |
| 59     | ROM.A0      |                      |                                                                |
| 60     | ROM.A1      |                      |                                                                |
| 61     | ROM.A2      |                      |                                                                |
| 62     | ROM.A3      |                      |                                                                |
| 63     | ROM.A4      |                      |                                                                |
| 64     | ROM.A5      |                      |                                                                |
| --     | --          | --                   | North side                                                     |
| 65     | ROM.A6      |                      |                                                                |
| 66     | ROM.A7      |                      |                                                                |
| 67     | ROM.A8      |                      |                                                                |
| 68     | ROM.A9      |                      |                                                                |
| 69     | ROM.A10     |                      |                                                                |
| 70     | ROM.A11     |                      |                                                                |
| 71     | ROM.A12     |                      |                                                                |
| 72     | ROM.A13     |                      |                                                                |
| 73     | ROM.A14     |                      |                                                                |
| 74     | ROM.A15     |                      |                                                                |
| 75     | ROM.A16     |                      |                                                                |
| 76     | ROM.A17     |                      |                                                                |
| 77     | ROM.A18     |                      |                                                                |
| 78     | ROM.A19     |                      |                                                                |
| 79     | ROM.A20     |                      |                                                                |
| 80     | ROM.A21     | Unused on this cart. | Pin for 8 MB ROMs.                                             |
| 81     | OPEN        | ?                    | Always gives VCC apparently.                                   |
| 82     | OPEN        | ?                    | Looks GND? I had trouble here because it was too close to VCC. |
| 83     | VCC         |                      |                                                                |
| 84     | GND         |                      |                                                                |
| 85     | GND         | ?                    | Some boards apparently has it OPEN instead.                    |
| 86     | SRAM.A16    |                      |                                                                |
| 87     | SRAM.A14    |                      |                                                                |
| 88     | SRAM.A12    |                      |                                                                |
| 89     | SRAM.A7     |                      |                                                                |
| 90     | SRAM.A6     |                      |                                                                |
| 91     | SRAM.A5     |                      |                                                                |
| 92     | SRAM.A4     |                      |                                                                |
| 93     | SRAM.A3     |                      |                                                                |
| 94     | SRAM.A2     |                      |                                                                |
| 95     | SRAM.A1     |                      |                                                                |
| 96     | SRAM.A0     |                      |                                                                |
| 97     | SRAM.A10    |                      |                                                                |
| 98     | SRAM.A11    |                      |                                                                |
| 99     | SRAM.A9     |                      |                                                                |
| 100    | C6+         | ?                    |                                                                |
| 101    | C6-         | ?                    |                                                                |
| 102    | SRAM.A8     |                      |                                                                |
| --     | --          | --                   | West side                                                      |
| 103    | SRAM.A13    |                      |                                                                |
| 104    | SRAM.A17    | $42-$43              | Extra SRAM pin for 256KB boards.                               |
| 105    | SRAM.A15    |                      |                                                                |
| 106    | SA-1 CLK    | Always 10.74 MHz     | VCC +5V square wave derived from PPU.                          |
| 107    | SNES CLK    | 2.68 or 3.58 MHZ     | VCC +5V square wave derived from PPU.                          |
| 108    | SRAM.OE_N   |                      |                                                                |
| 109    | SRAM.WE_N   |                      |                                                                |
| 110    | SRAM.D7     |                      |                                                                |
| 111    | SRAM.D6     |                      |                                                                |
| 112    | SRAM.D5     |                      |                                                                |
| 113    | SRAM.D4     |                      |                                                                |
| 114    | SRAM.D3     |                      |                                                                |
| 115    | SRAM.D2     |                      |                                                                |
| 116    | SRAM.D1     |                      |                                                                |
| 117    | SRAM.D0     |                      |                                                                |
| 118    | C10-        |                      |                                                                |
| 119    | C10+        |                      |                                                                |
| 120    | CART.26     | RESET_N              |                                                                |
| 121    | CART.57     | CPU_CLK              |                                                                |
| 122    | R5->CART.56 | CIC_CLK              | Passes though R5.                                              |
| 123    | CART.25     | CIC_IN               |                                                                |
| 124    | CART.55     | CIC_OUT_2            |                                                                |
| 125    | CART.24     | CIC_OUT_1            |                                                                |
| 126    | CART.54     | WR_N                 |                                                                |
| 127    | NTSC_N      | GND                  | According nocash, this is NTSC/PAL select pin.                 |
| 128    | R8->CART.23 | RD_N                 | Passes though R8.                                              |

## Battery
### CR2032
+ VBA
- GND

## Capacitors
| Number | +       | -              | Note               |
|--------|---------|----------------|--------------------|
| C7     | CHIP.10 | CHIP.11 // GND |                    |
| C8     | CHIP.37 | GND            |                    |
| C9     | VCC     | GND            |                    |
| C12    | CART.1  | R3 // C13+     | 21.477 MHz clock.  |
| C14    | CART.33 | CHIP.38        | REFRESH @ 2.68 MHz |


## Resistors
| Number | Estimated Resistance | +    | -       |
|--------|----------------------|------|---------|
| R2     | ~460k ohm            | R3   | CHIP.41 |
| R3     | ~1k ohm              | C13- | CHIP.40 |
| R6     | ~230 ohm             | ?    | ?       |

