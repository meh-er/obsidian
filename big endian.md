#Theory 

Stores the most significant byte (the "big end") first. This means that the first byte (At the lowest memory address) is the largest, which makes the most sense to people who read left to right.

For instance, a 32-bit integer  `0x12345678` would be stored in memory as follows in a big-endian system

Address:   00   01   02   03
Data:         12   34   56   78

Here  **0x12** is the MSB, placed at the lowest address (00), folllowed by **0x34**, **0x56**, and **0x78** at the highest address (03)

