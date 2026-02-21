#Theory 

Stack is one of the segments of application memory that is used to store the local variables, function calls, of the function. 
The [[stack]] memory is used to save the parameters passed to your program, allocate memory for local variables, and store the program's execution context.

Since the memory for the [[stack]] is reserved by the OS at the start of execution, you don't need to call the OS every time you allocate something. Instead, your code simply updates the memory address pointed to by the **top of the stack** and continues execution. 

The collection of saved data is called a Stack Frame. Each time a function is called, a new stack frame is created, and when the function finishes, the reverse process occurs, restoring the previous execution context.