#Theory 

# Stack allocation
- Assigning memory for local variables and function calls in the call stack
- Freed immediately when the function ends
- Fast, efficient, but has limited space
- If too many function calls exceed stack's capacity, results in stack overflow error

How Stack Allocation Works:
- Memory is allocated in **contiguous blocks** with the **call stack**
- The size of memory required is **already known** before execution
- When a **function is called**, its **local variables** are allocated on the stack.
- Once the function **finishes execution**, the allocated memory is **automatically freed**.
- Since the programmer **does not** need to handle or deallocation
- Since stack memory is freed when a function completes, it is also called **temporary memory allocation**.

Key Features of Stack Allocation
- Memory is available **only while the function is running**
- **Automatic deallocation** occurs when the function ends
- If the **stack memory is full**, an error like **Java.lang.StackOverflowError** occurs in Java, and segmentation fault in C++
- **Safer** than heap memory as data can only be accessed by the **owner thread**.
- **Faster** than heap memory due to automatic memory management.