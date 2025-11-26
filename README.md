# Wordle

A hardware-implemented recreation of Wordle, built entirely on the DE1-SoC FPGA using Verilog.
Users type guesses via a PS/2 keyboard, and the FPGA renders all letters, tiles, and game states directly to a 640×480 VGA display.

✨ Project Highlights

- Full Wordle gameplay implemented as hardware modules
- Real-time VGA rendering with a custom sprite sheet
- PS/2 keyboard input handling
- Correct Wordle logic: green / yellow / gray feedback
- Hardware FSM controlling all display stages
- Win/Lose screens drawn using sprite ROM letters
- Fully synthesized and tested on the DE1-SoC board

🧠 System Architecture

🎨 Display System (VGA)
- drawLetter - pulls pixels from a sprite ROM and draws each letter
- drawTileColor - fills grid tiles with the correct colors
- wordleDisplay - grid layout, coordinates, and plot timing
- Display FSM - orchestrates drawing order
- Sprite Sheet ROM - custom-designed letters

🎮 Game Logic

- buffers - 5-letter guess buffer
- compareWord - Comparison module (green/yellow/gray rules)
- FSM - Win/Lose detection logic

⌨️ Input Handling

- PS/2 keyboard interface
- Event parser for letters, Backspace, Enter

🌟 My Contributions

- Designed the entire VGA rendering pipeline
- drawLetter
- drawTileColor
- VGA grid placement
- Display FSM
- Integrated the sprite sheet (letter ROM)
- Built all tile coloring logic
- Performed full on-board debugging (timing bugs, plot issues, grid misalignment)
- Organized all Quartus project files
- Created simulation testbenches (ModelSim) for display modules
- Helped integrate top-level gameplay and display logic
- Took lead on documentation + slides + final presentation

🎥 Demo Gallery

Wordle grid on VGA
Typed letters appearing in real time
Correct color feedback
Win screen

🗂 Repo Contents

This repo contains:
Block diagrams
Presentation slides
Project proposal
Demo images/videos

🧰 Tools Used
- Verilog HDL
- Quartus Prime
- ModelSim
- DE1-SoC FPGA
- VGA 640×480 @ 60Hz
- PS/2 Keyboard Protocol
- FSM design
- Memory-mapped sprite ROMs

🌿 Future Improvements
- Add tile flip animations like real Wordle
- Add a word list stored in RAM for randomization
- Add a main menu + intro screen
- Add a timer or “daily challenge” mode
