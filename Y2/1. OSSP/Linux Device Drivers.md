---
tags:
  - OSSP
---
## Device drivers
View from user space:
Have special file in /dev associated with it, together with give system calls:
- `open`: make device available
- `read`: read from device
- `write`: write to device
- `ioctl`: Perform operations on device (optional)
- `close`: Make device available

#### Categorising devices
Kernel also keeps track of
- **Physical dependencies** between devices. Example: devices connected to a USB-hub
- **Buses**: Channels between processor and one or more devices. Can be either physical (e.g. pci, usb), or logical
- **Classes**: Sets of devices of the same type, e.g. keyboards, mice

#### Handling Interrupts in Device Drivers
Normal cycle of interrupt handling for devices:
- Device sends interrupt
- CPU selects appropriate interrupt handler
- Interrupt handler processes interrupt
	Two important tasks to be done:
	- Data to be transferred to/from device
	- Waking up processes which wait for data transfer to be finished
- Interrupt handler clears interrupt bit of device
	Necessary for next interrupt to arrive
Interrupt processing time must as short as possible
Data transfer fast, rest of processing slow
=> Separate interrupt processing in two halves:
- **Top Half** is called directly by interrupt handler
	Only transfers data between device and appropriate kernel buffer and schedules software interrupt to start
- **Bottom half** still runs in interrupt context and does the rest of the processing (e.g.  working through the protocol stack, and waking up processes)