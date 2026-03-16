---
tags:
  - OSSP
---
Program's view memory is set of memory cells starting at address 0x0 and finishing at some value (logical address).
Hardware: have set of memory cells starting at address 0x0 and finishing at some value (physical address)

Want to be able to store memory of several programs in main memory at the same time. Therefore, we need suitable **mapping from logical addersses to physical addresses**
- At Compile Time: absolute references are generated
- At load time: can be done by special program
- At execution time: needs HW support

Address mapping can be taken one step further: dynamic linking: use only one copy of system library. but the OS has to help: same code is accessible to more than one [[process]].

### Swapping
Swapping is a memory management technique where processes are temporarily moved between main memory and secondary storage to free up memory for other processes.
If memory demand is too high, memory of some [[process]] is transferred to **disk**.  This is usually combined with [[0Scheduling processes]]; as low priority processes are swapped out.
- Allows multiple processes to run efficiently.
- Lower-priority processes can be swapped out for higher-priority ones.
- Swapped-out processes resume when loaded back into memory.
- Transfer time depends on the amount of data moved.

Disadvantages
- Big transfer time
### Fragmentation
Swapping raises problems:
- Over time, many **small holes** appear in memory (external fragmentation)
- Programs only a little smaller than hole => leftover too small to qualify as hole (internal fragmentation)
- Fragmentation occurs when processes are loaded into and removed from memory, resulting in **unused memory spaces** that cannot be efficiently utilised.
- **Internal Fragmentation**: Occurs when a [[process]] is allocated more memory than it actually needs leading to wasted space inside the allocated memory block.
- **External Fragmentation**: Occurs when free memory is divided into small, scattered blocks, making it impossible to allocate a large contiguous block even though enough total free memory exists.

Strategies for choosing holes:
- **First fit**: Allocates the first available partition large enough to hold the [[process]].
- **Best fit**: Allocates the smallest available partition that fits the [[process]], reducing wasted space.
- Rotating first fit: Allocates after last assigned part of memory.
- Buddy system: Have holes in sizes power of 2. Smallest possible hole used. Split hole in two if necessary. Recombine two adjacent holes of same size.

- Next Fit: Similar to First Fit but starts searching for free memory from the point of the last allocation.

### Thrashing
Thrashing occurs when the system spends most of its time swapping pages between memory and disk **instead of executing the process**, causing very low CPU utilization.

If **process lacks frames it uses constantly**, page-fault rate very high.
=> CPU-throughput decreases dramatically
=> Disastrous effect on performance

Solutions
1) Working set model (based on locality)
	- Define working set as set of pages used in the most recent page references
	- Keep only working set in main memory
	=> Achieves high CPU-utilisation and prevents thrashing.
	Determining the working set:
	- Approximation - use reference bits, copy them each 10,000 references and define working set as pages with reference bit set.
2) Page-Fault Frequency: takes a direct approach
	- Give process additional frames if page frequency rate is high
	- Remove frame from process if page fault rate low



### Paging
Alternative approach: Assign **memory of a fixed size** (page) => avoids external fragmentation.
Translation of logical addresses to physical address is done via a **page table**.

**Hardware support mandatory** for paging:
If page table **small**, use **fast registers**. Store large page tables in main memory, but **cache most recently used entries**.

**Instance of a general principle**
Whenever **large lookup** tables are required, use **[[cache]]** (small but fast storage) to store most recently used entries.

**Memory protection easily added** to paging: protection information stored in page table.

### Segmentation
Idea: **Divide memory according to its usage** by programs:
- Data: **mutable, different** for each instance
- Program Code: **immutable, same** for each instance
- Symbol Table: **immutable, same** for each instance. **only necessary for debugging**.

Requires again HW support - can use same principle as for **paging**, but have to do overflow check.
Paging motivated by ease of allocation, segmentation by use o f memory (combination works well)

## Virtual memory
Idea: complete **separation of logical and physical memory** => Program can have extremely large amount of [[virtual memory]] - works because most programs use only small fraction of memory intensively

**Efficient implementation tricky**
Reason - enormous difference between:
- Memory access speed 
- Disk access speed

### Demand Paging
Virtual memory implemented as demand paging: memory divided into **units of same length** (pages), together with valid/invalid bit

Two strategic decisions to be made:
- Which process to 'swap out' (move whole memory disk and block process): swapper
- Which pages to move to disk when additional page is required: pager

**Minimisation of rate of page faults** (page has to be fetched from memory) **crucial**

If we want 10% slowdown due to page fault, require fault rate $p < 10^{-6}$ for HDD and $p <10^{-4}$ for SDD.

### Page replacement algorithms
1. **FIFO** 
	- easy to implement.
	- Does not take locality into accoun
	- Increase in number of frames can cause increase in number of page faults
2. **Optimal algorithm**
	- Select page which will be re-used at the latest time (or not at all) => not implementable, but good for comparisons
3. **Least-recently used:**
	- Uses past as guide for future and replaces page which has been unused for the longest time.
	- Requires a lot of HW support
	
### Page caches
Experience shows: have repeated cycles of allocation and freeing same kind of objects
- Can have pool of pages used as cache for these objects (so-called slab [[cache]])
- Cache maintained by application (e.g. file system)
- `kmalloc` uses slab caches for commonly used sizes