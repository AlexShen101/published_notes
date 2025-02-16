---
{"dg-publish":true,"permalink":"/my-notes/implementing-helper-functions-in-mips/","created":"2024-06-21T21:19:04.784-05:00","updated":"2024-06-21T21:19:35.662-05:00"}
---


## Introduction
MIPS assembly language is a low-level programming language that writes instructions for processors with the MIPS architecture. Today, I'll be discussing how we implement helper functions in MIPS code.

## Quick Intro to RAM in MIPS
When a program is loaded into memory, the loader reserves a block of RAM for the program's use. The register `$30` is set to point just past the last word of memory allocated. This setup allows for dynamic memory management through a stack-like structure. 

### Memory Allocation
- **Pushing onto the Stack:** When adding items to memory, `$30` is moved up.
- **Popping from the Stack:** When removing items from memory, `$30` is moved down.

## Using Procedures in MIPS
Procedures in MIPS are the equivalent to functions in your code. To implement them we need to consider a few things:
- How do we call a procedure and return from them?
- How do we pass arguments to procedures?
- How do we protect data from being altered by procedures, given that registers are finite?

### Calling Procedures and Returning
To call a procedure, the `jalr` (Jump and Link Register) instruction is used. This instruction jumps to the procedure's location and sets `$31` to the address of the instruction following the call, which serves as the return location.
- **Note:** Since `jalr` overwrites `$31`, the previous value must be saved in RAM or another register before calling the procedure.

### Passing Arguments to Procedures
Arguments can be passed to procedures using either registers or memory. Similarly, return values can also be stored in registers or in memory. It is important to document what registers or stack addresses a procedure uses as arguments, and where it stores return values. By convention, register `$3` is typically used to store the return value of a function.

## Protecting Data in Registers
Procedures can modify registers, potentially overwriting important data. To prevent this, we can save the current register values in RAM and restore them after the procedure completes. We use register `$30` to help keep track of used RAM for temporarily storing register values.

### Example
Assume a procedure wants to use registers `$1`, `$4`, `$10`, and `$11`. At the start, we save these registers:
```mips
sw $1, -4($30)
sw $4, -8($30)
sw $10, -12($30)
sw $11, -16($30)
addi $30, $30, -16  # Adjust $30 to point at the last item stored
```
At the end of the procedure, the registers are restored, and `$30` is readjusted accordingly.

