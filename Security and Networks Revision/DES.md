#SaN 

DES was **replaced** by AES.  

- It is a block cipher that encrypts data in **64 bit blocks**.
- It takes a 64-bit **plaintext input** and generates a corresponding 64-bit ciphertext output.
- The main key-length is 64-bit, which is transformed into 56 bits by skipping every 8th bit in the key.
- It encrypts the text in 16 rounds where each round uses 48-bit subkey.
- This 48-bit subket is generated from the 56-bit effective key. 
- The same algorithm and key are used for both encryption and decryption with minor changes.
- It is based on two attributes of **Feistel cipher** (Substitution and Transposition).   
    It consists of 16 rounds.