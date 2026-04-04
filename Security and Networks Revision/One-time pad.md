#SaN 

**One-time pad** encryption requires the use of a single-use **pre-shared key** that is >= to the size of the message being sent.   
A **plaintext** is paired with a **rando secret key** (aka one-time pad). Then, each bit or character of the plaintext is encrypted by combining it with the **corresponding** bit or character from the pad using **modular addition**.  
  
The key must be:  

1. At least as long as the plaintext.
2. Truly random.
3. Never reused in whole or in part.
4. Kept completely secret by the communicating parties.