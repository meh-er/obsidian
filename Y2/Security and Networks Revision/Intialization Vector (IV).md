#SaN 


IV is a random or unique value used in **combination** with a secret key to initialize the encryption process. It ensures that the **same plaintext** encrypted multiple times will produce different ciphertexts, enhancing security by preventing patterns from emerging. It is essential for CBC & CTR. IVs should be transmitted or stored alongside the ciphertext to enable successful decryption, but they must never be reused with the same key.