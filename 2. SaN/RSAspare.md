
# 1: Pick two prime numbers p and q
p = 11
q = 13

# 2: Calculate Key values

Private key: (n,d)
Public key (n.e)

n = p * q
n = 11 * 13
n = 143

phi(n) = (p - 1) * (q -  1)
phi(143) = (10 * 12)
phi(143) = 120

**e must be coprime to phi(n)**
e.g. e = 17

=> gcd(e, phi(n)) = 1
=> gcd (17,120) = 1

multiplicative inverse of e
d * e = 1 if we compute mod  phi(n)

(e * d) mod phi(n) = 1

e.g. d = 113

=> Private key (143, 113)
=> public key (143, 17)

# 3: Encrypt
To encrypt number *m* to ciphertext *c* the following formula is applied.

$$c = m^e mod n$$
m = 88
=> c = $88^{17} mod 143$
=> c = 121

# 4: Decrypt
Use inverse formula: 

$$m' = c^d mod n$$
c = 121 
=> m' = $121^{113} mod 143$
m' = 88

