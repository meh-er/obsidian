#Theory 

The Domain Name System helps convert human-readable domain names, e.g. google.com to [[IP address]]es so browsers can load Internet resources.
Web browsers interact through Internet Protocol (IP) addresses.

Each device connected to the Internet has a unique IP address which other machines use to find the device. DNS servers eliminate the need for humans to memorize IP addresses.

The process of DNS resolution involves converting a hostname into a computer-friendly IP address. When a user wants to load a webpage, a translation must occur between what a user types into their web browser and the machine friendly address.


There are 4 DNS servers involved in loading a webpage.
- **DNS recursor** - The DNS recursor is a server designed to **receive queries** from client machines through applications such as web browsers. Typically the recursor is then responsible for making additional requests in order to satisfy the client's DNS query.
	- Tracks down the DNS record. Makes a series of requests until it reaches the authoritative DNS nameserver for the requested record (or times out or returns an error if no record is found)
	- [[Caching]] means that this can be short-circuited
- **Root nameserver** - The root server can be thought of like an index in a library that points to different racks of books - typically it serves as a reference to other more specific locations.
- **TLD nameserver** - The top level domain server hosts the last portion of a hostname, e.g. the '.com'
- **Authoritative nameserver** - If thie server has access to the requested record, it will return the IP address for the requested hostname back to the DNS Recursor that made the initial request.
	- The server that actually holds the DNS resource records. 
	- Can satisfy queries from its own data without needing to query another source, as it is the final source of truth.