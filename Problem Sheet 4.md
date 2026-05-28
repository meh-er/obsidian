1. Threads are used as the smallest measurement of a process. A program can be made up of more than one threads, and each one has 

2. Shared: Global variables, data in the heap, open files
3. A critical section is a section of a program that executes code that changes the state of data/memory. Because it is state changing, it needs to be uninterrupted, as another process should not be able to access it while the state is changing. If another process interrupts, it could potentially read old data that has been overwritten, or overwrite data itself.
4. Critical