#SaN 

# SSL/TLS
- Secure Sockets Layer (SSL) protocol was renamed to Transport Layer Security (TLS)
- Provides encrypted communication and authentication using public keys
##### Encryption and Authentication
- SSL/TLS supports various cryptographic algorithms
	- RSA (Rivest-Shamir-Adleman)
	- DES (Data Encryption Standard)
	- DH (Diffie-Hellman Key Exchange)
- The specific cipher suite is negotiated at the start of the session.

#### X.509 Standard for Certificates
- X.509 certificates contain:
	- Subject (entity identity)
	- Subject's public key
	- Issuer's name
**Verification Process**
- The issuer signs the hash of all the certificate data.
- To verify a certificate:
	- Compute the hash of the data
	- Check the signature using the issuer's public key.
- If I trust the issuer's public key, I can trust the subject's public key

#### The Internet Protocol with TLS
The TLS layer runs between the Application and Transport layer
The encryption is transparent to the Application layer
Normal TCP and IP protocols etc. can be used at the low layers

#### The TLS Protocol
**TLS Handshake: Establishing a Secure Connection**
1. C -> S: ClientHello (Supported ciphers, random nonce)
2. S -> C: ServerHello (Chosen cipher, random nonce)
3. S -> C: Certificate (Server's public key signed by CA)
4. C -> S: Key Exchange (Pre-master secret encrypted with Server's public key)
5. C -> S: Finished (Client's verification message)
6. S -> C: Finished (Server's verification message)

**Key Exchange Options**
- RSA: Client encrypts pre-master secret with server's public key
- Diffie-Hellman: Client and server derive a shared secret
After the handshake, all communication is encrypted using the negotiated symmetric key.

TLS Handshake Steps
1. $C -> S : N_C$
2. $S -> C : N_S, Cert_S$
3. $C -> S : E_S(K_{seed}),({Hash_1})K_{CS}$
4. $S -> C : ({Hash_2})K_{CS}$

Hash Computation:
- $Hash_1$ = #($N_C,N_S,E_S(K_{seed}))$
- $Hash_2 = #(N_C,N_S,E_S(K_{seed}),({Hash_1})_K_{CS})$
Session Key Generation
- $K_{CS} - f(N_C,N_S,K_{seed})$ where $K_{CS}$ is the session key derived from $N_C, N_S$ and $K_{seed}$
#### Mapping TLS Message Flow to Cryptographic Representation
**ClientHello (C -> S)**
- Textual: Client sends a random nonce and supported cipher list.
- Mathematical: **C -> S : $N_C$**
- $N_C$ is the client's nonce, used in key derivation and preventing replay attacks
**ServerHello + Certificate (S -> C)**
- Textual: Server responds with a random none and chose cipher suite.
- Server sends its certificate (signed by CA)
- Mathematical: S -> C : $N_S$, $Cert_S$
- $N_S$ is the server's random nonce, and $Cert_S$ is the server certificate containing its public key
**Key Exchange (C -> S)**
- Textual: Client encrypts a pre-master secret with the server's public key.
- Mathematical: C -> S : $E_S(K_{seed}),({Hash_1})K_{CS}$
- $E_S(K_{seed})$: The pre-master secret encrypted with the server's public key
- $Hash_1$ ensures integrity and is encrypted using the session key $K_{CS}$
**Server Verifies and Responds (S -> C)**
- Textual: Server verifies handshake and confirms key agreement
- Mathematical: $S -> C: ({Hash_2})K_{CS}$
- $Hash_2$ is computed over handshake data, confirming mutual agreement.
**Key Derivation**
- Textual: Both sides derive the session key using nonces and exchanged key material
- Mathematical: $K_{CS} = f(N_C,N_S,K_{seed})$ 
- f is a Key Derivation Function (KDF) that combines $N_C, N_S$ and $K_{seed}$ to generate $K_{CS}$
![[Pasted image 20260121135150.png]]

#### Weaknesses in TLS
**Configuration Weaknesses:**
- **Cipher Downgrading** (forcing weaker ciphers)
- **Self-Signed Certificates** (no trusted authority)
**Direct Attacks on Implementations:**
- **Apple's** `goto fail` **bug** (logic flaw in TLS)
- **LogJam Attack** (weak Diffie-Hellman primes)
- **HeartBleed** (buffer over-read in OpenSSL)

#### Self-signed Certificates
- Maintaining a set of certificates is hard (especially on apps and IoT devices)
- It's much easier to accept any certificate (or certificates that sign themselves)
- If the client accepts the self-signed certificates, then it's easy to man-in-the-middle.
- This has been shown to happen a lot in devices and code that use TLS

#### Cipher Suites
- What if one side supports a weak cipher suite but the other does not?
- This is generally considered safe
- Browser developers removed all weak ciphers, some remained in servers
- This depends on different cipher suites being incompatible, e.g.
	- `SSL.RSAWITH.DES.CBC.SHA` and `TLS.DHE.DSS.WITH.AES.256.CBC.SHA`

### LogJam: Breaking TLS Encryption
**Key Takeaways**
- **TLS servers** commonly support **weak 512-bit 'export-grade' Diffie-Hellman (DH) groups**
- A **MITM attacker can force TLS to use a weak DH group**, even if a stronger one is available.
- **Precomputed discrete logarithms allow attackers to break the key in real-time**
- This lets an attacker **passively decrypt TLS traffic at scale**.

#### Diffie-Hellman in TLS
**Diffie-Hellman (DH) key exchange is widely used in TLS for forward secrecy:**
1. Client and server agree on a **prime number** *p* and a **generator** *g*.
2. Client picks a secret *a*, computes **A = $g^a$** mod *p*, and sends **A** to the server.
3. Server picks a secret *b*, computes **B = $g^b$** mod *p*, and sends *B* to the client.
4. Both parties compute the **shared secret**

		$K = B^a mod p = A^b mod p$
###### How LogJam Works
**Step 1: Man-in-the-Middle Attack**
- The attacker intercepts the `ClientHello` message.
- The client proposes a **strong Diffie-Hellman group** (2048-bit)
- The attacker modifies this to request an **export-grade 512-bit DH group**

**Step 2: Server Accepts Weak DH Group**
- The server **allows** the downgrade and responds with a weak DH group.
- The attacker can now easily compute the discrete log for the shared key.

##### LogJam: Downgrade Attack in Action
**Original Secure TLS Handshake:**
1. **C -> S**: `ClientHello` (Strong DH group, e.g. 2048-bit)
2. **S -> C**: `ServerHello` (Same DH group)
3. **S -> C**: `Certificate, DH Params`
4. **C -> S**: `Key Exchange`

**Downgraded TLS Handshake (LogJam Attack):**
1. **C -> MITM -> S**: `ClientHello` (Requesting weak 512-bit DH)
2. **S -> MITM -> C**: `ServerHello` (Accepting weak 512-bit DH)
3. **S -> C**: `Certificate, Weak DH Params`
4. Attacker **quickly computes the shared secret** due to precomputed discrete logs.
5. Attacker decrypts and relays traffic in real-time.

**Why LogJam Works**
1. **Many servers reuse the same small set of DH primes.**
	- The NSA (and others) can precompute discrete logs for these primes.
2. Export-grade cryptography is still widely supported.
	- These 'weak' DH groups were left in for legacy reasons.
	- Attackers can downgrade connections to force weak groups.
3. No authentication of the DH parameters.
	- The TLS handshake does not authenticate the DH group selection.
	- Attackers can modify the handshake without detection.

**Defending Against LogJam**
Mitigation Steps:
- Increase minimum DH key size to at least 2048 bits.
- Disable export-grade ciphers completely.
- Use unique DH groups instead of common shared primes.
- Prefer Elliptic Curve Diffie-Hellman (ECDH) over traditional DH

Industry Response:
- Browser vendors (Chrome, Firefox) removed support for weak DH groups.
- TLS 1.3 removes support for static DH and export-grade cryptography. 
#### Conclusion
- TLS secures communication, but only when **properly implemented and configured**.
- Weak ciphers, flawed implementations and misconfigurations lead to major attacks (**HeartBleed, LogJam, Cipher Downgrade**)
- Always use **modern TLS versions, strong ciphers and regular updates**
- Security is an ongoing process.

# TOR
### Proxy: Hotspot Shield VPN
- An internet connection reveals your IP number.
- VPNs promise **"Anonymity"**
- Connection made via their servers.
- The intended recipient server never sees your IP address

#### Virtual Private Networks (VPNs)
- VPNs securely connect you to another network over the internet.
- **E.g.** You can connect to the school's printers via the school's VPN.
- Provides privacy and security by encrypting your connection
- **Encryption**: VPNs use certificates and encryption protocols like **TLS** or **IPSec** to protect data.

##### Anonymity
- To get some anonymity, you can route all your traffic via the VPN.
	- Server thinks you are the VPN provider
	- ISP only sees the connection to the VPN
	- A global observer can probably link your connections.
- **There is no anonymity to the VPN provider**

Your WiFi provider knows:
- Your WiFi's outgoing Ip address
- That you are connected to the VPN

Your VPN provider knows:
- Your WiFi's outgoing IP address
- That you are connected to the VPN
- Your VPN's outgoing IP address
- That you are browsing to `https://bham.ac.uk`

Your website provider knows:
- Your VPN's outgoing IP address
- That you are browsing to `https://bham.ac.uk`
- The contents of your communication with the website

### Onion Routing
- You get the best anonymity by routing your traffic via **multiple proxies**.
- Onion Routing ensures that your message is **securely encrypted in layers** and routed through multiple nodes.
- Each node **only knows the previous and next hop**, ensuring **no single entity** can trace the full path.
- The **Tor network** implements this protocol.
- 