#Theory 

DNS spoofing is a form of hacking where DNS data is introduced to the DNS resolver's cache, causing the name server to return an incorrect result record, e.g. an IP address. This results in traffic being diverted to any computer that the attacker chooses.

e.g. the attacker exploits flaws in [[DNS]] software. The server should correctly validate [[DNS]] responses to ensure that they are from an authoritative source otherwise the server might end up caching incorrect entries locally and serve them to other users.

An attacker spoofs the IP address DNS entries for a target website, on a given DNS server, and replaces them with the IP address of a sever under their control.