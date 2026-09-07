## Stack allocation
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

Key Features of Stack Allocation
- Memory is available **only while the function is running**
- **Automatic deallocation** occurs when the function ends
- If the **stack memory is full**, an error like **Java.lang.StackOverflowError** occurs in Java, and segmentation fault in C++
- **Safer** than heap memory as data can only be accessed by the **owner thread**.
- **Faster** than heap memory due to automatic memory management.

## Heap Allocation
- Allocated **dynamically** during program execution. Unlike **stack**, it is **not freed automatically**, requires **manual deallocation (in C/C++)**
- Whenever an **object** is created, it is stored in **heap memory**, while references to these objects are stored in **stack memory**.
- Less safe than stack because it is **accessible by multiple threads**, increasing the risk of **data corruption** and **memory leaks** if not handled properly

Key Features of Heap Allocation
-  If heap memory is **full**, JVM throuws an error: **java.lang.OutOfMemoryError**
- **Automatic Deallocation** does not happen, a **garbage collector** is needed to free unused memory
- **Slower** than stack memory due to **manual allocation**
- Less **thread-safe**
- Typically **larger in size** compared to stack memory
- Heap memory **persists** as long as the entire application is running

