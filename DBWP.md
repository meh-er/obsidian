#DAWP 

## Week 7
### Ex 1: NIC
Questions: 
- What is your device's local IP address?
- Can you identify which network interface is used for internet connectivity>
- Is your IP address IPv4 or IPv6?

Input: `ip addr show`

Output:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
3: wlo1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether dc:90:09:90:56:73 brd ff:ff:ff:ff:ff:ff
    altname wlp0s20f3
    inet 172.22.154.244/16 brd 172.22.255.255 scope global dynamic noprefixroute wlo1
       valid_lft 41645sec preferred_lft 41645sec
    inet6 fe80::1e18:3d3d:f814:89a6/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```

Analysis:
- Local IP address is located in wlo1: inet: `172.22.154.244` or IPv6 address  (link local)`inetfe80:1e18:3d3d:f814:89a6`
- The network interface used is `wlo1`
- My IP address is both, but IPV4 for non local

### Ex 2 DNS
- What IP addresses does google.com.  resolve to?
- What differences do you notice between nslookup and dig?
- Why might a website have multiple IP addresses?

Input: `nslookup google.com`
Input: `nslookup 8.8.8.8`
Input `dig google.com`

Output:
```
Non-authoritative answer:
Name:	google.com
Address: 142.250.140.100
Name:	google.com
Address: 142.250.140.113
Name:	google.com
Address: 142.250.140.101
Name:	google.com
Address: 142.250.140.138
Name:	google.com
Address: 142.250.140.102
Name:	google.com
Address: 142.250.140.139
Name:	google.com
Address: 2a00:1450:4009:c0b::8a
Name:	google.com
Address: 2a00:1450:4009:c0b::66
Name:	google.com
Address: 2a00:1450:4009:c0b::8b
Name:	google.com
Address: 2a00:1450:4009:c0b::71

```


Output:
```
8.8.8.8.in-addr.arpa	name = dns.google.

Authoritative answers can be found from:

```

Output:
```
; <<>> DiG 9.18.39-0ubuntu0.24.04.3-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 51034
;; flags: qr rd ra; QUERY: 1, ANSWER: 6, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;google.com.			IN	A

;; ANSWER SECTION:
google.com.		77	IN	A	142.250.140.100
google.com.		77	IN	A	142.250.140.101
google.com.		77	IN	A	142.250.140.138
google.com.		77	IN	A	142.250.140.139
google.com.		77	IN	A	142.250.140.102
google.com.		77	IN	A	142.250.140.113

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Thu Apr 30 16:45:28 BST 2026
;; MSG SIZE  rcvd: 135

```

Answer:
- 142.250.140.100
- Dig has query time + more depth instead of just IP addresses, 'digs' for more info
- Multiple domains? 

### Ex 3: Network Connectivity
- What is the average response time to google.com?
- Does packet loss indicate network problems?
- Why might response times vary between different websites

Input: `ping google.com`
Input: `ping -c 5 google.com`

Output:
```
64 bytes from wj-in-f113.1e100.net (142.250.140.113): icmp_seq=1 ttl=112 time=9.44 ms
64 bytes from wj-in-f113.1e100.net (142.250.140.113): icmp_seq=2 ttl=112 time=12.6 ms
64 bytes from wj-in-f113.1e100.net (142.250.140.113): icmp_seq=3 ttl=112 time=11.3 ms
64 bytes from wj-in-f113.1e100.net (142.250.140.113): icmp_seq=4 ttl=112 time=10.3 ms
64 bytes from wj-in-f113.1e100.net (142.250.140.113): icmp_seq=5 ttl=112 time=10.7 ms
```

Answer:
- 7.959ms
- Yes 
- Different physical distance to server?

### Ex 4: Rest APIs
- What data format do these APIs return?
- How can you modify the curl commands to get other data?
- Find another useful RESTful API and use curl on it

Input: `curl https://pokeapi.com/api/v2/pokemon/ditto`
Input: `curl "https://api.agify.io?name=madasar"`
Input: `curl https://www.boredapi.com/api/activity`
Input: `curl https://restcountries.com/v3.1/name/uk`
