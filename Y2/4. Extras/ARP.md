Address resolution protocol (ARP) is a protocol or procedure that connects an ever-changing IP address to a physical machine address, also known as a media access control ([[MAC]]) address, in a LAN.

This mapping procedure is important because IP address and MAC addresses have different lengths, and a translation is needed so that the systems can recognise one another. MAC addresses are 48 bits long.

When a new computer joins a LAN, it will receive a unique IP address to use for identification and communication. 

Packets of data arrive at a gateway, destined fro a particular host machine. The gateway, or piece of the hardware on a network that allows data to flow from one network to another, asks the ARP program to find a MAC address that matches the IP address. The ARP cache keeps a list of each IP address and its matching MAC address. The ARP cache is dynamic, but users on a network can also configure a **static ARP table** containing this info.

Every time a device requests a MAC address to send data to another device connected to the LAN, the device verifies its ARP cache to see if the connection has been completed. If it exists, a new request is unnecessary. However if the translation has not yet been carried out, then the request for network addresses is sent, and ARP is performed.