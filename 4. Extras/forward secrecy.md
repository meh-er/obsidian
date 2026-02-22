#Theory 
A protocol has forward secrecy if it keeps the message secret from an attacker who has:
- A recording of the protocol run
- The long-term keys of the principals
If an attacker records your encrypted traffic and steals your private key in the future, forward secrecy ensures that they still can't decrypt the old traffic.
Example of this is [[Diffie-Hellman]]