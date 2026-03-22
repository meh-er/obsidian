---
tags:
  - OSSP
---
### Disk Access
Disk access contains three parts:
- **Seek**: head moves to appropriate track
- **Latency**: correct block is under head
- **Transfer**: data transfer
HDDs: Time necessary for seek and latency dwarfs transfer time 
=> Distribution of data and scheduling algorithms have vital impact on performance for HDDs, less so for SSDs.

### Disk Scheduling Algorithms
**Standard algorithms** apply, adapted to the special situation:
1) **FCFS**: easiest to implement, but: may require lots of head movements
2) **Shortest Seek Time First**: Select job with minimal head movement
	Problems:
	- May cause starvation
	- Tracks in the middle of disk preferred
	Algorithm does not minimise number of head movements
3) **SCAN-scheduling**: Head continuously scans the disk form end to end (lift strategy)
	=> solves the fairness and starvation problem of SSTF
	Improvement: **LOOK-scheduling**:
		head only moved as far as last request (lift strategy)
Particular tasks may require different disk access algorithms 
Example: Swap pace management
Speed absolutely crucial => different treatment:
- Swap space stored on **separate partition**
- **Indirect access methods not used**
- **Special algorithms used for access of blocks**
	Optimised for speed at the cost of space (e.g. increased internal fragmentation)
### Linux Implementation
Interoperability with Windows and Mac requires support of different file systems (eg vfat)
=> Linux implements common interface for all filesystems
Common interface called **virtual file system**
virtual file system maintains
- inodes for files and directories
- caches, in particular for directories
- superblocks for file systems
All systems call (e.g. `open`, `read`, `write` and `close`) first go to virtual file system
If necessary, virtual file system selects appropriate operation from real file system

### Disk Scheduler
Kernel makes it possible to have different schedulers for different file systems
Default scheduler (Completely Fair Queuing) based on lift strategy in addition separate queue for disk requests for each process queues served in Round-Robin fashion
Have in addition No-op scheduler: implements FIFO
Suitable for SSD's where access time for all sectors is equal