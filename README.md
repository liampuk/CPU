# CPU design

A simple 8-bit CPU loosely based on the SAP-2 computer from [Digital Computer Electronics](https://www.academia.edu/40474484/Digital_Computer_Electronics_Albert_Paul_Malvino).

## Architecture

![architecture](https://i.imgur.com/DEGpLQG.png)

Features of the CPU include:
- 256 bytes ROM (program memory)
- 256 bytes RAM (data memory)
- 4 registers
- I/O ports
- Hardware interrupt
- Stack pointer
- 8-bit data/address bus

## ROM/RAM

ROM is used to store program code, and RAM is used during program execution to store data. The CPU determines whether to access ROM or RAM based on the current instruction (e.g. `MOV [A], B` is a memory operation, so RAM will be accessed).

ROM will be implemented using an EEPROM, which can be programmed with a dip switch. This enables the CPU to retain program data when turned off. ROM contains the program code.

## ALU

The ALU uses two registers (X and Y) to latch inputs so the value can be output straight to the bus. It has 9 functions that are controlled by a 3-bit input (MODE), and an output enable (ALUo).

The table below describes how these inputs are combined to carry out functions.

| OP  | MODE | ALUo | REG X | REG Y |
|-----|------|------|-------|-------|
| ADD | 000  | 1    | A     | B     |
| SUB | 001  | 1    | A     | B     |
| INC | 010  | 1    | A     | 0     |
| DEC | 011  | 1    | A     | 0     |
| AND | 100  | 1    | A     | B     |
| OR  | 101  | 1    | A     | B     |
| XOR | 110  | 1    | A     | B     |
| NOT | 011  | 1    | 0     | A     |
| CMP | 001  | 0    | A     | B     |