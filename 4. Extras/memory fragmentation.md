#Theory 

Fragmented memory describes all of a system's unusable free memory. 
These resources remain unused because the memory allocator responsible for allocating them cannot make the memory available.
This problem occurs because free memory is scattered at separate locations in small, discontinuous portions. 
Because the allocation method determines whether memory  fragmentation becomes a problem, the memory allocator plays the central role in ensuring the availability of free resources.

When the [[compiler]] and the linker perform the memory-allocation function, memory fragmentation does not occur, because the compiler understands the data lifetime. 
Having the data lifetime available offers the advantage of making the data stackable in a LIFO arrangement. 
This fact makes it possible for the memory allocator to work efficiently and without fragmentation. 
Generally, memory allocation performed during runtime is not stackable. 
Memory allocations are independent in time, which makes the fragmentation problem difficult to resolve.