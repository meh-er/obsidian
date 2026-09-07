## 🔹 **Q2: RSA Signature with Multiplication**

Modified scheme:

- **Sign**:
    
    σ=(H(M1)⋅H(M2))dmod  N\sigma = (H(M_1)\cdot H(M_2))^d \mod Nσ=(H(M1​)⋅H(M2​))dmodN
- **Verify**:
    
    σe≡H(M1)⋅H(M2)\sigma^e \equiv H(M_1)\cdot H(M_2)σe≡H(M1​)⋅H(M2​)

### Tasks:

(a) Given signatures on M1M_1M1​ and M2M_2M2​, construct a valid signature on a new message  
(b) What property of RSA are you exploiting?





S: $x = (H(M1)H(M2))^d mod N$
$x1 = H(M1)^d mod N$
$x2 = H(M2)^d mod N$
V: $x^e = H(M1)H(M2)$
$x' = x1x2$

$(x′)^e modN$
= $(x1x2)^e mod N$
=$(x1)^e (x2)^e mod N$

$x1 = (H(M1)^d)^e) mod N$
$x2 = H(M2)^{de} mod N$
$de = 1$
$x2 = H(M2) mod N$
$x1 = H(M1) mod N$

$x' = H(M1)H(M2) mod N$
$H(M1)H(M2)mod N = H(M1)H(M2)$


## **Q3: Broken MAC Construction**

A MAC is defined as:

$$MAC_k(M)=H(k ∣∣ M)$$


### Tasks:

(a) Explain why this is insecure  
(b) Describe an attack  
(c) What attack property are you exploiting?

👉 _Hint_: Think **length extension**

a) Concatenates Message and key and then hashes
MACs are insecure because they are vulnerable to length extension attacks
therefore could do 
H1 = H(k || M)
H2 = H(H1, n) where n is extra attacker controlled bit of data, since includes the key will still be verified

b) Length extension attack on MAC

c) nature of hashes


## **Q4: CBC-MAC (Variable Length)**

CBC-MAC is used on variable-length messages:

$$MAC_k(M)=CBC(k,M)$$

You are given:

- $MAC(M1)$
- $MAC(M2)$

### Tasks:

(a) Construct a valid MAC for a new message  
(b) Explain why variable-length breaks security

a) 
$MAC(M1) = CBC(k,M1)$
$MAC(M2) = CBC((MAC(M1)),M2)$

$MAC(M3) = CBC((MAC(M2)),M3)$

let k = 1
then we know MAC(M1) and MAC(M2) and therefore MAC(M3)