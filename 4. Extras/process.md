#Theory 

- A program under execution.
- Programs dispatched from ready state --> scheduled is CPU for execution.
- Takes more time to terminate
- Independent of separate memory, efficient allocates
- Context switching reduces system speed.

### Process Concept
- An [[operating system]] executed a variety of programs:
	- Batch system - jobs
	- Time-shared systems - user programs or tasks
- Process - a program in execution, process execution must progress in sequential fashion. It includes:
	- Program (text) and program counter (PC)
	- [[Stack]]
	- Data section

### Process States
- As a process executes, it changes state
	- **new**: The process is being created
	- **running**: Instructions are being executed
	- **waiting**: The process is waiting for some event to occur
	- **ready**: The process is waiting to be assigned to a processor
	- **terminated**: The process has finished execution

### Process Control Block
- Information associated with each process, which is stored as various fields within a kernel data structure:
	- Process state
	- Program counter
	- CPU registers
	- CPU scheduling information
	- Memory-management information
	- Accounting information
	- I/O status information

### Process Creation
- Parent process create child processes, which, in turn create other processes, forming a tree of processes
- Generally, process identified and managed via a process identifier (pid)
- Resource sharing
	- Parent and children share all resources
	- Children share subset of parent's resources
	- Parent and child share no resources
- Execution
	- Parent and children execute concurrently
	- Parent waits until children terminate
- UNIX examples
	- `fork` system call creates new process
	- exec system call used after a fork to replace the process' memory space with a new program

### Process Termination
- Process executes last statement and asks the operating system to delete it (exit)
	- Output data from child to parent (via wait)
	- Process' resources are deallocated by operating system
- Parent may terminate execution of children processes (Abort)
	- Child has exceeded allocated resources
	- Task assigned to child is no longer required
	- If parent is exiting
		- Some operating systems do not allow child to continue if its parent terminates - all children terminated (i.e. cascading termination)