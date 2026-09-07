#Theory 

The Instruction Pointer (EIP) is a 32-bit register that **points to the memory address of the next instruction to be executed**. It is the 'brain' of program flow dictating where the CPU fetches instructions from.

EIP is automatically incremented after each instruction (e.g., after executing `mov eax, ebx`, EIP points to the next instruction). However it can also be manually modified by control-flow instructions like `jmp`, `call`, and `ret`

The return address pushed by `call` is critical for returning control to the caller.
For example:
- `main()` calls `func()`: `call func` pushes `main`'s next instruction address onto the stack.
- `func()` executes, then `ret` pops this address into EIP, so `main()` resumes.