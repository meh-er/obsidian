#SaN

### The Internet Protocol Stack - Layer Functions
##### Application Layer
- Web, Email, FTP, DNS
- Handles **user-facing applications

##### Transport Layer
- TCP, UDP
- Manages **end-to-end connections**

##### Internet Layer
- IP, ICMP, Routing
- Routes **packets across networks**

##### Link layer
- Ethernet, Wi-Fi, ARP
- Manages **physical network connections**

### MAC and IP Addresses
##### MAC Address (Media Access Control)
* Unique to each device, assigned by the manufacturer.
* E.g. `48:d7:06:D6:7A:51`

##### IP Address (Internet Protocol)
- Identifies devices **globally** across networks.
- E.g. `147.188.193.15`

##### NAT (Network Address Translation)
- Private IPs (10.`*`.`*`.`*`,192.168.`*`.`*`) are not **unique**
- NAT Enables multiple devices to share a single public IP

### DHCP and ARP: Managing IP Addresses
##### DHCP (Dynamic Host Configuration Protocol)
- Automatically assigns an **IP address** to a machine based on its **MAC address**.
- IP assignments are **temporary** and not stored long-term

##### ARP (Address Resolution Protocol)
- Helps routers map **IP addresses to MAC addresses**.
- Allows devices to **discover** who is using a specific IP

##### ARP Spoofing: Network Attack
- A malicious machine can **impersonate** another by faking ARP responses.
- This can allow **MITM (Man-in-the-Middle** attacks and data interception



#