# 🎮 CS100 Terminal Tank Battle Game
[![C](https://img.shields.io/badge/Language-C-blue.svg)]
[![Terminal Game](https://img.shields.io/badge/Type-Console%20Game-green)]
[![License](https://img.shields.io/badge/License-Private-red)]

> Repository Status: PRIVATE (C source code not uploaded, only compiled executable file)
> Easter Egg Ending Quote: *Welcome to the real world, it sucks, but you will love it* — Tribute to Friends Season 1 Episode 1

## 📋 Table of Contents
- [Project Overview](#project-overview)
- [Core Customized Features](#core-customized-features)
- [Game Operation Instructions](#game-operation-instructions)
- [Compile & Run Guide](#compile--run-guide)
- [File Structure (Only Published Files)](#file-structure-only-published-files)
- [Game Design Ideas](#game-design-ideas)
- [Easter Egg Explanation](#easter-egg-explanation)
- [Bug & Optimization Summary](#bug--optimization-summary)

---

## 🎯 Project Overview
This is a terminal tank battle game developed based on the CS10 C language framework, completely implemented in standard C.
The project uses self-developed `Registry` generic container macro tool to manage all game objects (tanks, bullets), realizes double-buffer terminal rendering, random procedural map generation, and independent AI logic for enemy tanks.
On the basis of the standard assignment requirements, a large number of original gameplay mechanisms are added, with unique victory/defeat ending animation screens.

### Basic Standard Functions Completed
1. WASD control player tank movement, collision detection with walls, rocks and other tanks
2. Press K to shoot bullets, 15 frames shooting cooldown limit
3. Bullets can break destructible walls, cannot break solid stone blocks
4. Enemy random movement + random shooting simple AI with independent cooling control
5. Randomly generate 30*30 game map with solid blocks & breakable wall blocks

## ⚙️ Core Customized Original Features (Self-Added)
1. **Player Blood Bar System**
   Max HP 5, displayed in the bottom-left corner of the map; recover 1 HP when destroying enemy tanks, cap at 5 HP.
2. **Ultimate Skill Mechanism (Consecutive Kill Trigger)**
   Get 2 consecutive tank kills to activate ultimate skill (6s duration):
   - Tank automatically rotates clockwise continuously
   - Automatic rapid fire every 5 frames without manual pressing K
3. **Independent Object Cooling Logic**
   Each enemy tank has separate movement/shooting cooldown to avoid synchronized robot actions.
4. **Custom 3×3 Tank Sprite Rendering**
   Custom tank shape with H (body) + O (center) + Y (cannon) for 4 directions (up/down/left/right), different colors for player (green) and enemy (red).
5. **Two Ending Animation Screens**
   - Victory: Full-screen random fireworks animation + green victory text
   - Defeat: Fixed classic quote easter egg screen
6. **Complete Memory Auto Recycling**
   Encapsulated registry container automatically malloc/free all tanks/bullets, no memory leak after exiting.

## 🎮 Game Operation Instructions
| Key | Function |
|-----|----------|
| W / S / A / D | Control tank to move up / down / left / right |
| K | Fire bullet (normal state, 15 frames cooldown) |
| ESC | Exit game at any time |

## 🚀 Compile & Run Guide
### Windows
1. Use MinGW to compile source code locally:
```bash
gcc Main.c -Wall -Wextra -Wpedantic -o TankGame.exe
```
2. Double-click `TankGame.exe` to launch the terminal game.

### Linux / MacOS
```bash
gcc Main.c -o TankGame
./TankGame
```

## 📂 File Structure (Only Published Files in Repo)
📥 游戏可执行文件下载：[TankGame.exe](./game.exe)
```
cs100-terminal-tank-game/
├── TankGame.exe       # Compiled executable program (only public file)
├── README.md          # Project introduction document
```
> Note: All `.h` / `.c` source files are stored locally and not uploaded to this private repository to protect original code.

## 💡 Game Design Ideas
1. **Modular Architecture Split**
   Split the entire game into 7 independent header files by responsibility:
   - `Base.h`: Basic math, vector, color, random tool functions
   - `Registry.h`: Self-made generic linked-list container (C macro black magic), unified management of tank & bullet objects, simplify add/delete/traverse logic
   - `Scene.h`: Game object structure definition (Tank / Bullet / Map)
   - `Renderer.h`: Terminal double-buffer rendering module, draw tanks, bullets and map
   - `Terminal.h`: Cross-platform terminal input/cursor control adaptation
   - `Config.h`: Global game parameter configuration (FPS, map size, enemy quantity)
   - `Game.h`: Core game logic loop, collision detection, AI, skill, ending logic
   - `Main.c`: Program entry, initialize global game parameters

2. **Collision Detection Design**
   All tanks use 3×3 bounding box collision judgment; detect map boundaries, solid obstacles and other tank overlapping before movement to realize real physical blocking.
   Bullet collision classification judgment: solid stone blocks bounce bullets, breakable walls disappear after hit, cross-faction tanks are destroyed when hit.

3. **AI Balance Design**
   Enemy tanks have independent 10-frame movement cooldown and 20-frame shooting cooldown, only 30% shooting probability per cycle to avoid excessive difficulty.

4. **Playability Optimization**
   Add blood bar feedback and continuous kill ultimate skill to increase operation sense; design distinctive victory fireworks animation to reward clearing all enemies, enrich game feedback.

## 🎬 Easter Egg Explanation
The failure screen displays the line:
`Welcome to the real world, it sucks, but you will love it`
This sentence is a classic line from the American drama *Friends (老友记)* Season 1 Episode 1, added as a personal tribute easter egg when the player's HP drops to 0 and the game fails.

## ⚠️ Bug & Optimization Summary
1. Fixed iterator invalid bug when deleting bullets during frame traversal (pre-save next iterator pointer)
2. Added 3×3 block placement collision detection to avoid overlapping map obstacles
3. Unified cross-platform terminal keyboard input function to compatible Windows & Linux
4. All memory allocation matched free release, pass memory leak detection
5. Strict compile warning suppression under `-Wall -Wextra` parameters

