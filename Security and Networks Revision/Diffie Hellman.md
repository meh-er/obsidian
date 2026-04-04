#SaN 

## What is **Diffie Hellman Key Exchange**?
DH key exchange is a **mathematical method** of securely generating a **symmetric cryptographic key** over a public channel. Example below.  
  
For the sake of simplicity and practical implementation of the algorithm, we will consider only 4 variables, one prime P and G (primitive root of P) and two private values a and b.  
P and G are both **publicly available numbers**. Users Alice and Bob pirck private values a and b and they generate a key and exchange it publicly. The opposite person receives the key and that generates a secret key after which they have the same secret key to encrypt.  
  

| **Alice**                                        | **Bob**                                          |
| ------------------------------------------------ | ------------------------------------------------ |
| Public Keys available = P, G                     | Public Keys available = P, G                     |
| Private Key Selected = a                         | Private Key Selected = b                         |
| Key generated = $x=G^amodP$                      | Key generated = $y = G^bmodP$                    |
| Exchange of generated keys takes place.          | Exchange of generated keys takes place.          |
| Key received = y                                 | Key received = x                                 |
| Generated Secret Key = $k_a = y^amodP$           | Generated Secret Key = $k_b = x^bmodP$           |
| Algebraically, it can be shown that $k_a = k_b$  | Algebraically, it can be shown that $k_a = k_b$  |
| Users now have a symmetric secret key to encrypt | Users now have a symmetric secret key to encrypt |
