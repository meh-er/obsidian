#SaN 


# What is a Digital Signature?

### Signature Schemes Designs: RSA Full Domain Hash
- **Public Functions**: A hash function  $H : {0,1}^* -> Z^∗_N$
- **Keygen**: Run RSA.Keygen. $pk = (e,N), sk = (d, N)$
- **Sign**: Input: $sk, M$. Output: $σ = RSA.Dec(sk, H(M)) = H(M)^d mod N$
- **Verify**: Input: $pk, M, σ.$ If RSA.Enc$(pk,σ) = H(M)$ output accept, else reject
- If $σ^e mod N = H(M)$ output accept, else reject.

Note: A hash function takes strings of abritrary length as input and produces a fixed length output. For cryptographic [[hash functions]], given a $z$, it is very expensive to find $x$ such that $H(x) = z$.
