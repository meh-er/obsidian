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
- **Physical dependencies** between devices.