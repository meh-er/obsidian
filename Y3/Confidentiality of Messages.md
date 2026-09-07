# Symmetric Cryptography
* **Symmetric** implies that the 'same key' is used on 'both ends'
* **Encryption** schemes are used to ensure confidentiality of messages

▶ ==m== is the message (plaintext) which is from the plaintext space: ==m ==∈ M
▶ c is the ciphertext which is from the ciphertext space: c ∈ C
▶ ==sk== is the secret key which is from the key space: ==sk== ∈ K

Secrets are indicated in ==yellow==

A symmetric encryption scheme is given by three algorithms
▶ Gen : K → ==sk ==generates a secret key via randomly sampling an element from the keyspace
▶ Enc : M × K → C maps an element from the plaintext space to the ciphertext space
(using an element from the key space)
▶ Dec : C × K → M recovers the plaintext from the ciphertext (using the secret key)

A symmetric encryption scheme is said to be correct if:
∀m ∈ M and ∀==sk== ∈ K : Decsk (Encsk (m)) = m. Thus encryption must be invertible.