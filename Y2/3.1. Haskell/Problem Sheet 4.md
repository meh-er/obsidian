1. Threads are used as the smallest measurement of a process. A program can be made up of more than one threads, and each one has 

2. **Shared: Global variables, data in the heap, open files**
3. A critical section is a section of a program that executes code that changes the state of data/memory. Because it is state changing, it needs to be uninterrupted, as another process should not be able to access it while the state is changing. If another process interrupts, it could potentially read old data that has been overwritten, or overwrite data itself.
		**A piece of code where switching between threads must be limited to ensure correct execution of the program**
4. Critical sections need to take as little time as possible so that other processes can also execute their critical sections without causing waiting.
	**Other threads may have to wait and cannot do any useful work while one thread executes a critical section. You want to keep this waiting time as short as possible**.
5. If a thread blocks during execution of a critical section, the critical section may not be able to complete, meaning that no other process waiting to enter their critical section will be able to complete, causing a complete stop in all activity.
6. fun1
	```
	isExecuted++;
	**totalCalls++;**
	result = malloc(5)
	return result;
	```
fun2
```
isExecuted++;
**totalCalls++;**
result = malloc(10)
return result;
```

7. You could protect this by using a mutex so that only one process can access the critical section at a time. Use a condition variable so if one process is in a critical section, the other can't be.
8. fun1
```
[critical section]
read_write_lock(&lock){
msg = NULL
} read_write_unlock(&lock)
```
fun2
```
[critical section]
mutex(&lock)
result = malloc(6);
strcpy(result,msg);
return result;
}
```