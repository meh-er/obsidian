---
tags:
  - OSSP
---
# System calls
- Programming interface to the services provided by the OS
- typically written in a high-level language (C, C++)
- Mostly accessed by programs via a high-level Application Program Interface (API) rather than direct system call
- Examples: Win32 for WIndows, POSIX APi for UNIX-based systems (including Linux, MacOS X)
- Why use APIs?
	- Since system calls result in execution of privileged [[kernel]] code, and since it would be crazy to let the user process switch the CPU to groveled mode, we must make used of the low-level hardware trap instruction
	- The user process runs the trap instruction, which will switch CPU to privileged mode and jump to a kernel pre-defined address of a generic system call function, hence the transition is controlled by the kernel.
	- Also, APIs can allow for backward compatibility if system calls change with the release of a OSS
![[Pasted image 20260217133150.png]]

![[Pasted image 20260217133208.png]]

#### Systems calls for file operations
Have the following operations for files:
	`open` Register the file with the operating system. must be called before any operation on the file. Returns an integer called the file descriptor - an index into the list of open files maintained by the OS.
	`read` Read data from the file. Returns number of bytes read or 0 for end of file.
	`write` Write data to a file. Returns number of bytes written.
	`close` De-registers the file with the operating system. No further operations on the file are possible.
These system calls return a negative number on error. Can use `perror` function to display error.


