Simple 8-Bit Multi-Cycle CPU Design

This repository contains the design a of a simple 8-bit Multi-Cycle Central Processing Unit (CPU) developed in Logisim.

The CPU features a hard-wired control unit, an 8-bit Arithmetic Logic Unit (ALU), and a register file with 8 general-purpose registers. It supports basic arithmetic operations and data transfer instructions.

## Features

* **Architecture:** 8-bit Multi-Cycle Datapath.
* **Registers:** 8 General Purpose Registers (`R0` - `R7`), plus Accumulator (`A`) and Temporary (`B`) registers.
* **ALU:** Supports **Addition** and **Subtraction** operations with flags.
* **Control Unit:** Hard-wired control logic using combinatorial gates (AND-OR arrays).
* **State Machine:** Uses a 2-bit counter to manage instruction states ($T_0, T_1, T_2$).
* **Reset Logic:** Implemented **Synchronous Reset** mechanism to prevent race conditions and ensure stable state transitions.
* **Input:** Manual Instruction/Data entry via 8-bit `DIN` pins.

## ⚙️ Instruction Set Architecture (ISA)

The CPU uses an 8-bit instruction format: `II XXX YYY`
* **II:** Opcode (2 bits)
* **XXX:** Destination Register ($R_x$) Address (3 bits)
* **YYY:** Source Register ($R_y$) Address (3 bits)

| Instruction | Opcode | Format | Description | Cycles |
| :--- | :---: | :--- | :--- | :---: |
| **mv $R_x, R_y$** | `00` | `00XXXYYY` | Copy value from $R_y$ to $R_x$ ($R_x \leftarrow R_y$) | 2 |
| **mvi $R_x, D$** | `01` | `01XXX000` | Load immediate 8-bit value $D$ into $R_x$ | 2 |
| **add $R_x, R_y$** | `10` | `10XXXYYY` | Add $R_y$ to $R_x$ ($R_x \leftarrow R_x + R_y$) | 3 |
| **sub $R_x, R_y$** | `11` | `11XXXYYY` | Subtract $R_y$ from $R_x$ ($R_x \leftarrow R_x - R_y$) | 3 |

> **Note:** Arithmetic operations (`add`, `sub`) utilize a multi-cycle approach where operands are loaded into ALU registers ($A$ and $B$) before the result is written back.

