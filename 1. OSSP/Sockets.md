---
tags:
  - OSSP
---
## Sockets
A socket behaves similar to a file (Can read/write) once connected. A **client** connects to a **server** (usually TCP or UDP)

```
#include <sys/socket.h>
...
int sockfd = socket(AF_INET6, SOCK_STREAM, 0);
...
```
From there, server and client start to differ
Server binds to port, listens on the socket, and accepts each client connection
```
bond(sockfd, &srv_struct, len)
listen(sockfd, backlog)
newsockfd = accept(sockfd, &cl_struct, len);
```
Now can read() and write() on newsockfd and close() later

Client connects to IP/port, and then read() and write() on socket
```
connect(sockfd, &addr_Struct, len)
write(sockfd, buffer, len)
...
close(sockfd)
```
Same as server regarding read/write/close


![[Pasted image 20260215192153.png]]

## Multicore Systems

![[Pasted image 20260215192347.png]]
![[Pasted image 20260215192504.png]]

- 'Coherence' is the quality of being logical and consistent. During program execution, data must remain coherent.
- On a multicore system, a data variable may reside in multiple caches and might get updated 'locally' by its local core
	- This causes coherence problem, and protocols are needed (not going into detail here)
#### Programming multicore platforms
- Option 1: program directly targeting processor cores
	- Programmer takes care of synchronization
	- painful and error-prone
-  Option 2: Use a **concurrency platform***
	- It abstracts processor cores, handling synchronization and communication protocols, and performs load balancing.
	- Hence offers much easier multicore programming environment
	- Examples:
		- **Pthreads** and WinAPI threads
		- OpenMP