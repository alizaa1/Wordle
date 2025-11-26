# FPGA Wordle

A hardware implementation of the popular Wordle game, built entirely in Verilog for the Altera DE1-SoC FPGA. Players type guesses using a PS/2 keyboard while the VGA display renders letters, tiles, and colours in real time.

## Table of Contents
- Overview
- Features
- Hardware Requirements
- Game Controls
- File Structure
- Module Documentation
- Display System
- Game Logic
- Technical Details
- Customization
- Demo Gallery
- Future Improvements
- Tools Used

## Overview
This project recreates the iconic daily five-letter guessing game directly on FPGA hardware. All rendering, logic, and input handling is implemented in Verilog using the digital systems concepts learned throughout ECE241.

Players enter five-letter guesses using a PS/2 keyboard. The FPGA compares each guess to the target word and displays green, yellow, and grey tiles similar to the real game. The entire system runs in real time at 640×480 VGA output with 9-bit colour.

## Features
- Full Wordle gameplay (6 guesses, 5-letter words, colour-coded feedback)
- VGA display with real-time rendering of letters, tiles, and grid
- Sprite-sheet based letter rendering
- Hardware tile colouring for grey, yellow, and green
- PS/2 keyboard letter entry, backspace, and enter
- Finite state machines for input, logic, and display
- Pure hardware graphics without any CPU or software

## Hardware Requirements
- Altera DE1-SoC FPGA
- VGA monitor (640×480)
- PS/2 keyboard
- 50 MHz system clock (CLOCK_50)

## Game Controls
| Input | Function |
|-------|----------|
| A–Z | Enter letters |
| Backspace | Delete last letter |
| Enter | Submit guess |
| KEY[0] | Reset (active-low) |

## File Structure
### Core Modules
- `wordleTopLevel.v`  
  Top-level integration, VGA wiring, PS/2 interface, system state.

- `wordleDisplay.v`  
  Grid drawing, tile positions, letter placement.

- `drawLetter.v`  
  Renders one 38×37 letter from sprite ROM onto VGA.

- `drawTileColor.v`  
  Draws coloured background tiles (grey, yellow, green).

- `sprite_sheet.v`  
  ROM containing 26 letter bitmaps.

- `compareWord.v`  
  Wordle comparison logic with colour output encoding.

- `eventParser.v`  
  Converts PS/2 scancodes into usable game actions.

- `buffers.v`  
  Stores guesses and target words.

- `FSM.v`  
  Main gameplay FSM.

### Support Modules
- `PS2_Controller.v`
- `vga_adapter.v` (Altera UP IP)

## Display System
- 640×480 VGA resolution  
- 9-bit colour (3-3-3 RGB)
- Pixel-accurate tile placement
- 5×6 grid with 38×37 tiles
- Letter rendering using sprite ROM
- Centered win and lose screens

Tile colours:
- Grey: letter not in word  
- Yellow: right letter wrong place  
- Green: correct letter and position  

## Game Logic
### Core sequence:
1. Player types a guess
2. `compareWord` checks correctness
3. Colours generated for 5 letters
4. Display FSM draws coloured row
5. Move to the next row
6. Win if all greens, lose after 6 rows

### Target Words
Up to three predefined target words may be stored.

## Technical Details
| Parameter | Value |
|----------|--------|
| Resolution | 640×480 |
| Colour Depth | 9 bits |
| Tile Size | 38×37 |
| Rows | 6 |
| Columns | 5 |
| Clock | 50 MHz |

Design concepts used:
- Finite state machines
- Line-by-line VGA drawing
- Debounced PS/2 input parsing
- Sprite ROM lookup
- Dedicated guess counter to prevent premature state changes

## Customization
You can modify:
- Target words  
- Letter sprites  
- Tile colours  
- Background  
- Win/lose messages  
- Keyboard mappings  

## 🎥 Demo Gallery
![Wordle](https://github.com/user-attachments/assets/5a6bd6fc-14f9-4e45-80dc-5c42cfc4b1e8)

Link to slides: https://docs.google.com/presentation/d/e/2PACX-1vTQccX7mRjS4KjdPMT4b_SZh7facKOJLdeaH-8s9pCPjQMyzwNOgUMMaQmyXP3Hhp4GLKjpc4OQt3di/pub?start=false&loop=false&delayms=3000

## Tools Used
- Verilog HDL
- Quartus Prime
- ModelSim
- DE1-SoC FPGA
- VGA 640×480 @ 60Hz
- PS/2 Keyboard Protocol
- FSM design
- Memory-mapped sprite ROMs

## Future Improvements
- Add tile flip animations like real Wordle
- Add a word list stored in RAM for randomization
- Add a main menu + intro screen
- Add a timer or “daily challenge” mode
