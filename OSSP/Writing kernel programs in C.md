---
tags:
  - OSSP
---
# kernel
- The user process calls the system call wrapper function from the standard C library
- The wrapper function issues a low-level *trap* instruction (in assembly) to switch from user mode to kernel mode

![[Pasted image 20260217134122.png]]

- To get around the problem that no call can directly be made from user space to a specific function in kernel space:
	- Before issuing the trap instruction, an index is stored in a well known location (e.g. CPU register, the stack, etc)
	- Then, once switched into kernel space, the index is used to look up the desired kernel service function which is then called.
	- Some function calls may take arguments, which may be passed as pointers to structures via registers.
	![[Pasted image 20260217134531.png]]

### Modular Kernel
- Most modern operating systems implement kernel modules
	- Uses object oriented-like approach
	- Each core component is separate
	- Each talks to others over known interfaced
	- Each is loadable as needed within the kernel, so you could download a new device driver for your OS and load it at run-time, or perhaps when a device is plugged in
- Overall, similar to layered architecture but with more flexibility, since all require drivers or kernel functionality need not be compiled into the kernel binary.
- Note that the separation of the modules is still only logical, since all kernel code (including dynamically loaded modules) runs in the same privileged address space (a design now referred to as monolithic), so I could write a module that wipes out the operating system no problem.
	- This leads to the benefits of micro-kernel architecture, which we will look at soon

![[Pasted image 20260217135415.png]]

### Microkernel
- Moves as much as possible from the kernel into less privileged 'user' space (e.g. file system, device drivers, etc)
- Communication takes place between user modules using message passing
	- The device driver for e.g. a hard disk device can run all logic in user space (e.g. decided when to switch on and off the motor, queuing which sectors to read next, etc)
	- But when it needs to talk directly to hardware using privileged I/O port instructions, it must pass a message requesting such to the kernel.
- Benefits:
	- Easier to develop microkernel extensions
	- Easier to port the operating system to new architectures
	- More reliable (less code is running in kernel mode) - if a device driver fails, it can be re-loaded
	- More secure, since kernel is less-complex and therefore less likely to have security holes
	- The system can recover from a failed device driver, which would usually cause 'a blue screen of death' in Windows or a 'kernel panic' in linux
- Drawbacks:
	- Performance overhead of user space to kernel space communication
- Examples
	- Minix OS
	- L3/L4
![[Pasted image 20260217140835.png]]