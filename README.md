# game_spop
A work in progress Gameboy emulator written in C.

## Build project:

### Linux / macOS / Unix:

You need to have [SDL2](https://wiki.libsdl.org/SDL2/Installation) and [CMake](https://cmake.org/) installed.

```console
mkdir build
cd build
cmake .. -G "Unix Makefiles"
make
```

(Note: build have only been tested on Linux for now).

### Windows:

In MinGW [MSYS2](https://www.msys2.org/) terminal, install the following packages (if needed):
```console
pacman -S --needed  mingw-w64-x86_64-SDL2 \
                    mingw-w64-clang-x86_64-toolchain  
```
Build:
```console
mkdir build
cd build
cmake .. -G "MinGW Makefiles"
mingw32-make
```

## How to use:

You need a Gameboy ROM file.

OPTIONAL: to run the bootrom, create a folder called `boot_rom` in the executable path.
          Paste the Gameboy DMG boot ROM in this folder with the name `dmg_rom.bin`. Then
          run the program with `-b` option. It is possible to run only the bootrom, without 
          any ROM.

### Usage:
```console
./game_spop <ROM file> [options]
```

### Options:
* `--audio`, `-a`           = disable audio.
* `--audio-log`             = print various audio variables in a file at each sample.
* `--breakpoint`, `-p`      = enable debugging with breakpoints. The program will
                              ask to enter a PC value breakpoint at start, and will
                              ask for a new breakpoint when the previous one is
                              reached.
* `--bootrom`, `-b`         = launch the DMG bootrom before ROM. If no ROM is
                              provided, this option is always on. The file path must
                              be `boot_rom/dmg_rom.bin`.
* `--debug-info`, `-i`    = print cpu state at each instruction.
* `--gb-doctor`, `-d`    =  log cpu state into a file to be used with the [Gameboy
                            doctor tool](https://github.com/robert/gameboy-doctor) (only at launch).
                            Emulator behavior might be inaccurate since LY reading always send 0x90 in
                            this mode.
* `--log-instrs`, `-l`  = log cpu state into a file for comparison with other
                        emulators (only at launch).
* `--step`, `-s`        = enable step by step debugging. Emulator will stop
                          at each new instruction and ask to continue or edit options.
* `--help`, `-h`        = show this help message and exit.

### Controls:

Controls are customizable through the file `game_spop.ini`. If the file doesn't exist, it is 
automatically created with default parameters in the current path when the program is launched.

To modify a control, write a key name after the wanted control, using one of the names provided in the
`Key Name` column in the [SDL_Keycode documentation](https://wiki.libsdl.org/SDL2/SDL_Keycode). If a control
or keyname is missing or unvalid, default controls are applied.

This table shows the default controls:

Control   | QWERTY key | AZERTY key | Bépo key
---       | :---:      | :---:      | :---:
UP        | W          | Z          | é
DOWN      | S          | S          | U
LEFT      | A          | Q          | A
RIGHT     | D          | D          | I
START     | Return     | Return     | Return
SELECT    | RShift     | RShift     | RShift
A         | L          | L          | R
B         | M          | ,          | Q
Pause emulation | P | P | P
Show an option menu (during pause) | O | O | O
Next frame (during pause) | N | N | N
Toogle fast forward | SPACE | SPACE | SPACE
Toogle fullscreen | F11 | F11 | F11

Note: for other keyoard layouts, scancodes are used for Gameboy joypad buttons controls (same keys positions 
but different key names), and keycodes for other emulator options (same key names but possible different positions).
