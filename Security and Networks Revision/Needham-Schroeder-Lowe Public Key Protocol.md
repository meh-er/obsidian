#SaN 

### Public-key protocol
This assumes the use of a **public-key encryption algorithm** (asymmetric methods).

Here, Alice (A) and Bob (B) use a trusted server (S) to distribute public keys on request. These keys  are:
- $K_{PA}$ and $K_{SA}$, respectively public and private halves of an encryption key-pair belonging to A
- $K_{PB}$ and $K_{SB}$, similar belonging to B
- $K_{PS}$ and $K_{SS}$, similar belonging to S. (note that this key-pair will be used for [[Digital Signatures]], i.e. $K_{SS}$ used for signing a message and $K_{PS}$ used for verification. $K_{PS}$ must be known to A and B before the protocol starts)/

![[Pasted image 20260405163013.png]]

At the end of the protocol, A and B know each other's identities, and know both $N_A$ and $N_B$. These nonces are **not** **known** to eavesdroppers.


### MITM
This protocol is vulnerable to a [[Man-In-The-Middle (MITM)]] attack. If an imposter *I* can persuade *A* to initiate a session with them, they can relay the messages to *B* and convince *B* that he is communicating with *A*.


![[Pasted image 20260405163241.png]]

At the end of the attack, B falsely believes that A is communicating with him, and that $N_A$ and $N_B$ are known only to A and B.


#### Fix
The fix involves the modification of message six to include the responder's identity, that is we replace:

$B->A:{N_A, N_B}_K_{PA}$

with the fixed version:

$B -> A : {N_A, N_B,B}_K_{PA}$
