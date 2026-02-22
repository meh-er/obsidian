#Theory 

Stores the least significant byte (the "little end") first. This means that the first byte (At the lowest memory address) is the smallest, which makes the most sense to people who read right to left.


For the same 32-bit integer `0x12345678`, a little-endian system would store it as:

Address:   00   01   02   03
Data:        78   56   34   12

Here **0x78** is the least significant byte, placed at the lowest (00), followed by **0x56**, **0x34**, and **0x12** at the highest address (03)
