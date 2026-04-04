#SaN 

AES performs operations on bytes of data. Since the block size is 128 bits, the cipher processes 128 bits (16 bytes) of input data at a time. The number of rounds depends on the key length. From this, a **Key Schedule Algorithm** calculates all the round keys from the initial key. It considers each block as a 4x4 matrix.  
Each round:  

1. **Substitutes** each byte by another byte (using lookup table)
2. **Shifts** each row a particular number of times (performing a left circular shift, the first row does not move)
3. **Multiplies** each column with a specific matrix (every round but the last one)
4. **XORs** previous stage with the corresponding round key. The bytes are no longer considered as a grid and are then output as 128 bits of data. 

Decryption is simply the inverse of this.