1. Kernel mode is a privileged mode, so processes being executed in kernel mode means that they have privileged, administrative access to the whole OS. Most processes will be executed in the user mode, which is safer (an attacker cannot get very far exploiting this)
2. .
	- Clear memory
	- Turn off intrrupts
	- Modify entries in device-status table.
	- Access I/O device
3. Memory leaks in the kernel can lead to the whole system becoming corrupted.
4. If interrupt service routine takes a long amt of time,w ill cause a long wait with the whole system :( big sad bro
5. Users would have privileged access, easy to attack, 