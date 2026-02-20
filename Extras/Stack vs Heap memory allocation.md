Stack allocation
- assigning memory for local variables and function calls in the call stack
- Freed immediately when the function ends
- Fast, efficient but has limited space
- If too many function calls exceed stack's capacity, results in stack overflow error

How Stack Allocation Works:
- Memory is allocated in **contiguous blocks** within the **call stack**.
- The size of memory required is **already known** before execution.
- When a **function is called**, its **local variables** are allocated on the stack.
- Once the function **finishes execution**, the allocated memory is **automatically freed**.
- The programmer **does not** need to handle allocation or deallocation.
- Since stack memory is freed when a function completes, it is also called **temporary memory allocation**.
