---
{"dg-publish":true,"permalink":"/notes/representing-numbers-in-computers/","created":"2024-06-17T22:40:55.696-04:00","updated":"2024-06-17T22:41:13.057-04:00"}
---


One of the fundamental ideas in programming is representing numbers. At the core of this concept lies binary representation, the language of computers. Binary only contains the digits 0 and 1, but by chaining these digits into strings, we can represent larger numbers. Let's delve into the details of how numbers are represented in computers, particularly focusing on unsigned and signed integers.

## Unsigned Integers
Binary strings can be directly converted to unsigned integers. The binary string is read similar to a normal decimal number starting form the rightmost bit.

For example, the binary number 1011 represents $1 \cdot 2^{3} + 0 \cdot 2^{2} + 1 \cdot 2^{1} + 1 \cdot 2^{0} = 8 + 0 + 2 + 1 = 11$ 

However, we also want to be able to represent negative numbers. To do this, we use a signed bit.

## Signed Integers
Signed integers use the leftmost bit (most significant bit) to indicate the sign of the number (0 for positive, 1 for negative)

### Sign Magnitude
The simplest way to represent signed integers is the sign magnitude method. In this approach, the leftmost bit represents the sign, and the remaining bits represent the magnitude of the number, treated as an unsigned integer.

For example, in an 8-bit system:
- The binary number 00001010 represents +10.
- The binary number 10001010 represents -10.

While straightforward, this method has a significant drawback: it requires separate circuits for addition and subtraction, complicating the arithmetic operations.

### Two's Complement
Another method of representing signed integers is two's complement.

If we take the sign magnitude representation for 0 (00000000) and subtact 1 from it, the circuit will underflow and return (11111111). So we use this to our advantage and set this value to -1. Thus, if we add 1 to -1, the circuit will overflow and return 0.

From there, we map the rest of the negative values based on the value of -1.

Two's complement has several advantages:
- It allows for a single zero representation (00000000).
- Arithmetic operations like addition and subtraction are simplified since both positive and negative numbers can be processed using the same circuitry.


To get a negative number, we take the binary representation of its positive counterpart, invert all the bits, and then add 1 to the result. 
