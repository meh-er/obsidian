## Q1 
### (a)  What is the difference between call-by-value and call-by-reference? `[4]`
Call-by-Value: Creates a new copy of the value in memory to modify, meaning that the original value stays in memory untouched. In c this is normally done as variables.
Call-by-Reference: Uses the original value, taken from the reference to it's memory address, and modifies it directly. In C this is done with pointers.

### (b) Give two possible consequences of an access beyond the boundaries of an array in a C program `[4]`
1. Can throw an error/exception in the program - cannot continue because of the error as it does not exist
2. Can overwrite whatever is stored in stack memory next.

### (c) The intention is that the function addElem has a list allItems, a title ID newID and a title newTitle as arguments and adds a new element consisting of the ID and the title to the list. You may assume that the list is ordered by the title ID when the function is called. You may assume that newTitle points to a properly null-terminated string of arbitrary length. The list which is returned by addElem should also be ordered by titleID. 
### The function deleteAllItems should delete the list and all titles stored in the list. This code compiles correctly, but does not work as intended. List the errors (including memory management) and provide corrections. Do not list or provide corrections for concurrency errors. `[12]`

- strcpy does not take in the size of newTitle, so if it is longer than BUFFERLENGTH will overwrite whatever is below it.
CORRECTION: use strncpy() which takes in newItem.entry.title, newTitle, size_of(newTitle) and validate that sthe size is less than buffer length before continuing to set newItem.entry.entry_id = newID
- prevItem -> next = &newItem but &newItem is a local variable so this pointer will return nothing once the function is closed?
CORRECTION: unsure
- frees items but then tries to use items afterwards - illegal! use after free!
CORRECTION:
change order: do items = items-> next and then free(items)
- does not account for if currentItem == NULL, would crash in that case
CORRECTION: 
before line 19, add an iff statement that says if currenItem == NULL return, then do the while loop.
- prevItem is updated but the while loop does not progress on, currentItem is never moved to next
CORRECTION:
set prevItem = currentItem 
then set currentItem = currentItem -> next
# Q2
## (a) What is a context switch? Why is it important for the OS to minimise the number of context switches? `[4]`
A context switch occurs when a process is interrupted by a new process that needs to use the CPU immediately, often because of higher priority. As part of this context switch, the old 'context' of the current process is saved, including details such as process id, memory usage, registers, and program counter. These are all stored in an associated PCB for that process. The new process will then be 'restored' if it already existed in a PCB, or be created and use the CPU instead. By saving the context of the old process, the scheduler can switch back to that process later on when the CPU is available. While context switching is important, it is pure overhead and the CPU cannot execute any processes while it is happening, so it is important to keep the number of context switches to as low as possible; our aim is to maximise CPU usage for executing processes.

## (b) A multi-user system used to work well, with low response times and good throughput. Now many users use a package for automatic program verification, and as a result the response time is high, and throughput low. How would you distinguish between overloaded CPU, thrashing and overused disk  as a possible reason? `[4]`
- CPU overloading: occurs when there are many processes being executed at one time and the CPU cannot be executing them all at once so is overloaded. This would be caused by too many processes at a time and not have a high response time, which this system does.
- Thrashing: when too many context switches are happening so the OS can't focus on actually executing processes. This could be the reason here as the OS seems to be receiving all of these automatic program verification requests (response time high) but not managing to execute them (throughput low) as it must be getting interrupted by new automatic program verifications, even from doing other tasks.
- Overused disk: don't know enough about this, but i would assume that when the disk is full/near to full it takes a long time to travel to each next process in order to execute it.
Most likely to be thrashing but would only be able to distinguish between them if you looked at the system itself.

## (c) A webserver for an ecommerce shop is serving several kinds of requests. The first kind consists of rendering large images, which is computationally expensive and can happen in the background. The second kind is a preview of the list of items for sale, which needs to be fast. These preview requests are computationally inexpensive but use lots of I/O. The third kind are purchase requests which are computationally inexpensive and use a moderate amount of I/O. Assume the system is highly loaded.
### (i) Describe the effects of using each of FCFS, Round Robin and priority scheduling strategy in this scenario `[9]`
- render large images, can happen in background, computationally expensive
- preview list of items for sale, fast, inexpensive but use i/o
- purchase requests computationally expensive and use a moderate amount of I/O.

- FCFS: has very bad average waiting time, especially considering that the first process is incredibly large, the others would be required to wait for it to finish before being able to execute at all. This will not be a good solution in this situation, as the second process also specifically needs to be Fast.
- Round Robin: This may be better in this scenario - if we allowed each process to run for a specified amount of time, presumably processes 2 and 3 would finish a lot quicker and process 1, which takes longer, would be able to run interleaved with them. However, this would require a large amount of context switching as both process  2 & 3 will also be switching into waiting mode for the vast amounts of IO used.
- Priority scheduling: Each of the three processes can be assigned a weight and 'age', overtime, meaning that presumably process 2 & 3 are higher priority, they will finish first and then the CPU can just execute process 1 for a long time. However, if process 1 has higher priority than either 2 or 3, this would cause an extremely long wait time for any process after 1, which is not optimal.
### (ii) Which of the three scheduling strategies mentioned in part (i) would you choose for this scenario `[3]`
- I would use Round Robin scheduling, as it seems the most easy to interleave multiple processes, and means that each process gets time spent executing it but does not take over the CPU for a long amount of time, meaning that fast processes can work right after parts of slow processes (process 1)