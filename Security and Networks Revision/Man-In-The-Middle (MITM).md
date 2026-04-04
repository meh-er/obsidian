#SaN 

## Example
Suppose **Alice** wishes to communicate with **Bob**. Meanwhile **Mallory** wishes to intercept the converrsaion and deliver a false message to Bob under the guise of Alice.
1. Alice sends a message to Bob, which is intercepted by Mallory
2. Mallory relays this message to Bob; Bob cannot tell it is not really from Alice
3. Bob responds with his encryption key
4. Mallory replaces Bob's key with her own, and relays this to Alice, claiming this is Bob's key.
5. Alice encrypts a message with what she believes to be Bob's key, thinking only Bob can read it
6. However, because it was actually encrypted with Mallory's key, Mallory can decrypt it, read it, modify it, re-enrypt with Bob's key, and forward it to Bob.
7. Bob thinks that this message is a secure communication from Alice.

### Defence
#### Authentication
A **public key infrastructure**, such as **Transport Layer Security**, may harden **TCP** against MITM attacks. In such structures, clients and servers exchange certificates which are issued and verified by a trusted third party called a **certificate authority** (CA). If the **original key** to authenticate this CA has **not** been the subject of a MITM attack, then the certificates **issued by the CA** may be used to authenticate the messages sent by the owner of that certificate. Use of **mutual authentication**, in which both the server and the client validate the other's communication, covers both ends of a MITM attack. If the server or client's identity is not verified or deemed as invalid, the session will end.

#### Tamper Detection
Latency examination can potentially detect the attack in certain situations, such as with **long calculations**, such as [[hash functions]]. To detect potential attacks, parties check for discrepancies in response times. 