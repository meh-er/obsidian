1. What is the use of SUID and GUID?
		Saved User ID: Saves the 'Effective UID (EUID)' when it was executing a process, useful for logs where you want to know what permissions a user had at a given moment.
		Global User ID: Used as a wisder user id that persists through the entire account and doesn't change.
2. N/A
3. Suppose you are designing a linux shell program that would involve a login/password based access control. Assuming you have root access, what should you do to ensure security from probable trojan password capture programs?
		You should not be logged in to root access as much as possible, so that there are limited times where you can have your password stolen, update firewall to check for malicious programs, need sudo before executing any important processes. 
4. Suppose a password hashing does not involve salt. What could be the security vulnerabilities.
		No element of randomization which means passwords may match rainbow tables if common. Attackers who find these hashed passwords without salt could compare them to other known passwords and their hashes (rainbow table) and figure out what the password means.
5. Suppose h is a preimage-resistant and collision hash function. I construct another function such that H(x) = h(x)||x where || is the concatenation operation. Is H collision resistant? Is H preimage resistant?
		H(x) = h(x) concat x
		to be preimage resistant: y = h(x)||x where we can find out x easily
		if we split y we get: h(x) and x, therefore we know x and this is **not preimage resistant**.
		to be collision resistant: there must not be any H(x1) = H(x2) where x1 != x2
		would need: h(x1)||x1 == h(x2)||x2
		**is collision resistant**. 
6. Is it sensible to reccomend minimum password length?
		Yes - for security purposes, it is more difficult to brute force or guess a longer password.
7. Suppose I create a hash function H which works as H(x) = xor_i x_i In other words, H(x) is the xor of all the bits of x. Find collision in H.
		say x1 = 1. x2 = 1 | y1 = 0, y2 = 0
		then hash function is x1 XOR x2: 0
						y1 XOR y2: 0
		H(x) = H(y) but x != y so we have a collision.
8. What will be the cipertext when the message 'random' is encrypted using the one time pad with key 'number'?
		

| m   | k   | total | mod | letter |
| --- | --- | ----- | --- | ------ |
| 17  | 13  | 30    | 4   | e      |
| 0   | 20  | 20    | 20  | u      |
| 13  | 12  | 25    | 25  | z      |
| 3   | 1   | 4     | 4   | e      |
| 14  | 4   | 18    | 18  | s      |
| 12  | 17  | 29    | 3   | d      |

9. Suppose we have a processor which works on HEX characters. What will be the algorithm for one-time pad encryption and decryption.
		It will be m + k (mod 16), as there are 16 hex characters in 
10. You want to encrypt an English text using a block cipher that only takes binary strings as input messages. How will you perform this encryption.
		Should still be fine - block ciphers at minim take in 1 byte at a time (CTR), which will still be 9 bits which will still be a binary string. You can convert all of these English text characters into binary.
11. AES requires 10 rounds. Argue why the AES algorithm with only 1 round will be insecure.
		With only 1 round, AES will only have substituted values once, xored with subkey once, and shifted once. This means that there is no proper randomness or diffusion of the block, so an attacker may be able to undo it a lot easier.
12. Write the pseudocode for the block cipher modes of operations ECB, CBC, and counter mode
		```ECB: p -> E_k -> c
			let plaintext = getInput
			ciphertext = ENCRYPT(plaintext)_KEY 
		CBC: c = E_K(p XOR IV)
			let p = getInput
			let iv = 00000000000
			let in = p ^ iv
			ENCRYPT(in)_KEY
		CTR: c = E(N)_K XOR p
			let n = random()
			p = getInput()
			enc = ENCRYPT(n)
			c = p ^ enc
13. Write the decryption algorithm for ECB, CBC, and counter mode
			`ECB: p = D_k(c)`
			`CBC: p = D_k(c) XOR IV`
			`CTR: no decryption, xor again, i.e.`
					`p = E_K(N) XOR c`
14. Why can't we use CBC-MAC as a cryptographic hash function
		CBC-MAC is an authentication method, based on CBC mode of operation, which is **reversable**. For something to be a hash function, the key idea is that it cannot be undone. Since you can decrypt CBC, you can therefore decrypt CBC-MAC (the last block sent through CBC), which is also used to ensure that the MAC was created by who it says it was. Therefore, it cannot be a hash function!
15. For secure key exchange, can Alice use the same public-key/secret key for establishing secret keys to communicate with two parties, Bob and Malory?
		Say A -> B uses PK_A, SK_A
			and A -> M uses PK_A, SK_A
			only A has SK_A so can decrypt communications from B and M. B and M only have access to the public key, so yes she should be fine to use the same pair as long as the secret key **stays secret**.
16. Why public keys need to be authenticated. Explain with an example.
		authenticated means knowing who is on the other end.
		If not authenticated: 
			-  A -> E, N_A thinking E is a valid person
			- E -> B,  N_A where B thinks E is A
			- B -> A, N_A, N_B, A thinks that this is from E
			- A -> E, N_B E decrypts N_B from A and now has access to secure communication
			- E -> B, B and A authenticate the connection and now think they are safe
		Without authentication, A and B will never know that E has done a MITM attack and has access to their secure channel. However, if they send their identifications in the communications, A and B will know that theya re the only ones in this communication and a MITM will fail, so it is important for absolute secrecy and security.
17. In RSA we have the public exponent N = pq, product of two primes p and q. What would be the problems if we had N to be just a prime p. 
		If P was the large number, then computing the rest of RSA would not work. 
18. Given c, a ciphertext generated by RSA encryption using the public (e,N) on some unknown message m, can you construct a ciphertext c' that would decrypt to m^2 mod N
		c = m^e mod n
		RSA is malleable
		c' = m^2 mod N.
		c' = c^2 mod N
		
19. The certificate of canvas.ham.uk is signed by Let's Encrypt. If we do not know/trust the public key of Let's Encrypt, how will we establish the validity of the signature?
		Let's Encrypt should have their certificate from a Certified Authority. If we do nto trust the certificate authority, we can check their certificate and follow the chain of command until we reach the root certificate, which should be from a trustworthy organisation. 