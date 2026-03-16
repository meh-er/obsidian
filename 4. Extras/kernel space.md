#Theory #OSSP 

Kernel space is reserved for running a privileged Operating System kernel, kernel extensions, and most device drivers.
- Some OS are single address space OS - single address space for all user mode code.

Have separate logical addresses for kernel an user memory.
For 32-bit architectures (4GB [[virtual memory]]):
- Kernel space address are the upper 1GB of address space (>= 0xC000000)
- [[User space]] addresses are 0x0 to 0xBFFFFFF (lower 3GB)

Kernel memory is always mapped but protected against access by user processes

For 64-bit architectures:
- kernel space address are the upper half of address space (>= 0x8000 0000 0000 0000)
- [[User space]] addresses are 0x0 0x7fff ffff ffff, starting from above

