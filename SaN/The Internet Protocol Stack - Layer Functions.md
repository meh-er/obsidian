#SaN

### The Internet Protocol Stack - Layer Functions
##### Application Layer
- Web, Email, FTP, DNS
- Handles **user-facing applications
- 'Stuff that you write'

##### Transport Layer
- TCP, UDP
- Manages **end-to-end connections**
- 

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

#### Wireshark Demo: Capturing and Analysing Traffic
##### Why Wireshark matters
- Network analysis helps debug connectivity and security issues
- Attack detection is a key cybersecurity skill
- Wireshark is widely used for investigating suspicious traffic.

#### Understanding the ARP Spoofing Attack
##### What Happened in the Capture?
- The attacker sends fake ARP replies, pretending to be the gateway
- This tricks the victim into sending traffic to the attacker instead
- The attacker can now intercept, modofy, or drop packets

##### How to Detect ARP Spoofing in Wireshark?
- Look for multiple ARP Replies claiming the same IP address
- Verify if the MAC address of the gateway changes unexpectedly
- Use **Wireshark filters**: `arp` or `eth.src != eth.dst`

# Cryptographic Protocols
**nonce** => Number only used once
CODE
{-}$K_{ab}$ means symmetric key encryption
##### Key Establishment Protocol
This protocol was possible because **A** and **B** shared a key.
##### How is a Session Key Set Up?
Often, the principals need to set up a session key using a **Key Establishment Protocol**
##### Ensuring Secure Communication
To be sure they are communicating with the correct principal, they must either:
- Know each other's public keys, or
- Use a **Trusted Third Party (TTP)**
#### The Needham-Schroeder Public Key Protocol
If Alice and Bob know each other's public keys, can they set up a symmetric key?
1. A -> B : $E_B(N_a,A)$
2. B -> A : $E_A(N_a,N_b)$
3. A -> B : $E_B(N_b)$
Public Key Encryption Notation $E_X(~)$ means public key encryption
$N_a$ and $N_b$ can be used to generate a symmetric key.


* Public key is slower
* Use this to show talking with right person --> want to have encryption for a session
* Less data lost/exposed if key is exposed
* Can mutually authenticate via certificates

**Message Guarantees**
- Goals: Alice and Bob are sure they are talking to each other
	- Whoever could know $N_a$ is the person who decrypted the first message.
	- Whoever could know $N_b$ is the person who decrypted the second message.
**Why is this Secure?**
- A and B mutually authenticate each other
- The attack where Elvis intercepts and impersonates Bob is no longer possible
- **Mutual Authentication** - Alice and Bob both verify each other
- **Protection Against MITM** - Attackers cannot impersonate Bob

#### Forward Secrecy
**Definition**
A protocol has **Forward Secrecy** if it keeps the message secret from an attacker who has:
- A recording of the protocol run
- The long-term keys of the principals
##### Why does this matter?
Protection against:
- Governments that can force people to give up their keys
- Hackers that might steal private keys

###### Why is this Secure?
- x,y, $g^{xy}$ are not stored after the protocol run
- A and B's keys don't let the attacker read M
- Station to Station Protocol ensures **Forward Secrecy**
#### Certificates: Verifying Public Keys
**The Problem**
What if Alice and Bob don't know each other's public keys to start with?
**Possible Solutions**
- Meet face-to-face and securely exchange keys
- Use a pre-shared key mechanism
**Trusted Third Party (TTP)** A TTP can sign identities and public keys, creating:
***A Certificate***

#### Full Station-to-Station Protocol
**Why Add Certificates?**
- The 'full' STS protocol includes certificates for A and B.
- Certificates contain public keys signed by a Trusted Third Party (TTP)
- Alice and Bob don't need to know each other's public key beforehand

#### The Needham-Schroeder Key Establishment Protocol
**How it Works**
- S is a Trusted Third Party (TTP) that helps establish a shared key $K_{ab}$
- S encrypts the session key separately for Alice and Bob
- Alice and Bob mutually authenticate using nonces $N_a$ and $N_b$
- Ensures that only Alice and Bob know $K_{ab}$
#### Some Key Establishment Goals
**Key Freshness**
The key established is new (either from a trusted third party or because it uses a new nonce)
**Key Exclusivity**
The key is only known to the principals in the protocol.
**Good Key**
A good key is both fresh and exclusive.

#### Authentication Goals
##### Far-end Operative: 
A knows that B is currently active
For instance, B might have signed a nonce generated by A, e.g.
- A -> B: $N_a$
- B -> A: $S_B(N_a)$
Not enough on its own (e.g. Needham-Schroeder protocol)
##### Once Authentication: 
A knows that B wishes to communicate with A.
For instance, B might have the name A in the message, e.g.
- B -> A: $S_B(A)$
Both of these together give:
##### Entity Authentication
A knows that B is currently active *and* wants to communicate with A.
e.g.
- A -> B: $N_a$
- B -> A: $S_B(A,N_a)$

##### The Highest Goal
A protocol provides Mutual Belief in a key **K** for Alice with respect to Bob if, after running the protocol, Bob can be sure that:
- K is a good key with A
- Alice can be sure that Bob wishes to communicate with Alice using K
- Alice knows that Bob believes that K is a good key for B

#### Conclusion
- Secure communication relies on key establishment protocols
- Mutual authentication ensures both parties are who they claim to be
- Forward secrecy prevents past communications from being decrypted if long-term keys are compromised.
- Certificates help verify identities using a trusted third part (TTP)
- The ultimate goal is **Mutual Belief in a Key** - ensuring both Alice and Bob trust the established key and each other.

