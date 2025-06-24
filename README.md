## Life Force SNES Port - V 1.0

This is a 1:1 port of the NES version of Life Force, running on the SNES. It is utilizing FastROM/HiROM.

This has been tested in Mesen2, MiSTer, on original hardware via FxPak Pro, as well as a physical cart using a MouseBite Labs board.

NES-style music is provided via Memblers 2A03 Emulator.

## Additional Features

MSU-1 Audio music is supported.  If your platform supports MSU-1 Audio, there are 5 included packs available.

Additionally, the following Quality-of-Life options are available:
1. Set lives to values from 3 to 99.
2. Set the difficulty from easy, medium and hard without having to loop the game.
3. 8 different palettes to choose from.  You can select it on the intro options, or while paused you can press SELECT to cylce through them.

## MSU-1 Track List
Track Indexes:

* 01 - Level 1
* 02 - Level 2
* 03 - Level 3
* 04 - Level 4
* 05 - Level 5
* 06 - Level 6
* 07 - Boss
* 08 - Death
* 09 - Ending
* 10 - Level 5 Mini Boss
* 11 - Level 5 2nd half

Additionally, this romhack supports 5 playlists.  For each playlist after the first, add 16 to each track number for the next playlist (1-11, 17-27, 33-43, etc).

Included are 5 sets of PCMs for Life Force:

* Rock AST by Relikk
* Synth AST by Batty
* VRC6 Cover by Batty
* Arcade by Batty
* X68000 Midi by Relikk

## Prerequisites

* [cc65](https://www.cc65.org/) - the 65c816 compiler and linker
* [Go](https://go.dev/) - Go is used for a few useful scripts/tools


## Other Userful Tools I've used for this project

* [Mesen2](https://github.com/SourMesen/Mesen2) - A fantastic emulator for development on a bunch of platforms
* [HxD](https://mh-nexus.de/en/hxd/) - A Hex Editor
* [Visual Studio Code](https://code.visualstudio.com/) - Used as the development environment

## Structure of the Project

* `bankX.asm` - The NES memory PRG banks, there are 8 of them.  This code is heavily edited/altered for the port  
* `chrom-tiles-X.asm` - The NES CHR ROM banks, also 8 of them. These are untouched aside from converting them to the SNES tile format that we use.  The go script takes care of that for you.
* `2a03_xxxxx.asm` - Sound emulation related code
* `bank-snes.asm` - All the code that runs in the `A0` bank, this is where we put most of our routines and logic that we need that is SNES-specific.  Also includes various included asm files:

  * `attributes.asm` - dealing with tile and sprite attributes
  * `hardware-status-switches.asm` - various useful methods to handle differences in hardware registers
  * `hud-hdma.asm` - HDMA logic for the player health bars and names to be shown
  * `intro_screen.asm` - Title card that is shown at the start of the game
  * `palette_lookup.asm` and `palette_updates.asm` - palette logic
  * `sprites.asm` - sprite conversion and DMA'ing
* `msu.asm` - MSU-1 Support Code
* `main.asm` - the main file, root for the project
* `options_xxxx.asm` - Options screen related code.  Parts of this are genearted by `generate_options_asm.go` in the utilities directory
* `qol.asm` - various Quality-of-Life routines are here
* `vars.inc`, `registers.inc`, `macros.inc` - helpful includes
* `resetvector.asm` - the reset vector code
* `hirom.cfg` - defines how our ROM is laid out, where each bank lives and how large they are
* `windows.asm` - used for managing the windows that sometimes hide the left side of the screen.
* `wram_routines.bin` - binary copy of audio routines that we put in work ram to make them available to all banks.

## Building

* Update the `build.sh` file with the location of your cc65 install
* make sure you've extracted and copied the rom banks to `/src`
* port all the changes you need to port! (magic)
* run `build.sh`
* The output will be in `out/`
