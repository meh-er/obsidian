#SaN 

SSL/TLS uses [[digital certificate]]s to establish an encrypted link between a server and a client. This allows **sensitive information** like credit card details to be transmitted securely over the internet. 
- It typically implements [[Needham-Schroeder-Lowe Public Key Protocol]] and [[Diffie Hellman]] for Internet.
- SSL protocol was standardised as TLS
- Provides encrypted communication and authentication using public keys.

**Encryption and Authentication**
- SSL/TLS supports various cryptographic algorithms:
	- [[RSA]]
	- [[DES]]
	- [[Diffie Hellman]]
- The specific cipher suite is negotiated at the start of the session.

### How it Works
SSL/TLS certificates authenticate identities and enable encrypted connections through the SSL/TLS handshake:

1. Client sends a random nonce and supported cipher list. (C->S)
2. Server responds with a random nonce and a chosen cipher suite. (S -> C)
3. Server sends its certificate (signed by CA). (S -> C)
4. Client encrypts a pre-master secret with the server's public key. (C->S)
5. The server verifies handshake and confirms key agreement. (S -> C)
6. Both sides derive the session key using nonces and exchanged key material.

### Weaknesses in TLS
**Insufficient Encryption Key Lengths**
- The longer the key length, the more possible values it can have
- TLS essentially provides 'a secure tunnel'
**Config**
- **Cipher Downgrading** (forcing weaker ciphers)
- **Self-Signed Certificates** (no trusted authority)
- 

### TLS
- Essentially provides 'a secure tunnel'
- TLS is used to prevent **eavesdropping** or **tampering** (vulnerable to other kinds of attacks)
- Creates a **stateful connection**
- Provides
	- What ciphers to use
	- Secret key
	- Authentication
	- Robust MITM, Replay attacks, Downgrade attacks
- Meant to be interoperable
- Message structure is fixed doesn't matter what language sent it

Padding attacks
Implementation attacks
Bug in implementation of TLS
