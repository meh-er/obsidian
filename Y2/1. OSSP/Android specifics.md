---
tags:
  - OSSP
---
### Application distributed as bytecode
Android apps (bundled as APK) usually contain only bytecode but no native code.
- Byte code is compiled to native code:
	- At the applications install time
	- Or at the start of the application
- Shipping applications with native code is still supported

### Security enhancements
- Assign a separate user id to each app
- Force all data exchange between apps to go via binder, with fine-grained access control mechanisms
- For system services running as root use selinux-kernel extensions, which specify which file can be accessed by which process.
- => Vulnerabilities in system services do not immediately lead to full access

### Binder
- Android uses RPCs very frequently
- Add new RPC mechanism called binder to kernel
- Copies directly from user space of writer to user space of reader
- Integrates capability mechanism into RPC
- Use separate thread pool for incoming RPC for system services

### Android-specific changes to the linux kernel
Need to have finer control over which devices are suspended (e.g. music still playing while screen turned off)
Android added wakelocks to kernel
- Kernel is set to suspend as soon and as often as possible
- Drivers need to actively prevent system from suspending device (and therefore, kernel)
- Have several wakelocks, which combination of CPU, screen and keyboard awake
Using wakelocks properly is crucial to achieve long battery life


### Alarm timers
Standard linux kernel timers not sufficient for advanced power management
Android introduces alarm timers:
- Alarm timers wake up particular process even if system is suspended
- Application will grab wakelock once woken up

### New life cycle management
- On a traditional Linux system, apps are started and terminated explicitly
- Android uses a different approach:
	- Apps are started when requested by the user
	- Alternatively when a message is sent to the application
- When the system is low on memory, apps are killed
- Apps are responsible to persist/ load their state whenever required

### Network security
- Linux kernel allows any process to open socket and initiate network communication
- Android introduces network permission, filtered by group id
- Permission needed to access IP, Bluetooth or raw sockets