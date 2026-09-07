---
tags:
  - OSSP
---
# Operating Systems
Main functions of an Operating System:
**OS as a resource allocator:**
	Manages all resources (e.g. hardware) and decides between conflicting requests for efficient and fair resource use (e.g. accessing disk or other devices)
**OS as a control system**:
	Controls execution of programs to prevent errors and improper use of the computer (e.g. protects one user process from crashing another)

#### Bootstrapping of the OS
- Small bootstrap program is loaded at power-up or reboot
	- Typically stored in ROM or EPROM, generally known as firmware (e.g. BIOS)
- Initializes all aspects of the system (e.g. detects connected devices, checks memory for errors, etc)
- Loads operating system kernel and starts its execution

![[Pasted image 20260215203859.png]]
- One ore more CPUs, device controllers connect through common bus providing access to shared memory
- CPU(s) and devices compete for memory cycles (i.e. to read and write memory addresses)
- I/O devices and the CPU can execute concurrently
- Each device controller (e.g. controller chip) is in charge of a particular device type
- Each device controller has a local buffer (i.e. memory store for general data and/or control registers)
- CPU moves data from/to main memory to/from controller buffers (e.g. write this data to the screen, read coordinates from the mouse, etc)
- I/O is from the device to local buffer of controller
- Device controller informs CPU that is has finished its operation by causing an *interrupt*

**Interrupts**
- Interrupt transfers control to the interrupt service routine generally, through the interrupt vector, which contains the addresses of all the service routines
- Interrupt architecture must save the address of the interrupted instruction so original processing may be resumed
- Incoming interrupts are disabled while another interrupt is being processed to prevent a lost interrupt
- A trap is a software-generated interrupt caused either by an error or a user request
y
**Storage Structure**
- Main memory - only large storage media that the CPU can access directly
- Secondary storage - provides large non-volatile storage capacity
- Important example: magnetic disks - rigid metal or glass platters covered with magnetic recording material
	- Disk surface is logically divided into tracks, which are subdivided into sectors
	- The disk controller determines the logical interaction between the device and the computer
- Today also often flash memory

## OS Architecture
#### UNIX - one big kernel
- Consists of everything below the system-call interface and above the physical hardware
- Provides the file system, CPU scheduling, memory management, and other OS functions; a large number of functions for one level
- Limited to hardware support compiled into the kernel

![[Pasted image 20260217134725.png]]


