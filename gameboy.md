## Gameboy (DMG) [GB]
### some models
dmg stands for dot matrix game (the original codename for the gameboy)
- dmg-01 (Game Boy) 1989
- mgb-001 (Game Boy Pocket) 1996
- mgb-101 (Game Boy Light) 1998
- cgb-001 (Game Boy Color) 1998

gameboy color had twice the cpu speed twice the ram and a color screen

---
the gamboy advance are a totally different architecture using arm processors, but 100% compatible with the gameboy and gameboy color
- agb-001 (Game Boy Advance) 2001

the original gameboy advance has no light and takes disposable batteries
- ags-001 (Gameboy Advance SP) 2003

this model has a front light and rechargeable battery
- agb-101 (Gameboy Advance SP) 2005

this model has a backlit screen and a rechargeable battery

---
console gameboy advance
all have complete gameboy hardware embedded in them
just puts its pixel into the host system instead of having its own screen

- SHVC-027 SGB (Super Gameboy) 1994
runs twice as fast as the gameboy

- SHVC-042 SGB2 (Super Gameboy 2) 1998
runs proper speed only released in japan

- DOL-017 (Gameboy Player) 2003
this is for the gamecube and plays gameboy games and gameboy advance games

### hardware
 - battery indicator red or green light
 - power switch
 - volume control
 - headphone jack
 - cartridge slot
 - start/select buttons
 - a/b buttons
 - directional pad
 - 66 mm (2.6 in) screen
 - speaker (mono)
 - link port (serial port to connect two gameboys together)
 - external power port
 - four double A batteries

---
### gameboy
- 1mhz processor* (4mhz) 8 bit
- 8kb internal ram
- 8kb video ram
-  160x144 pixels resolution
- 4 shades of gray
- 10 sprites per line

### NES
- 1.8mhz processor 8 bit
- 2kb internal ram
- 2kb video ram
- 256x240 pixels resolution
- 25 simultaneous colors
- 8 sprites per line

### SNES
- 3.6mhz processor 16 bit
- 128kb internal ram
- 64kb video ram
- 256x224 pixels resolution (512x448 pixels resolution)
- 32768 simultaneous colors
- 32 sprites per line
---
- dmg cpu B (Z80) 4mhz

### SoC
> cpu, interrupt controller, Timer, Memory, Boot Rom, Joypad Input, Serial Data Transfer, Sound Controller, Pixel Processing Unit.

- Ram Sharp LH5264N4 8kb
- Vram Sharp LH5264N4 8kb

### CPU

the nes came with a 6502
the snes came with a 65816 (16 bit version of the 6502)

the gameboy was released between these two consoles and had a  (sharp lr35902) somewhere between an intel 8080 and a zilog z80 (8 bit cpu with 16 bit address space bc of 16 bit pointers)

intel 8080 used in the altair 8800 (first computer billgates released software for) also used in imsai 8080)

the zilog z80 was used in about any other home computer of the time (zx spectrum,Osborne 1, TRS-80, etc)
the z80 is backwards compatible with the 8080

the sharp lr35902 uses some of the same opcodes as the z80, and some of the same opcodes as the 8080
but does not use all of either of them, and also has some opcodes that are unique to it.
the core features are the same as the 8080 (register set, instruction encoding)

## 8080 core architecture
### registers 
- 8 bit registers
    - A accumulator (special can do the arithmetic) and logic which are exclusive to this register
    - B
    - C
    - D
    - E
    - H
    - L
    - F flags only two useful flags (zero and carry) other two are for decimal adjust
    - SP stack pointer (also 16 bit)
    - PC program counter
- 16 bit registers can be used as pointers
- bc pair
- de pair
- hl pair

r8
- a
- b
- c
- d
- e
- h
- l
- (hl) the memory address pointed to by hl can be used in place of a register in any instruction

r16
- bc
- de
- hl
- sp

flags of gameboy
- z zero
- n subtract
- h half carry
- c carry
- _
- _
- _
- _

flags of 8080
- s sign
- z zero
- _
- h half carry
- _
- p parity
- _
- c carry
### instructions
- 8 bit load/store
    - ld r8,d8
    - ld r8,r8
    - ld a,(bc)
    - ld a,(de)
    - ld a, (a16) (different opcode than 8080)
    - ld (bc), a
    - ld (de), a
    - ld (a16),a (different opcode than 8080)
    - ld (r16),d16
-  stack (can only push and pop 16 bit registers)
    - ld sp,hl
    - push r16
    - pop r16

-  Arith/Logical 
    - add: a,r8/ a,d8
    - adc: a,r8/ a,d8
    - sub: a,r8/ a,d8
    - sbc: a,r8/ a,d8
    - xor: a,r8/ a,d8
    - or: a,r8/ a,d8
    - cp: a,r8/ a,d8
    - inc r8
    - dec r8
    - daa
    - cpl
    - add: hl, r16
    - inc: r16
    - dec: r16
   
-   Rotate
    - rlca
    - rla
    - rrca
    - rra
-   Control Flow
    - jp a16
    - jp hl
    - jr hl
    - jr f,a16
    - call a16
    - call f,a16
    
-   Misc
- ccf (complement carry flag)
- scf (set carry flag)
- nop (no operation)
- halt (halt cpu until interrupt)
- di (disable interrupts)
- ei (enable interrupts)

-   Unsupported by gameboy
    - sign/parity 

         - ret po
         - jp po, nn
         - call po, nn
         - ret pe
         - jp pe, nn
         - call pe, nn
         - ret p
         - jp p, nn
         - call p, nn
         - ret m
         - jp m, nn
         - call m, nn
    - load/store hl
         - ld (a16),hl
         - ld hl,(a16)
    - exchange
       - ex (sp),hl
       - ex de,hl
    - port/io (gameboy uses memory mapped io instead)
       - out (a8),a
       - in a,(a8)
### supported z80 features
- Shift & Bit Ops
    - rlc r8
    - rl r8
    - rrc r8
    - rr r8
    - sla r8
    - sra r8
    - srl r8
    - bit n,r8
    - set n,r8
    - res n,r8
      
  (cb prefix)

- Relative Jumps (more optimized ver of a jump)
    - jr a8
    - jr nz,a8
    - jr z,a8
    - jr nc,a8
    - jr c,a8

- Interrupt Return
    - reti (different opcode than z80)

---
not supported by gameboy from z80
second register set (af' bc' de' hl') (a' f' b' c' d' e' h' l') (IX and IY)

and instruction 
- auto increment and decrement (nice for copying memory)
  - (cpi/cpir/cpd/cpdr)
  - (ini/inir/ind/indr)
  - (outi/outir/outd/outdr)
  - (ldi/ldir/ldd/lddr)
  - (djnz)
- control flow
    - retn

- SPR
    - im 0/1/2
    - ld a, i 
    - ld i , a
    - ld a, r
    - ld r, a
- Alternate register set
    - ex af, af'
    - exx
- 16 bit load/store
    - ld r16, (a16)
    - ld (a16), r16
- 4 bit rotate
    - rld
    - rrd
- arithmetic
    - adc hl, r16
    - sbc hl, r16
    - neg
### new features exclusive to gameboy
- post increment and decrement
    - ld a,(hl+)
    - ld (hl+),a
    - ld a,(hl-)
    - ld (hl-),a
```asm
mem[hl] = a; hl++;
a = mem[hl]; hl++;
hl--; mem[hl] = a;
hl--; a = mem[hl];
```
- zeri page 
    - ld a,(0xff00 + c)
    - ld (0xff00 + c),a
    - ld a,(0xff00 + d8)
    - ld (0xff00 + d8),a
```asm
fa 40 ff  ld a,($ff40)   4 cycles
f0 40     ld a, ($ff40)    3 cycles
```
>optimized intstruction encoding for memory accesses that are in the top most page in ram
> not actually the zero page in ram but the top most page in ram (0xff00 - 0xffff) which is used for memory mapped io

- stack
    - add sp, r8
    - ld hl, sp+r8
- store SP
    - ld (a16), sp (z80 has a more generic version of this)
- Swap Nibbles
    - swap r8
- Power Saving
    - stop
> https://youtu.be/HyzD8pNlpwI?t=15m17s
opcode map
 
- opcode cp prefix hold another 256 opcodes (rotate and shift borrowed from z80)

```asm
ld a, (a16) 
3 bytes 16 clocks @ 4mhz 4 clocks @ 1mhz
```
> internet disagrees whether this should be seen as 4mhz or 1mhz

> 4mhz is the speed of the cpu 4 mibihertz 4,194,304 hz

> 1mhz is the speed of the ram 1 mibiherz 1,048,576 hz

> 4mhz is the speed of the ppu 4 mibiherz 4,194,304 hz

> vram runs at 2mhz 2 mibiherz 2,097,152 hz

> most of the numbers can be expressed at 1mhz
### interrupts
interupt model
 jumps to fixed points in ram at the beginning of the rom
for the different interrupts it jumps at different locations

0000 rst $00 (software interrupt) (rst $00 is the same as a reset)

0008 rst $08

00010 rst $10

00018 rst $18

00020 rst $20

00028 rst $28

00030 rst $30

00038 rst $38

00040 irq service routine #0

00048 irq service routine #1

00050 irq service routine #2

00058 irq service routine #3

00060 irq service routine #4


## memory 64KB
- 0x0000 - 0x00ff boot rom
- 0x0000-0x7FFF - 32KB ROM Bank two banks of 16KB (tetris fits in only 32kb)


       - 0x0000-0x3FFF - 16KB ROM Bank 0 (fixed)
       - 0x4000-0x7FFF - 16KB ROM Bank 1-n (switchable, in cartridge, if any)
       - other games added more chips that could switch between banks of rom
       - controlled by writing magic values into rom locations that then go to the cartidge 
       - and are interpreted by the memory bank controller which then can switch those banks

>code run automatically from the gameboy to boot up also includes game cartridge code


- 0x8000-0x9FFF - 8KB Video RAM
>gpu struct
- 0xA000-0xBFFF - 8KB External RAM
      
       - if the cart wants to expose extra ram for something like save games that are battery backed it 
       - can do so by exposing it here same as the rom banks it can be switched by writing to the cartidge

- 0xC000-0xCFFF - 4KB Work RAM Bank 0
>ram the game can use to store data
- 0xD000-0xDFFF - 4KB Work RAM Bank 1

- 0xE000-0xFDFF - Echo RAM

- 0xFE00-0xFE9F - Sprite Attribute Table (oem ram)

- 0xFEA0-0xFEFF - Not Usable

- 0xFF00-0xFF7F - I/O Ports

- 0xFF80-0xFFFE - High RAM

- 0xFFFF - Interrupt Enable Register
## boot rom
1. initialize the ram
2. initialize sound
3. setup logo
4. decode logo
5. scrolls logo
6. plays chime
7. compares logo to logo data
8. checksums header
9. turns off rom
```asm
; boot rom  
	LD SP,$fffe		; $0000  Setup Stack

	XOR A			; $0003  Zero the memory from $8000-$9FFF (VRAM)
	LD HL,$9fff		; $0004
Addr_0007:
	LD (HL-),A		; $0007
	BIT 7,H		; $0008
	JR NZ, Addr_0007	; $000a

	LD HL,$ff26		; $000c  Setup Audio
	LD C,$11		; $000f
	LD A,$80		; $0011 
	LD (HL-),A		; $0013
	LD ($FF00+C),A	; $0014
	INC C			; $0015
	LD A,$f3		; $0016
	LD ($FF00+C),A	; $0018
	LD (HL-),A		; $0019
	LD A,$77		; $001a
	LD (HL),A		; $001c

	LD A,$fc		; $001d  Setup BG palette
	LD ($FF00+$47),A	; $001f

	LD DE,$0104		; $0021  Convert and load logo data from cart into Video RAM
	LD HL,$8010		; $0024
Addr_0027:
	LD A,(DE)		; $0027
	CALL $0095		; $0028
	CALL $0096		; $002b
	INC DE		; $002e
	LD A,E		; $002f
	CP $34		; $0030
	JR NZ, Addr_0027	; $0032

	LD DE,$00d8		; $0034  Load 8 additional bytes into Video RAM
	LD B,$08		; $0037
Addr_0039:
	LD A,(DE)		; $0039
	INC DE		; $003a
	LD (HL+),A		; $003b
	INC HL		; $003c
	DEC B			; $003d
	JR NZ, Addr_0039	; $003e

	LD A,$19		; $0040  Setup background tilemap
	LD ($9910),A	; $0042
	LD HL,$992f		; $0045
Addr_0048:
	LD C,$0c		; $0048
Addr_004A:
	DEC A			; $004a
	JR Z, Addr_0055	; $004b
	LD (HL-),A		; $004d
	DEC C			; $004e
	JR NZ, Addr_004A	; $004f
	LD L,$0f		; $0051
	JR Addr_0048	; $0053

	; === Scroll logo on screen, and play logo sound===

Addr_0055:
	LD H,A		; $0055  Initialize scroll count, H=0
	LD A,$64		; $0056
	LD D,A		; $0058  set loop count, D=$64
	LD ($FF00+$42),A	; $0059  Set vertical scroll register
	LD A,$91		; $005b
	LD ($FF00+$40),A	; $005d  Turn on LCD, showing Background
	INC B			; $005f  Set B=1
Addr_0060:
	LD E,$02		; $0060
Addr_0062:
	LD C,$0c		; $0062
Addr_0064:
	LD A,($FF00+$44)	; $0064  wait for screen frame
	CP $90		; $0066
	JR NZ, Addr_0064	; $0068
	DEC C			; $006a
	JR NZ, Addr_0064	; $006b
	DEC E			; $006d
	JR NZ, Addr_0062	; $006e

	LD C,$13		; $0070
	INC H			; $0072  increment scroll count
	LD A,H		; $0073
	LD E,$83		; $0074
	CP $62		; $0076  $62 counts in, play sound #1
	JR Z, Addr_0080	; $0078
	LD E,$c1		; $007a
	CP $64		; $007c
	JR NZ, Addr_0086	; $007e  $64 counts in, play sound #2
Addr_0080:
	LD A,E		; $0080  play sound
	LD ($FF00+C),A	; $0081
	INC C			; $0082
	LD A,$87		; $0083
	LD ($FF00+C),A	; $0085
Addr_0086:
	LD A,($FF00+$42)	; $0086
	SUB B			; $0088
	LD ($FF00+$42),A	; $0089  scroll logo up if B=1
	DEC D			; $008b  
	JR NZ, Addr_0060	; $008c

	DEC B			; $008e  set B=0 first time
	JR NZ, Addr_00E0	; $008f    ... next time, cause jump to "Nintendo Logo check"

	LD D,$20		; $0091  use scrolling loop to pause
	JR Addr_0060	; $0093

	; ==== Graphic routine ====

	LD C,A		; $0095  "Double up" all the bits of the graphics data
	LD B,$04		; $0096     and store in Video RAM
Addr_0098:
	PUSH BC		; $0098
	RL C			; $0099
	RLA			; $009b
	POP BC		; $009c
	RL C			; $009d
	RLA			; $009f
	DEC B			; $00a0
	JR NZ, Addr_0098	; $00a1
	LD (HL+),A		; $00a3
	INC HL		; $00a4
	LD (HL+),A		; $00a5
	INC HL		; $00a6
	RET			; $00a7

Addr_00A8:
	;Nintendo Logo
	.DB $CE,$ED,$66,$66,$CC,$0D,$00,$0B,$03,$73,$00,$83,$00,$0C,$00,$0D 
	.DB $00,$08,$11,$1F,$88,$89,$00,$0E,$DC,$CC,$6E,$E6,$DD,$DD,$D9,$99 
	.DB $BB,$BB,$67,$63,$6E,$0E,$EC,$CC,$DD,$DC,$99,$9F,$BB,$B9,$33,$3E 

Addr_00D8:
	;More video data
	.DB $3C,$42,$B9,$A5,$B9,$A5,$42,$3C

	; ===== Nintendo logo comparison routine =====

Addr_00E0:	
	LD HL,$0104		; $00e0	; point HL to Nintendo logo in cart
	LD DE,$00a8		; $00e3	; point DE to Nintendo logo in DMG rom

Addr_00E6:
	LD A,(DE)		; $00e6
	INC DE		; $00e7
	CP (HL)		; $00e8	;compare logo data in cart to DMG rom
	JR NZ,$fe		; $00e9	;if not a match, lock up here
	INC HL		; $00eb
	LD A,L		; $00ec
	CP $34		; $00ed	;do this for $30 bytes
	JR NZ, Addr_00E6	; $00ef

	LD B,$19		; $00f1
	LD A,B		; $00f3
Addr_00F4:
	ADD (HL)		; $00f4
	INC HL		; $00f5
	DEC B			; $00f6
	JR NZ, Addr_00F4	; $00f7
	ADD (HL)		; $00f9
	JR NZ,$fe		; $00fa	; if $19 + bytes from $0134-$014D  don't add to $00
						;  ... lock up

	LD A,$01		; $00fc
	LD ($FF00+$50),A	; $00fe	;turn off DMG rom
```
usually a jump when game data starts 
```asm
0100 00 nop
0101 c3 50 01 jp $0150
0104
```
> header
```
0100 - 0103 (entry point) nop , jp $0150
0104 - 0133 (Nintendo logo) $CE, $ED, $66, $66, $CC, $0D, $00, $0B, $03, $73, $00, $83, $00, $0C, $00, $0D, $00, $08, $11, $1F, $88, $89, $00, $0E, $DC, $CC, $6E, $E6, $DD, $DD, $D9, $99, $BB, $BB, $67, $63, $6E, $0E, $EC, $CC, $DD, $DC, $99, $9F, $BB, $B9, $33, $3E
0134 - 0143 (title) "POKEMON RED" (uppercase ASCII)
013f - 0142 (manufacturer code) "01" (uppercase ASCII)
0143 - 0134 (CGB flag) $80
0144 - 0145 (new licensee code) "01" (uppercase ASCII)
0146 - 0147 (SGB flag) $00
0147 - 0148 (cartridge type) $00
0148 - 0149 (ROM size) $08
0149 - 014a (RAM size) $00
014a - 014b (destination code) $00
014b - 014c (old licensee code) $00
014c - 014d (mask ROM version number) $00
014d - 014e (header checksum) $00
014e - 014f (global checksum) $00, $00
```
there was no cleanup code, and it doesnt clear the screen
so  the nintendo logo is still on the screen, you could do something with it.

## Io and Hram
- 0xFF00 - 0xFFFF is IO
- 0xFF00 - 0xFF7F is Hram

- top most page of memory is IO and Hram
-top 127 bytes are extra ram
- 0xFF00 is the joypad register
```
FF00 - P1 - JOYP - ($FF00) - R/W - Joypad
FF01 - SB - SB - ($FF01) - W - Serial transfer data
FF02 - SC - SC - ($FF02) - R/W - SIO control (Serial I/O)
FF04 - DIV - DIV - ($FF04) - R/W - Divider Register
FF05 - TIMA - TIMA - ($FF05) - R/W - Timer counter
FF06 - TMA - TMA - ($FF06) - R/W - Timer Modulo
FF07 - TAC - TAC - ($FF07) - R/W - Timer control
FF0F - IF - IF - ($FF0F) - R/W - Interrupt Flag
FFFF - IE - IE - ($FFFF) - R/W - Interrupt Enable
FF10 - NR10 - NR10 - ($FF10) - W - Channel 1 Sweep register
FF11 - NR11 - NR11 - ($FF11) - W - Channel 1 Sound length/Wave pattern duty
FF12 - NR12 - NR12 - ($FF12) - W - Channel 1 Volume Envelope
FF13 - NR13 - NR13 - ($FF13) - W - Channel 1 Frequency lo data
FF14 - NR14 - NR14 - ($FF14) - W - Channel 1 Frequency hi data
FF16 - NR21 - NR21 - ($FF16) - W - Channel 2 Sound Length/Wave Pattern Duty
FF17 - NR22 - NR22 - ($FF17) - W - Channel 2 Volume Envelope
FF18 - NR23 - NR23 - ($FF18) - W - Channel 2 Frequency lo data
FF19 - NR24 - NR24 - ($FF19) - W - Channel 2 Frequency hi data
FF1A - NR30 - NR30 - ($FF1A) - W - Channel 3 Sound on/off
FF1B - NR31 - NR31 - ($FF1B) - W - Channel 3 Sound Length
FF1C - NR32 - NR32 - ($FF1C) - W - Channel 3 Select output level
FF1D - NR33 - NR33 - ($FF1D) - W - Channel 3 Frequency's lower data
FF1E - NR34 - NR34 - ($FF1E) - W - Channel 3 Frequency's higher data
FF20 - NR41 - NR41 - ($FF20) - W - Channel 4 Sound Length
FF21 - NR42 - NR42 - ($FF21) - W - Channel 4 Volume Envelope
FF22 - NR43 - NR43 - ($FF22) - W - Channel 4 Polynomial Counter
FF23 - NR44 - NR44 - ($FF23) - W - Channel 4 Counter/consecutive; Inital
FF24 - NR50 - NR50 - ($FF24) - W - Channel control / ON-OFF / Volume
FF25 - NR51 - NR51 - ($FF25) - W - Selection of Sound output terminal
FF26 - NR52 - NR52 - ($FF26) - R/W - Sound on/off
FF40 - LCDC - LCDC - ($FF40) - R/W - LCD Control
FF41 - STAT - STAT - ($FF41) - R/W - LCDC Status (STAT,LYC)
FF42 - SCY - SCY - ($FF42) - R/W - Scroll Y
FF43 - SCX - SCX - ($FF43) - R/W - Scroll X
FF44 - LY - LY - ($FF44) - R - LCDC Y-Coordinate (LY)
FF45 - LYC - LYC - ($FF45) - R/W - LY Compare
FF46 - DMA - DMA - ($FF46) - W - DMA Transfer and Start Address
FF47 - BGP - BGP - ($FF47) - R/W - BG & Window Palette Data
FF48 - OBP0 - OBP0 - ($FF48) - R/W - Object Palette 0 Data
FF49 - OBP1 - OBP1 - ($FF49) - R/W - Object Palette 1 Data
FF4A - WY - WY - ($FF4A) - R/W - Window Y Position
FF4B - WX - WX - ($FF4B) - R/W - Window X Position

```
- 0xFF00 is the joypad register
```
FF00 - P1 - JOYP - ($FF00) - R/W - Joypad
bit 7 - Not used
bit 6 - Not used
bit 5 - P15 Select Button Keys      (0=Select)
bit 4 - P14 Select Direction Keys   (0=Select)
bit 3 - P13 Input Down  or Start    (0=Pressed) (Read Only)
bit 2 - P12 Input Up    or Select   (0=Pressed) (Read Only)
bit 1 - P11 Input Left  or Button B (0=Pressed) (Read Only)
bit 0 - P10 Input Right or Button A (0=Pressed) (Read Only)
```
0xFF01 - 0xFF02 is serial transfer data
```
FF01 - SB - SB - ($FF01) - W - Serial transfer data
FF02 - SC - SC - ($FF02) - R/W - SIO control (Serial I/O)
bit 7 - Transfer Start Flag
bit 0 - Internal Clock Select (0=External, 1=Internal) clock speeds out are 8192khz and in is 0-524288khz
```

0xFF04 - 0xFF07 is timer
```
FF04 - DIV - DIV - ($FF04) - R/W - Divider Register
FF05 - TIMA - TIMA - ($FF05) - R/W - Timer counter
FF06 - TMA - TMA - ($FF06) - R/W - Timer Modulo
FF07 - TAC - TAC - ($FF07) - R/W - Timer control
bit 2 - Timer Stop  (0=Stop, 1=Start)
bit 1-0 - Input Clock Select
       00:   4096 Hz    (~4194 Hz SGB)
       01: 262144 Hz  (~268400 Hz SGB)
       10:  65536 Hz  (~67110 Hz SGB)
       11:  16384 Hz  (~16780 Hz SGB)
```
FFF0 - 0xFFFF is interrupt enable
```
FFFF - IE - IE - ($FFFF) - R/W - Interrupt Enable
bit 4 - joypad interrupt
bit 3 - serial interrupt
bit 2 - timer interrupt
bit 1 - LCD stat interrupt
bit 0 - vblank interrupt
```
FF00 - FF0F is interrupt flag
```
FF0F - IF - IF - ($FF0F) - R/W - Interrupt Flag
bit 4 - joypad interrupt flag (rst 60h)
bit 3 - serial interrupt flag (rst 58h)
bit 2 - timer interrupt flag (rst 50h)
bit 1 - LCD stat interrupt flag (rst 48h)
bit 0 - vblank interrupt flag (rst 40h)
```
FF10 - FF3F is sound
```
FF10 - NR10 - NR10 - ($FF10) - W - Channel 1 Sweep register
bit 6-4 - Sweep Time
bit 3   - Sweep Increase/Decrease  (0=Decrease, 1=Increase)
bit 2-0 - Sweep Shift Number
FF11 - NR11 - NR11 - ($FF11) - W - Channel 1 Sound length/Wave pattern duty
bit 7-6 - Wave Pattern Duty (00:12.5% 01:25% 10:50% 11:75%)
bit 5-0 - Sound length data (t1: 0-63)
FF12 - NR12 - NR12 - ($FF12) - W - Channel 1 Volume Envelope
bit 7   - Initial (1=Restart Sound)
bit 6   - Envelope Direction (0=Decrease, 1=Increase)
bit 5-0 - Number of envelope sweep (n: 0-7)
         (If zero, stop envelope operation.)
FF13 - NR13 - NR13 - ($FF13) - W - Channel 1 Frequency lo data
FF14 - NR14 - NR14 - ($FF14) - W - Channel 1 Frequency hi data
bit 7   - Initial (1=Restart Sound)
bit 6-4 - Frequency's higher data
bit 3   - Counter/consecutive selection
         (1=Stop output when length in NR11 expires)
bit 2-0 - Frequency's higher 3 bits (x)
FF16 - NR21 - NR21 - ($FF16) - W - Channel 2 Sound Length
FF17 - NR22 - NR22 - ($FF17) - W - Channel 2 Volume Envelope
FF18 - NR23 - NR23 - ($FF18) - W - Channel 2 Frequency's lower data
FF19 - NR24 - NR24 - ($FF19) - W - Channel 2 Frequency's higher data
FF1A - NR30 - NR30 - ($FF1A) - W - Channel 3 Sound on/off
bit 7   - Sound Channel 3 Off  (0=Stop, 1=Playback)
bit 6-0 - Not used
FF1B - NR31 - NR31 - ($FF1B) - W - Channel 3 Sound Length
FF1C - NR32 - NR32 - ($FF1C) - W - Channel 3 Select output level
bit 7-5 - Not used
bit 4-6 - Select output level (00=0%, 01=100%, 10=50%, 11=25%)
bit 3-0 - Not used
FF1D - NR33 - NR33 - ($FF1D) - W - Channel 3 Frequency's lower data
FF1E - NR34 - NR34 - ($FF1E) - W - Channel 3 Frequency's higher data
FF20 - NR41 - NR41 - ($FF20) - W - Channel 4 Sound Length
FF21 - NR42 - NR42 - ($FF21) - W - Channel 4 Volume Envelope
FF22 - NR43 - NR43 - ($FF22) - W - Channel 4 Polynomial Counter
bit 7-4 - Shift Clock Frequency (s)
bit 3   - Counter Step/Width (0=15 bits, 1=7 bits)
bit 2-0 - Dividing Ratio of Frequencies (r)
FF23 - NR44 - NR44 - ($FF23) - W - Channel 4 Counter/consecutive; Inital
bit 7   - Initial (1=Restart Sound)
bit 6   - Counter/consecutive selection
         (1=Stop output when length in NR41 expires)
bit 5-0 - Not used
FF24 - NR50 - NR50 - ($FF24) - W - Channel control / ON-OFF / Volume
bit 7-4 - Vin to SO2 terminal (volume) (0-0Fh)
bit 3-0 - Vin to SO1 terminal (volume) (0-0Fh)
FF25 - NR51 - NR51 - ($FF25) - W - Selection of Sound output terminal
bit 7   - Output sound 4 to SO2 terminal
bit 6   - Output sound 3 to SO2 terminal
bit 5   - Output sound 2 to SO2 terminal
bit 4   - Output sound 1 to SO2 terminal
bit 3   - Output sound 4 to SO1 terminal
bit 2   - Output sound 3 to SO1 terminal
bit 1   - Output sound 2 to SO1 terminal
bit 0   - Output sound 1 to SO1 terminal
FF26 - NR52 - NR52 - ($FF26) - R/W - Sound on/off
bit 7   - All sound on/off  (0=Stop all sound circuits) (Read Only)
bit 3   - Sound 4 ON flag (Read Only)
bit 2   - Sound 3 ON flag (Read Only)
bit 1   - Sound 2 ON flag (Read Only)
bit 0   - Sound 1 ON flag (Read Only)
```
4 voices of sound each get 5 registers
```
pulse a - 0xFF10 - 0xFF14
pulse b - 0xFF16 - 0xFF19
wave - 0xFF1A - 0xFF1E
noise - 0xFF20 - 0xFF23
control
frequency
volume
length
sweep
```
FF30 - FF3F is wave pattern RAM
```
simplist one 16 bytes of register 32 entries of 4 bits
FF30 - WAVE0 - WAVE0 - ($FF30) - W - Channel 3 Wave Pattern RAM
w0 w1 w2 w3 w4 w5 w6 w7 w8 w9 wA wB wC wD wE
T L _ _ _ F F F  F F F F F F F F  _ V V _ _ _ _ _  L L L L L L L L  _ _ _ _ _ _ _ _
pulse a - 0xFF10 - 0xFF14
T L _ _ _ F F F  F F F F F F F F  V V V V A P P P  D D L L L L L L  _ P P P N S S S
pulse b - 0xFF16 - 0xFF19
T L _ _ _ F F F  F F F F F F F F  V V V V A P P P  D D L L L L L L  _ _ _ _ _ _ _ _
noise - 0xFF20 - 0xFF23 (shift register) that gens psuedo randoms, 15 bit and 7 bit modes
T L _ _ _ _ _ _  S S S S W D D D  V V V V A P P P  _ _ L L L L L L  _ _ _ _ _ _ _ _
```

## pixel processing unit
```
FF40 - LCDC - LCDC - ($FF40) - R/W - LCD Control
bit 7 - LCD Display Enable             (0=Off, 1=On)
bit 6 - Window Tile Map Display Select (0=9800-9BFF, 1=9C00-9FFF)
bit 5 - Window Display Enable          (0=Off, 1=On)
bit 4 - BG & Window Tile Data Select   (0=8800-97FF, 1=8000-8FFF)
bit 3 - BG Tile Map Display Select     (0=9800-9BFF, 1=9C00-9FFF)
bit 2 - OBJ (Sprite) Size              (0=8x8, 1=8x16)
bit 1 - OBJ (Sprite) Display Enable    (0=Off, 1=On)
bit 0 - BG Display (for CGB see below) (0=Off, 1=On)
FF41 - STAT - STAT - ($FF41) - R/W - LCDC Status (Read/Write)
bit 6 - LYC=LY Coincidence Interrupt (1=Enable) (Read/Write)
bit 5 - Mode 2 OAM Interrupt         (1=Enable) (Read/Write)
bit 4 - Mode 1 V-Blank Interrupt     (1=Enable) (Read/Write)
bit 3 - Mode 0 H-Blank Interrupt     (1=Enable) (Read/Write)
bit 2 - Coincidence Flag  (0:LYC<>LY, 1:LYC=LY) (Read Only)
bit 1-0 - Mode Flag       (Mode 0-3, see below) (Read Only)
         0: During H-Blank
         1: During V-Blank
         2: During Searching OAM-RAM
         3: During Transfering Data to LCD Driver
FF42 - SCY - SCY - ($FF42) - R/W - Scroll Y
FF43 - SCX - SCX - ($FF43) - R/W - Scroll X
FF44 - LY - LY - ($FF44) - R - LCDC Y-Coordinate (Read Only)
FF45 - LYC - LYC - ($FF45) - R/W - LY Compare
FF46 - DMA - DMA - ($FF46) - W - DMA Transfer and Start Address
FF47 - BGP - BGP - ($FF47) - R/W - BG Palette Data
         Bit 7-6 - Shade for Color Number 3
         Bit 5-4 - Shade for Color Number 2
         Bit 3-2 - Shade for Color Number 1
         Bit 1-0 - Shade for Color Number 0
         (0=White, 1=Light Gray, 2=Dark Gray, 3=Black)
FF48 - OBP0 - OBP0 - ($FF48) - R/W - Object Palette 0 Data
            Bit 7-6 - Shade for Color Number 3
            Bit 5-4 - Shade for Color Number 2
            Bit 3-2 - Shade for Color Number 1
            Bit 1-0 - Shade for Color Number 0
            (0=White, 1=Light Gray, 2=Dark Gray, 3=Black)
FF49 - OBP1 - OBP1 - ($FF49) - R/W - Object Palette 1 Data (Same as OBP0)
FF4A - WY - WY - ($FF4A) - R/W - Window Y Position
FF4B - WX - WX - ($FF4B) - R/W - Window X Position minus 7
```
- 160x144 pixels
- 4 shades of gray
- 8x8 pixel tile-based, 20x18 background tiles
- 40 sprites (10 per line)
- 8 kb of VRAM

-  Tile
    - 8x8 pixels
    - 4 colors
      - 00 - black
      - 01 - light gray
      - 10 - dark gray
      - 11 - white
    - 2 bytes per line of pixels
    - 16 bytes per tile
    - 384 tiles per background
    - 256 tiles per window
    - 40 tiles per sprite

```
01 01 01 01 01 01 11 01    02 FF
01 10 10 10 01 01 10 10    73 8C
01 10 10 01 01 10 01 10    65 9A
01 10 01 01 10 01 01 00    B6 12
01 01 01 10 01 01 10 00    EC 26
01 01 10 01 01 10 10 00    D8 CE
11 10 01 01 10 10 10 00    60 80
01 10 10 00 00 00 00 00    
   
```
- FF47 - BGP - BGP - ($FF47) - R/W - BG Palette Data
        
    - Bit 7-6 - Shade for Color Number 3
    - Bit 5-4 - Shade for Color Number 2
    - Bit 3-2 - Shade for Color Number 1
    - Bit 1-0 - Shade for Color Number 0
    - (0=White, 1=Light Gray, 2=Dark Gray, 3=Black)
> on top of background there is another layer you can put on top called the window
> it can cover it fully or it can start at any location as there is an x an y coordinate for it
it will draw from there to the right to the bottom. 
there is no transparency in the window layer so usually you put it to the very right or the very bottom
great for a score board or something like that
- FF40 - LCDC - LCDC - ($FF40) - R/W - LCD Control
    - bit 7 - LCD Display Enable             (0=Off, 1=On)
    - bit 6 - Window Tile Map Display Select (0=9800-9BFF, 1=9C00-9FFF)
    - bit 5 - Window Display Enable          (0=Off, 1=On)
    - bit 4 - BG & Window Tile Data Select   (0=8800-97FF, 1=8000-8FFF)
    - bit 3 - BG Tile Map Display Select     (0=9800-9BFF, 1=9C00-9FFF)
    - bit 2 - OBJ (Sprite) Size              (0=8x8, 1=8x16)
    - bit 1 - OBJ (Sprite) Display Enable    (0=Off, 1=On)
    - bit 0 - BG Display (for CGB see below) (0=Off, 1=On)

> on top of the background and window you can put sprites FF40 obj enable
> . these are objects that dont fit into the 8x8 tile system, you can position them anywhere on the screen
> these are sprites but nintendo calls the obj for object
- FF48 - OBP0 - OBP0 - ($FF48) - R/W - Object Palette 0 Data
    - Bit 7-6 - Shade for Color Number 3
    - Bit 5-4 - Shade for Color Number 2
    - Bit 3-2 - Shade for Color Number 1
    - Bit 1-0 - Shade for Color Number 0
    - (0=White, 1=Light Gray, 2=Dark Gray, 3=Black)
>every sprite has attributes in the OAM Entry
> the top left is at pos 0x08 x pos 0x10 y  
> there are translucent pixels allowed in the sprite with the color 00  
> the sprite is 8x8 pixels and the color is 2 bits per pixel  
> you can have 40 sprites on the screen at once per line you can only have 10 sprites  
> this is per pixel line  
> OAM entry is 4 bytes long there are 40 of them and the whole thing is called the OAM RAM
- FF00-FF9F OAM Entry (Object Attribute Memory)  
    - Y Position
    - X Position
    - Tile Number
    - Attributes
        - Bit 7 - OBJ to BG Priority (0=OBJ Above BG, 1=OBJ Behind BG color 1-3)
        - Bit 6 - Y flip          (0=Normal, 1=Vertically mirrored)
        - Bit 5 - X flip          (0=Normal, 1=Horizontally mirrored)
        - Bit 4 - Palette number  **Non CGB Mode Only** (0=OBP0, 1=OBP1)
        - Bit 3 - Tile VRAM-Bank  **CGB Mode Only**     (0=Bank 0, 1=Bank 1)
        - Bit 2-0 - Not used
   
      
- FF40 -bit 2 - OBJ (Sprite) Size              (0=8x8, 1=8x16)
    > if you set this to 1 then the sprite is 8x16 pixels and the color is 2 bits per pixel  
  > but this is global and the whole system would have to deal with sprites 8x16 pixels