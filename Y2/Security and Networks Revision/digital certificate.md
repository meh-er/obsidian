#SaN 

Browsers protect communications by **authenticating** HTTPS servers using **certificates**, digital documents that **bind** a public key to an individual subject (i.e. person, company, organisatiion).  The binding is asserted by having a trusted **certificate authority** (CA) verify the identity of prospective certificate owners, via automated and manual checks against qualified databases.

CAs can use a private key to cryptographically sign all issued certificates. Such signatures can cryptographically prove that a certificate was issued by a specific CA and that it was not modified after it was signed.
CAs establish **ownership** of their **signing key** by holding a self-issued certificate (called the **root**) for the corresponding public key. 
Browsers are shipped with a built-in list of trusted roots. To verify a certificate, a browser will obtain a **sequence of certificates**, each one having signed the next certificate in the sequence, connecting the signing CA's root to the server's certificate. (called a **certification path**)

### X.509 certificates
X.509 certificates contain:  

- **Subject** (entity identity)
- **Subject's public key**
- **Issuer's name**

Verification Process:

- The issuer signs a hash of all the certificate data.
- To verify a certificate:
-   Compute the hash of the data
-   Check the signature using the issuer's public key.
- If i trust the issuer's public key, I can trust the subject's public key.