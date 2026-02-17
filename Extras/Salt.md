#Theory


In cryptogarphy, a **salt** is random data fed as an additional input to a **one-way function** that **hashes data**, a **password** or **passphrase**. 
Salting helps defend against attacks that use precomputed tables (e.g. rainbow tables), by vastly growing the size of table needed for a successful attack. It also helps protect passwords that occur multiple times in a database, as a new salt is used for each password instance. Additionally, salting does not place any burden on users.

Knowing the salt would not help the attacker.
