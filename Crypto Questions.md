1. What is the use of SUID and GUID?
		Saved User ID: Saves the 'Effective UID (EUID)' when it was executing a process, useful for logs where you want to know what permissions a user had at a given moment.
		Global User ID: Used as a wisder user id that persists through the entire account and doesn't change.
2. N/A
3. Suppose you are designing a linux shell program that would involve a login/password based access control. Assuming you have root access, what should you do to ensure security from probable trojan password capture programs?
		You should not be logged in to root access as much as possible, so that there are limited times where you can have your password stolen, update firewall to check for malicious programs, need sudo before executing any important processes. 
4. Suppose a password hashing does not involve salt. What could be the security vulnerabilities.
		No element of randomization which means passwords may match rainbow tables if common. Attackers who find these hashed passwords without salt could compare them to other known passwords and their hashes (rainbow table) and figure out what the password means.
5. Suppose h is a preimage-resistant and collision hash function. I construct another function such that H(x) = h(x)||x where || is the concatenation operation. Is H collision resistant? Is H preimage resistant?