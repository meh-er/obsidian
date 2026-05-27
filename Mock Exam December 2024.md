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
- delete frees but that has never been mallocated?
- 
