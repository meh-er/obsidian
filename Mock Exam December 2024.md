## Q1 
### (a)  What is the difference between call-by-value and call-by-reference?
Call-by-Value: Creates a new copy of the value in memory to modify, meaning that the original value stays in memory untouched. In c this is normally done as variables.
Call-by-Reference: Uses the original value, taken from the reference to it's memory address, and modifies it directly. In C this is done with pointers.

### (b) Give two possible consequences of an access beyond the boundaries of an array in a C program
1. Can throw an error/exception in the program - cannot continue because of the error as it does not exist
2. Can overwrite whatever is stored in stack memory next.

### (c) The intention is that the function addElem has a list allItems, a title ID newID and a title newTitle as arguments and adds a new element consisting of the ID and the title to the list. You may assume that the list is ordered by the title ID when the function is called. You may assume that newTitle points to a properly null-terminated string of arbitrary length. The list which is returned by addElem should also be ordered by titleID. 
### The function deleteAllItems should delete the list and all titles stored in the list. This code compiles correctly, but does not work as intended. List the errors (including memory management) and provide corrections. Do not list or provide corrections for concurrency errors.

- strcpy does not take in the size of newTitle, so if it is longer than BUFFERLENGTH will overwrite whatever is below it.
- prevItem -> next = &newItem but &newItem is a local variable so this pointer will return nothing once the function is closed?
- frees items but then tries to use items afterwards - illegal! use after free!
- does not account for if currentItem == NULL, would crash in that case
- prevItem is updated but the while loop does not progress on, currentItem is never moved to next

# Q2
## (a) What is a context switch? Why is it important for the OS to minimise the number of context switches? `[4]`
A context switch occurs when the OS changes the process running. For example, this may be from a user thread to a kernel thread. If many context switches are occuring, then the OS will be unable to actually execute any of the tasks, and this will decrease efficiency, so it must minimise this number.

## (b) A multi-user system used to work well, with low response times and good throughput. Now many users use a package for automatic program verification, and as a result the response time is high, and throughput low. How would you distinguish between overloaded CPU, thrashing and overused disk  as a possible reason? `[4]`
- CPU overloading: occurs when there are many processes being executed at one time and the CPU cannot be executing them all at once so is overloaded. This would be caused by too many processes at a time and not have a high response time, which
- 