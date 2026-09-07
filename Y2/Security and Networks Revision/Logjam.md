#SaN 

Logjam is a security vulnerability in systems that use [[Diffie Hellman]] key exchange with the same prime number. 

### How Logjam Works
**Step 1**: Man-in-the-Middle Attack
- The attacker intercepts the (1) message.
- The client proposes a **strong Diffie-Hellman group** (2048-bit)
- The attacker modifies this to request an **export-grade 512-bit DH group** (downgrade attack)

**Step 2**: 
- The server **allows** the downgrade and responds with a weak DH group.
- The attacker can now easily compute the discrete log for the shared key.

### Why Logjam Works
1. **Many servers reuse the same small set of DH primes**.
	The NSA (and others) can precompute discrete logs for these primes.
2. **Export-grade cyrptography is still widely supported**.
	These 'weak' DH groups were left in for legacy reasons. 
	Attackers can downgrade connections to fore weak groups.
3. **No authentication of the DH parameters**
	The TLS handshake does not authenticate the DH group selection.
	Attackers can modify the handshake without detection.

### Defending against Logjam
**Mitigation Steps**:
- **Increase minimum DH key size** to at least **2048 bits**
- **Disable export-grade ciphers** completely
- **Use unique DH groups** instead of commonly shared primes.
- **Prefer Elliptic Curve DH** over traditional DH
