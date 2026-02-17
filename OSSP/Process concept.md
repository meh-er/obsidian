---
tags:
  - OSSP
---
How do Users and Processes interact with the Operating System?
- **Users** interact indirectly through a collection of system programs that make up the operating system interface. The interface could be:
	- A GUI, with icons etc
	- A command-line interface for running processes and scripts, browsing files in directories etc
	- Or. non-interactive batch system that takes a collection of jobs
- **Processes** interact by making *system calls* into the operating system proper (i.e., the *kernel*)

Typically, operating systems will offer the following services to processes:
- **Program execution**: The system must be able to load a program into memory and to run that program, end execution, either normally or abnormally (indicating error)
- **I/O operations**: A running program may require I/O, which may involve a file or an I/O device
- **File-system manipulation**: Programs need to read and write files and directories, create and delete them, search the, list file information, and do permission management
- **Interprocess Communication (IPC)**: Allowing processes to share data through message passing or shared memory.

Typically, operating systems will offer the following internal services:
- **Error handling**: what if our process attempts a divide by zero or tries to access a protected region of memory, or if a device fails?
- **Resource allocation**: Processes may compete for resources such as the CPU, memory, and I/O devices.
- **Accounting**: e.g. how much disk space is this or that user using? How much network bandwidth are we using?
- **Protection and Security**: The owners of information stored in a multi-user or networked computer system may want to control use of that information, and concurrent processes should not interfere with each other.
![[Pasted image 20260217131544.png]]