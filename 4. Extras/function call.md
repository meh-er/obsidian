#Theory 

Before executing a function, a program pushes all of the parameters for the function onto the [[stack]] in the reverse order that they are documented. Then the program issues a `call` instruction indicating which function it wishes to start. The `call` instruction does two things:
1. First it pushes the address of the next instruction, which is the return address, onto the [[stack]].
2. Then, it modifies the [[instruction pointer]] to point to the start of the function.


When you call a function, you should assume that everything currently in your registers will be wiped out. The only register that is guaranteed to be left with the value it started with is ebp. This, if there are registers you want to save before calling a function, you need to save them by pushing them on the [[stack]] before pushing the function's parameters.
