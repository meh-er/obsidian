---
tags:
  - OSSP
---
- A virtual machine allows to run one operating system (the guest) on another operating system (the host)
- A virtual machine provides an interface interface identical to the underlying bare hardware
- The operating system host creates the illustion that a process has its own processor and (virtual memory)
- Each guest is provided with a (virtual) copy of underlying computer, so it is possible to install, e.g. Windows 10 as a guest OS on Linux.

![[Pasted image 20260217141026.png]]

- Useful for development, testing, especially OS development, where it is trivial to revert an accidentally destroyed OS back to a previous stable snapshot.
- Multiple execution environments can share same hardware

### Para-virtualisation
- Presents guest with system similar but not identical to hardware
- guest OS must be modified to run on paravirtualized 'hardware'
	- e.g. the kernel is recompiled with all code that uses privileged instructions replaced by hooks into the virtualization layer
	- After an OS has been successfully modified, para-virtualization is very efficient, and is often used for providing low-cost rented Internet servers

### VMWare Architecture
- VMWare implements full virtualisation, such that guest OS do not require modification to run upon the virtualised machine.
- The virtual machine and guest OS run as a user-mode process on the host operating system.
- As such, the VM must get around some tricky problems to convince the guest OS that it is running in privileged CPU mode when it is not.
	- Consider a scenario where a process of the guestOS raises a divide-by-zero error.
	-  Without special intervention, this would cause the host OS immediately to halt the virtual machine process rather than the just offending process of the guest OS.
	- So VMWare must look out for troublesome instructions and replace them at run-time with alternatives that achieve the same effect within user space, albeit with less efficiency
	- But since usually these instructions occur only occasionally, many instructions of the guest OS can run  unmodified on the host CPU.

