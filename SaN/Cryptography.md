---
tags:
  - SaN
  - SaN
---
# Cryptography

- Cryptography describes how to transfer messages between participants without anyone else being able to read or modify them
- Prerequisite for CS

### Codes vs Ciphers

- A code is any way to represent data. Will use bitstrings (sequence of bits) to represent data
- A cipher is a code where it is difficult to derive data from code
    - Almost always uses a key
    - Data for a cipher usually called _plain txt_, encoding called _cipher text_
    - Function from plain text to cipher text called _encryption_
    - Function from cipher text to plain text called _decryption_

### Using a Key

These ciphers are easy to break because as soon as you know the scheme you can decrypt the message

**Kerchoffs’ principle**: A cipher should be secure even if the attacker knows everything about it apart from the key

For instance, we can use the Caesar cipher using _n_ rotations, but only 26 possible keys so you can just try them all (breaking the cipheri s 26 times harder without the key)

A better scheme replaces each letter with another letter. here there are 26! possible keys

**Frequency Analysis**

- While hard to break by brute force, replacing each letter with another is easy to break using _frequency analysis._
    
- Frequency analysis counts the number of times
    
    - each symbol occurs
    - each pair of symbols
    - etc
    
    and tries to draw conclusions from this.
    

## Symmetric Cryptography

- Arithmetic modulo _n_ means that you count up to _n_ -1 then loop back to 0
- i.e., 0,1,2,…,n-1,0,1,2,…n-1,0,1,2,…
- _a mod b = r_ for the largest whole number _k_ such that _a = b * k + r_
- e.g. 9 _mod_ 4 = 1 because 9 = 2 * 4 + 1

**xor**

- xor ⊕ is binary addition modulo 2:
    
    - 0 ⊕ 0 = 0
    - 1 ⊕ 0 = 1
    - 0 ⊕ 1 = 1
    - 1 ⊕ 1 = 0
- xor on bitstrings of same length defined by applying xor to corresponding bits
    
- Important properties
    
    - xor is associative and commutative
    - for all bitstrings _M_, _M_ ⊕ 0 = _M_
    - for all bitstring _M_, _M_ ⊕ _M_ = 0
    
    where 0 s a bitstring of all 0’s of the appropriate length
    
    **One Time Pads**
    
    - Needs a key as long as the message.
    - XOR/add the key and the message:
    - (Demonstrated here with strings and addition and subtraction of keys, for bitstrings use xor)
    
    ```c
    Message: HELLOALICE
    Key: HFLQRZFJK
    Cipher text: ALRWERKNLO
    ```
    
    _**Given any ciphertext of a certain length, without knowing the key the probability of the ciphertext being the encryption of a plaintext of the same length is the same for all plaintexts of the same length as the ciphertext.**_
    

**Block Ciphers**

- Modern ciphers work on blocks of plain text, not just a single symbol
- They are made up of a series of permutations and substitutions repeated on each block.
- The key controls the exact nature of the permutations and substitutions

### **Advanced Encryption Standard (AES)**

- AES is a state-of-the-art block cipher
- It works on blocks of 128-bits
- It generates 10 round keys from a single 128-bit key
- Uses one permutation, _ShiftRows_ and three substitutions SubBytes, _MixColumns, AddRoundKey_

**Security of AES**

- No formal proof of securiy (P = NP?) but best known cryptographic attack requires $2^{126}$ key guesses - an (irrelevant) improvement of factor 4 compared to $2^{128}$ key guesses via briute force attack
- There are side channel attacks (e.g. via measuring power consumption, execution time)
- Key aspects of security:
    - Shuffling of rows and columns to ensure small chane in input causes very big change in output
    - Require at least one non-linear operation (in the sense of linear algebra) on the data

### Data Encryption Standard (DES)

- Standard before AES
- S-boxes had made DES resistant to differential cryptanalysis

### Padding

- Block ciphers only work on fixed size blocks
- If the message isn’t of the right block size we need to pad the message
- But receiver needs to tell the difference between the padding and the message.
- If there is 1 byte of space write 01
- If there are 2 bytes of space write 0202
- If there are 3 bytes of space write 030303
    - If the message goes to the end of the block add a new block of 16161616..
- Block Ciphers can be used in a number of modes:
    - Electronic codebook mode (ECB)
        - Each block is encrypted individually
        - Encrypted blocks are assembled in the same order as the plain text blocks
        - If blocks are repeated in the plain text, this is revealed y the cipher text
- Cipher Block Chaining Mode (CBC)
    - Each block XOR’d with previous block
    - Start with a random Initialization Vector (IV)
    - Helps overcome replay attack
    - Suppose the plain text is $B_1$, $B_2$…, $B_n$
        - IV = random number (sent in the clear)
        - $C_1$ = encrypt ($B_1$ ⊕ IV)
        - $C_n$ = encrypt($B_n$ ⊕ $C_{n-1}$)

### Probabilistic Encryption

- Probabilistic encryption schemes use random elements to make every encryption different.
- CBC with a random IV is a good way to make encryption probabilistic
- Using CBC and random IVs lets me encrypt the same message, and with the same key, without an attacker realising.
- IV must be random, different for each encrypted block
- Choosing fixed IV can have devastating effect (Zerologon vulnerability for Microsoft Windows)
    - Windows has RPC for updating password on the domain controller
    - Uses cryptographic protocols for authenticating these requests
    - In particular, use AES with block cipher mode called CFB8, which uses IV exactly as CBC mode
    - This is secure with randomly chosen IV
    - Implementation chooses IV to always be 0
    - Consequence: AES-CFB8 encryption on all-zero plaintext will produce all-zero ciphertext
    - This can be used to bypass authentication completely and set domain controller password
    - Attack only requires network access to domain controller, which is available from any machine in the domain
    - CVSS score of 10.0
    - Department of Homeland Security forced all US government institutions to patch Windows Servers within 3 days
- Example: Sony PlayStation
    - Sony needs to stop games being copied
    - CD and full disk encryption
    - User can read and write areas of the hard disk, for own files, notes, etc
    - Why won’t CBC work?
    - With CBC, you need to encrypt, or decrypt, the whole file to get to the end.
    - The Sony PlayStation uses ECB full disk encryption, to stop people copying games.
    - User can access files they made themselves
    - Hardware controls user access to data
    - Disk Encryption Attack
        - Remove disk and make copy
        - Replace disk in Playstation
        - Copy a file to the disk
        - Remove disk and find the bit of disk that changed (this is the encrypted file)
        - Copy target data to user area
        - Restart the PlayStation and ask for your file back
        - PlayStation decrypts the file and gives you back the plain text

### Counter Mode (CTR)

- Plain text: $B_1$, $B_2$,…, $B_n$
- IV: random number (sent in clear)
- Cipher text: $C_1$, $C_2$,…, $C_n$ where

### Cipher Texts Can Be Altered

- AES encryption with a particular key maps any 128-bit block to a 128-bit block (or 256)
- AES decrypt also maps any 128-bit block to a 128-bit block
- Decrypt can be run on any block (not just encryptions)
- If you know the plaintext you can change CTR encrypted messages
    - e.g. if I know $Enc_{CTR}(M_1)$ and I know $M_1$, I can make a ciphertext that decrypts to any message I want, e.g. $M_2$
    - New ciphertext is
        - $ENC_{CTR}(M_1)$ ⊕ $(M_1 ⊕ M_2)$

# Hashes, MACs and Authenticated Encryption

**Hashes:** Detect corruption of messages in general. new hashes can be generated by the attacker.

**MAC (Message Authentication Codes)**: use a key to ensure that message has not been changed

**Authenticated Encryption**: Provides encryption such that manipulation of cipher texts can be detected. Often uses MACs

## Block mode

- CBC mode: any change affects all of the rest of the message
- ECB mode: any change affects only the block
- CTR mode: any change affects only the bits altered