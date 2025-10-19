# 4-bit mini CPU processor

**Tool:** Logisim Evolution  
**Project Type:** CPU design with Multi-cycle microarchitecture  

## Overview

This project implements a **4-bit CPU** capable of executing 5 basic instructions:  
`NOP`, `LDA`, `LDI`, `ADD`, and `SUB`.

Originally designed as a single-cycle CPU, the processor was later optimized into a multi-cycle microarchitecture featuring a 2-phase clock system to eliminate race conditions and ensure stable instruction execution timing.  
The architecture models how real microprocessors fetch, decode, and execute instructions across multiple microcycles.

## Features

- 4-bit program counter (PC) and accumulator (ACC)  
- 16×8 ROM for instruction memory  
- 16×4 RAM for data memory  
- Instruction register (IR) with opcode + operand splitter  
- 4-to-16 decoder for instruction control logic  
- Memory data register (MDR) for stable memory reads  
- Arithmetic & logic unit (ALU) for add/subtract operations  
- 2-bit state counter (T0–T3 microcycle FSM) 
- 2-phase clock design (CLK and inverted CLK)  
- State-qualified enable logic - each module activates only in its required microcycle  

## Instruction Set

| Opcode | Instruction | Description |
|:------:|:-------------|:-------------|
| 0000 | NOP | No operation — processor idle |
| 0001 | LDA | Load value from RAM into ACC |
| 0010 | LDI | Load immediate operand value into ACC |
| 0011 | ADD | Add RAM[operand] to ACC |
| 0100 | SUB | Subtract RAM[operand] from ACC |

## Microcycle Timing (FSM)

| State | Phase | Operation |
|:------:|:------|:-----------|
| T0 | Fetch Address | PC drives the address to ROM |
| T1 | Fetch Instruction | ROM output loaded into IR; PC increments |
| T2 | Decode | IR decoded; RAM read if required (LDA/ADD/SUB); MDR stores output |
| T3 | Execute | ALU/ACC perform the instruction operation |

## How to Run

1. Open the project in Logisim Evolution  
2. Load the circuit file: `digital_prjct.circ`  
3. Tick the clock manually to observe the T0–T3 microcycle transitions  
4. Once verified, switch to auto-clock mode for continuous execution  
5. Update the ROM and RAM with instructions and operands as per requirement
