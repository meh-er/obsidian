#DAWP 

The TCP 3-Way Handshake is a process used by the Transmission Control Protocol (TCP) to establish a reliable connection between a client and a server before data transfer.

### 3-Way Handshake Process
**Step 1 (SYN)**: In the first step, the client wants to establish a connection with a server, so it sends a segment with SYN(Synchronise Sequence Number) which informs the server that the client is likely to start communication and with what sequence number it starts segments with.
**Step 2 (SYN + ACK)**: Server responds to the client request with SYN-ACK signal bts set. Acknowledgements (ACK) signifies the response of the segment it received and SYN signifies with what sequence number it is likely to start the segments with.
**Step 3 (ACK)**: In the final part client acknowledges the response of the server and they both establish a reliable connection with which they will start the actual data transfer.



![[Pasted image 20260408191639.png]]

