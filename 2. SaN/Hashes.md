---
tags:
  - SaN
  - SaN
---
# Hashes

- A hash of any message is a short string generated from that message
- The hash of a message is always the same
- Any small change makes the hash totally different
- It is very hard to go from the hash to the message
- It is very unlikely that any two different messages have the same hash

### Uses

- Verification of download of message
- Tying parts of a message together (hash the whole message)
- Hash the message, then sign the hash (electronic signature)
- Protect passwords (store the hash not the passwords)

### Attacks on hashes

- _Preimage attack:_ Find a message for a given hash: very hard
- _Collision attack:_ Find two messages with the same hash
- _Prefix collision attack:_ A collision attack where the attacker can pick a prefix for the message.

**SHA1**

- Not really practical, but no one trusts SHA-1 anymore

**SHA2**

- Improved version of SHA1, longer hash
- 256 or 512 bits (also called SHA256, SHA512
- Based on SHA-1 it has some of the same weaknesses

**SHA3**

**MD4 and MD5**

- Only useful when we only care about preimage attacks or Integrity

**MD6**

- Seems good and fast