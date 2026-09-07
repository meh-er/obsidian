#SaN 

Block cipher Modes of Operation define how to securely encrypt and decrypt large amounts of data using a block cipher. To encrypt data larger than a single block, different modes of operation are used to ensure both security and efficiency.  

- **Electronic Code Book (ECB)**: Each block of bits input plaintext is encoded independently with the same key. This provides **secure transmission of single values** (e.g. encryption key). It can be used in parallel encryption and is simple byt is prone to **cryptanalysis.**
	
- **Cipher Block Chaining** **(CBC)**: THe input to the algorithm is **XOR** of the **following** block of plaintext with the **previous** block of ciphertext to produce the next **unit** of plaintext. This is **general**-purpose block transmission. it works well for authentication and is more resistive to **cryptanalysis** but requires the previous ciphertext block, making parallel processing difficult.  
    
- **Counter Mode (CTR)**: An encrypted counter (CTR) is **XORed** for each block of plaintext, with the counter incremented for each successive block. A different counter for each block means the **same** **plaintext** c**an map to different ciphertext** - no direct relationship! Parallel execution is possible as they are not chainted together but CTR requires a **synchronous counter** at both transmitter and receiver and if this is lost will be inaccurate.