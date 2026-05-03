# Project README

## Overview
This project is a simple raycasting implementation in C. It includes both the source code and necessary build scripts for various platforms.

## Features
- Basic 2D raycasting engine to render a scene.
- Support for different platforms including Linux, Windows, Wine, and WebAssembly.
- Uses OpenGL for rendering on Linux and macOS.

## Project Structure
```
Gui_Raycaster_Modern/
├── build/              # .exe files produced by Main.c
├── bin/                # .so / .dll produced by *.c in libs
├── libs/               # *.c for bin
├── lib/                # librarys for my own languages
├── code/               # scripts from my custom languages for example .rex, .ll, .omml
├── data/               # Datafile for example .txt or dumped files
├── assets/             # images and sound files
├── src/                # src code
│   ├── Main.c          # Entry point
│   └── *.h             # stand alone Header-based C-files, without *.c files that implement it
├── Makefile.linux      # Linux Build configuration
├── Makefile.windows    # Windows Build configuration
├── Makefile.wine       # Wine Build configuration
├── Makefile.web        # Emscripten Build configuration
└── README.md           # This file
└── LICENCE
└── .gitignore
```

### Prerequisites
- C/C++ Compiler and Debugger (GCC, Clang)
- Make utility
- Standard development tools
- Libraries needed in specific projects:
  - Linux: X11, OpenGL, PNG, JPEG
  - Windows: WINAPI, X11, ALSA
  - WebAssembly: Emscripten

## Build & Run
### Linux
```sh
cd Gui_Raycaster_Modern
make -f Makefile.linux all
./build/Main
```

### Windows
```sh
cd Gui_Raycaster_Modern
make -f Makefile.windows all
./build/Main.exe
```

### Wine (Linux Cross Compile for Windows)
```sh
cd Gui_Raycaster_Modern
make -f Makefile.wine all
wine build/Main.exe
```

### WebAssembly (Emscripten)
```sh
cd Gui_Raycaster_Modern
emcc -O0 -msimd128 -mavx2 -std=gnu17 -Wall -Wno-unused -Wshadow -Werror -Isrc -D_WEB -sINITIAL_MEMORY=169082880 src/*.c -o build/index.html -s USE_SDL=0
emrun --no_browser --port 8080 build
```

# Build Steps
```sh
cd Gui_Raycaster_Modern
make -f Makefile.linux all  # For Linux
make -f Makefile.windows all  # For Windows
make -f Makefile.wine all  # For Wine
make -f Makefile.web all  # For WebAssembly

# For clean rebuild:
make -f Makefile.linux clean
make -f Makefile.windows clean
make -f Makefile.wine clean
make -f Makefile.web clean

# If there are ./bin and ./libs directories, build libs with:
make -f Makefile.linux cleanlib
make -f Makefile.windows cleanlib
make -f Makefile.wine cleanlib
make -f Makefile.web cleanlib

# Build Options
make -f Makefile.linux all     # build output
make -f Makefile.windows do      # build + exe output
make -f Makefile.wine clean   # Remove build artifacts

# Execute it with make:
make -f Makefile.linux exe
make -f Makefile.windows exe
make -f Makefile.wine exe
make -f Makefile.web exe
```