# PSoC 5LP Reaction Game

## Project Overview

This project implements a real-time reaction game on the 
PSoC 5LP (CY8C58LP, ARM Cortex-M3) platform.

The system measures user reaction time using hardware timers, displays random values on a 7-segment display, validates button inputs, and reports detailed statistics over UART.

The application is developed using the ERIKA Enterprise RTOS and follows structured embedded software design principles:

- Modular driver abstraction
- Clear separation between application and hardware layers
- Controlled variable scope
- Use of typedefs defined in `global.h`
- State-machine-driven execution inside the main loop
- Deterministic task execution under RTOS scheduling

The game runs for 10 rounds and outputs individual and total timing statistics.


---

## Functional Behavior

### Game Flow

1. User presses the **Start** button  
2. System waits for a random delay  
3. A random number (1–4) is displayed on the 7-segment display  
4. The user must press the corresponding button as fast as possible  
5. The system:
   - Validates button correctness  
   - Detects multiple button presses  
   - Measures reaction time using a hardware timer  
6. Feedback is provided:
   - **Success** → Point awarded + reaction time recorded  
   - **Error** → No point  
7. Steps 2–6 repeat for 10 rounds  
8. Final statistics are printed via UART:
   - Individual reaction times  
   - Total reaction time  
   - Final score  

---

## System Architecture

The software is structured in layered architecture:

### 1. Application Layer

- `main.c` → Contains the endless loop  
- `game.c / game.h` → Implements the game state machine and logic  

### 2. Driver Layer

Reusable hardware drivers:

- Button driver (debounce + multi-press detection)
- 7-segment display driver
- UART driver
- Timer driver
- Random number logic

### 3. Hardware Abstraction

- Pin mapping defined via schematic
- Hardware resources configured in PSoC Creator
- Peripheral integration handled through generated APIs


## Technical Features

- Random delay generation
- Random number generation (1–4)
- Timer-based reaction time measurement (ms resolution)
- UART output for debugging and result logging
- Controlled scope of variables
- Use of `const` where applicable
- Strict adherence to defined coding conventions

---

## UART Output Example
- Round 1: 421 ms - OK
- Round 2: 512 ms - OK
- Round 3: Wrong Button
---

## Hardware Requirements

- PSoC 5LP development board
- 4 push buttons
- 7-segment display
- UART connection (USB-UART bridge)

---

## Learning Objectives Demonstrated

This project demonstrates:

- Embedded real-time application design
- Driver reuse and abstraction
- Hardware/software integration
- Timing measurement techniques
- Input validation in embedded systems
- Structured iterative development
- UART-based diagnostic reporting

---

## Build Environment

- PSoC Creator
- Target device: CY8C5888LTQ-LP097
- Language: Embedded C
- RTOS: ERIKA Enterprise
