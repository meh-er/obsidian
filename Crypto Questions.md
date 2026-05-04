1.**What is the use of SUID and GUID**
- Saved UID holds the uid when an action was executed, storing a copy of the EUID at the time. This is useful if a user's permissions change over time, you can see what they could do at a particular time. Useful for logging/auditing purposes.
- GUID
2 . **To ensure the login/password page is not fakeWindows requires Ctrl-Alt-Del before displaying the log-in screen. How would the operating system ensure that the correct log-in screen is displayed?**
- Use of MACs to ensure that the page matches?

3.**Suppose you are designing a linux shell program that would involve a login/password based access control. Assuming you have root access, what should you do to ensure security from probable trojan password capture programs. You do not need to write exact commands.**

- Not use root access at all times, only when necessary - like sudo
- MFA

4.**Suppose a password hashing does not involve salt. What could be the security vulnerabilities**
- Rainbow tables - could find hash on them and then know password
- Collision or pre-image attacks - two hashes of the same password will have the same result without salt

5.**Suppose h is a preimage-resistant and collision resistant hash function. I construct another function H such that
	H(x)=h(x)||x where || is concatenation
	 Is H collision resistant? Is H preimage resistant?**

- No?

6.**Is it sensible to recommend minimum password length?**
- no

7.**Suppose I create a hash function H which works as H(x) = xor_i x_i
	In other words, H(x) is the xor of all the bits of x. Find Collision in H.**

8.**What will be the ciphertext when the message 'random' is encrypted using the one time pad with key 'number'**

| **message** | **key** | **ciphernum** | **ciphertext** |
| ----------- | ------- | ------------- | -------------- |
| r = 17      | n = 13  | 30 - 26 = 4   | e              |
| a = 0       | u = 20  | 20            | u              |
| n = 13      | m = 12  | 25            | z              |
| d = 3       | b = 1   | 4             | e              |
| o = 14      | e = 4   | 18            | s              |
| m = 12      | r = 17  | 29 - 26 = 3   | d              |
- Message: euzesd

9.**Suppose we have a processor which works on HEX characters. What will be the algorithm for one-time pad encryption and decryption**

c = m  + k mod (no. of options)
m = k - c mod (no.options)

10.**You want to encrypt an English text using a block cipher program that only takes binary strings as input messages. How will you perform this encryption?**
- Convert every letter to it's binary equivalent for both message key

11.**AES requires 10 rounds. Argue why the AES algorithm with only 1 round will be insecure**
- Could brute force the changes to find the original input
- The changes are: substitution, left-shift (generally), multiplying rows (won't happen on the last one so won't happen if only used once), and xoring with the key. Considering you're left with substitution - could be brute forced if it only 1 round, left shift - once again can shift all rows back once easily and xoring with key - can be undone if key is found, very insecure!

12.**Write the pseudocode for the block cipher modes of operations ECB, CBC, and counter mode**

13.**Write the decryption algorithm for ECB, CBC and counter mode**
ECB: 
- encrypted with p ENC E_k = c
- decrypted with c DEC D_k = p

CBC:
- encrypted with p XOR iv /oldc' ENC E_k  = c
- decrypted with D_K(c) XOR oldc' = p

CTR:
- encrypted with ctr ENC E_k XOR p = c
- decrypted with c XOR ctr DEC D_k = p
14.**Why can't we use CBC-MAC as a cryptographic hash function?**
- 