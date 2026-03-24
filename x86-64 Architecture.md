---
tags:
  - SaN
---
### Registers
Small but extremely fast units of storage for the CPU. Referenced by *name*
- *General Purpose Registers* for computations etc
- *Special Purpose Registers* that store the instruction pointer (program counter) etc

### Memory (RAM)
Large(r) chunk of data. Referenced by [[address]]. 
- Contains *code, [[heap]]* and [[stack]].

### Register Aliasing
The registers RAX, EAX, AX, AH, AL all describe different parts of the same memory cell.
This is called *register aliasing*


### Common Instructions
#### Data Movement
- `mov dst, src` => Move data from src to dst
- `push src` => Push src onto the stack
- `pop dst` => Pop value from the stack and store it in dst

#### Arithmetic
- `add dst, src` => dst += src
- `sub dst, src` => dst -= src
- `imul dst, src` => dst `*`= src (signed multiply)
After an arithmetic operation; flags are set:
- ZF: zero flag, set to 1 if the result is 0
- SF: sign flag, set to 1 if the result is negative
- OF: overflow flag, set to 1 if operation overflowed

#### Control Flow:
- `jmp label` => Jump to label
- `call fn` => Pushes instruction pointer  (IP) onto stack, jump to function
- `ret` => pops IP from stack (and continues there)
- `cmp a, b` => Calculates b-a and sets flags
- `test a, b` => Calculates a&b and sets flags
- `je label` => Jumps to label if zero flag is set
- `jne label` -> Jumps to label if zero flag is not set
- `nop` => No-op instruction - doesn't do anything

#### Bitwise Operations
- `and dst, src` => dst &= src
- `or dst, src` => dst |= src
- `xor dst, src` => dst ^= src

### Memory Addressing
Square brackets indicate that the operand is a **memory addresss** - rather than a direct value or register
- **Direct Memory Access** `[address]`
	- E.g. `mov aeax [0x1234]`: *Move the value at address 0x1234 into eax*
- **Register-based Memory Access: ** `[register]``
	- E.g. `mov ea, [ebp]` *Move the value at the address in the ebp into eax*
	- Optionally with offset
		- `[register + offset]`
		- E.g. `mov eax, [rbp-4]`
- More ways exist too!
### Common Patterns

### The Stack
- The top of the stack is the *lowest address* that belongs to the stack
- The RSP (*stack pointer*) always points to the top of the stack
- The `push rax` instruction is equivalent to:
	- `sub rsp, 8`
	- `mov [rsp], rax`
- The `pop rax` instruction is equivalent to:
	- `mov rax, rsp]
	- `add rsp, 8`
	- Note - it does not overwrite the memory!
(images)


### Calling Conventions
There exists a convention on how function arguments should be passed.
- The first 6 integer and pointer arguments should be passed by register (`rdi, rsi, rdx, rcx, r8, r9`).
- Any further argument is passed on the stack
- Result is normally passed in `rax`

- Want to be able to pass a structure (but in libc) often can only return a pointer to a structure :(

### Stack frame (Linux)
- A function will usually first save the previous base pointer (`rbp`)
	- Then, it will set the `rbp` to the current stack pointer `rsp`
- Before returning, it will cleanup the stack and restore the old `rbp`.
