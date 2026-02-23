#Theory 

One way conversion of data used for integrity, verification & password storage.
- Fixed size output

**Examples**
MD5
- Produces a 128-bit hash value, commonly represented as a 32-character hexadecimal number
- Collision vulnerabilities --> susceptible to collision attacks, where two different inputs produce same hash
- Attackers can reverse engineer (logic not the hash itself which is one way) the hash to find an input that matches
- Speed at which hashes can be generated means its susceptible to brute force

SHA-1
- Collision attacks
- Improvements in technology, brute force attacks

SHA-256
- 512-bit input, producing a final 256-bit hash value.
- Computes quickly so it can be brute force attacker
