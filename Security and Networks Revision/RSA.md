#SaN 



## RSA scheme
- $Enc(PK,m)$: on input an element $m ∈ ℤ^∗_N$ and the public key $PK = (e, N)$ compute
	- $c = m^e (mod N)$
- $Dec(SK,c)$: On input an element $c ∈ ℤ^∗_N$ and the private key $SK = (e,d,N)$ compute
	- $m = c^d (modN)$

### Example
Generate two distinct primes *p* and *q* of same bit size $𝜆$
	$p = 3, q = 11$
Compute $N = pq$ and $𝜙(N) = (p - 1)(q - 1)$
	$N = 33, 𝜙(N) = 20$
Choose at random an integer $e (q < e < 𝜙(N))$ such that gcd $(e, 𝜙(N)) = 1$
	Let $e = 7$
	Note $gcd(7,20) = 1$
Compute *d* such that $e * d ≡ 1 (mod) 𝜙(N))$
	We find $d = 3 as$
		$7 *3 + (-1) * 20 = 1$
Public key $PK = (e, N)$. The private key $SK = (e,d,N)$
	$PK = (e = 7, N = 33)$
	$SK = (e = 7, d = 3, N = 33)$

## Exploits
- E.g.  To get $m^2$, the adversary just needs to compute $c^2 (mod N)$
- 