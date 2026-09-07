#Theory 

A heap overflow is a type of buffer overflow that occurs in the [[heap]] data area. Heap overflows are exploitable in a different manner to that of [[stack]] based overflow. Memory on the [[heap]] is dynamically allocated at runtime and typically contains program data. Exploitation is performed by corrupting this data in specific ways to cause the application to overwrite internal structures such as linked list pointers. 
The canonical heap overflow technique overwrites dynamic memory allocation linkage (such as `malloc` metadata) and uses the resulting pointer exchange to overwrite a program function pointer.

An accidental overflow may result in data corruption or unexpected behaviour by any [[process]] that accesses the affected memory area. On OS without memory protection, this could be any [[process]] on the system.