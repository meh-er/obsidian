---
tags:
  - OSSP
---
- Function: main permanent data storage. **Speed bottleneck!**
- **Capacity not problem** nowadays: 2TB disks even for PC. But **backup becoming a problem**
- Logical view (view of programmer): **tree structure of files** together with read/write operation and creation of directories
- Physical view: **sequence of blocks**, which can be read and written. OS has to map logical view to physical view, mist impose tree structure and assign blocks for each file

Two main possibilities to realize filesystem:
- **Linked list**: Each block contains pointer to next 
	=> Problem: random access (`seek()`) costly: have to go through whole file until desired position.
- **Indexed allocation**: Store pointers in one location: so-called index block (similar to page table). To cope with vastly differing file sizes, may introduce **indirect index blocks**.
Index blocks are called `inodes` in Unix.
Inodes store additional information about the file (e.g. size, permissions)

### Caching
Disk blocks used for storing directories or recently used files cached in main memory
Blocks periodically written to disk
=> Big efficiency gain
**Inconsistency arises when system crashes**
Reason why computers must be shutdown properly

### Journaling File Systems
To minimise data loss at system crashes, ideas from databases are used:
	- Define **Transaction pointers**: points where cache is written to disk
	=> Have consistent state
	- Keep log-file for each write-operation
	Log enough information to unravel any changes done after latest transaction point.

