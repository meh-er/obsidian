Describe three possible vulnerabilities for a web application posed by an attacker who **fabricates HTTP headers** rather than using the web app running via a reliable browser

1. Fabricated authentication headers to allow admin priveleges e.g. sending `X-Role: admin`
2. Fabricated session id/ cookie to get privileges e.g. guessing or reusing valid session id 
3. Fabricated header onput manipulation e.g. fake client IP to byass IP-based restrictions, fake Origin/referer to bypass CSRF protections, fake Host

How would you mitigate a**utomated brute-force attacks** (credential stuffing)?
- salting passwords so they are harder to match with brute forcing
- save passwords as hash so can't be guessed
- only allow a certain amt of password guesses in a time frame - either wipe data or record attempts  and stop action for y mins after x attempts

How would you mitigate **passwords/ other credentials being sent over unencrypted connections**?
- Send hashes over where possible so actual credential not being sent - `still vulnerable to a replay attack`
- Use MFA so even if credential is exposed, attackers can't get in
- * use tls (https) to encrypt data in transit
- `use token based authentication`

Describe three auxiliary motives that an attacker may have when using SQL injection techniques to learn about a target.
- witholding sensitive data
- idk
- murder
- `database enumeration
- identify valid inputs/auth bypass
- look at error messages`

What is RSA vulnerable to?
- malleability - x mod n + y mod n = x + y mod n - can be adapted if you know a certain amount
- if n is too small, can brute force p and q


aes cbc
- bit flipping
- if iv is known/ van be changed (variable length can be controlled by attacker)

aes ctr
- bit flipping
- plaintext not actually encrypted
- reuse of keystream
- known plaintext attack
- no auth/integrity

What is RSA vulnerable to?
- badly chosen n, p, q
- 