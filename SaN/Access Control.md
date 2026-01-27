---
tags:
  - SaN
  - SaN
---
# Access Control

- Need to ensure that only authorised users have access to what they need

Access:

`User/program/Subject` ⇒ `action e.g. read` ⇒ `resource monitor` ⇒ `object (resource) e.g. file`

### Access Control Matrix

- ACM is a matrix of all principals and objects
- The matrix entries describe the permissions
- Problem: maintaining such a matrix can be difficult
- If the matrix is corrupted, then all control is lost

**Permissions**

- r: read
- w: write
- x: execute/ permission to traverse a directory
- -: none

**File Type**

- -: file
- d: directory
- b/c: device file

### Different User identifiers

- have different uids
    - Real uid `ruid` owner of process
    - effective uid `euid`: used for access checks (Except filesystem)
    - file system uid `fsuid` : used for access checks and ownership of files (usually equal to effective uid)
    - saved suer uid `suid`: when the `euid` is changed, the old `euid` is saved as `suid`. Unprivileged process may change `euid` only to `ruid` or `suid`
- Provides flexibility for granting higher privileges temporarily
    - e.g. daemons: start as root (to bind to ports < 1024), then set `ruid`, `euid` and `suid` to unprivileged values. Cannot gain root privileges afterwards.
    - Process run as privilege user may set `euid` to unprivileged value, then execute non-privileged operations, and gain root privileges afterwards.

### Security issues with granting higher privileges

- Users can run process with more privileges
- If there was a mistake in the passwd program we could use it to do root only actions
- Particular problem: race conditions in code like `if can_acess file then perform_operations on file`
- Make sure process have as low a level as possible!

## Storing Passwords

- passwords not stored in clear text
- Only hashes are stored
- Further security measure: Store pair (Salt, Hash), where Salt is random bitstring, and Hash is the hash of the salt and the password
- ⇒ same password for two users gives rise to different entries in the password file
- Makes cracking passwords much harder

### Windows password Hashes

- Windows stores its password hashes in: `system32/config/SAM`
- This file requires Admin level to read
- It is locked and encrypted with a key, based on other key values (this adds no real security)
- In a Windows Domain, passwords hashes are used to authenticate users on hosts in the domain
- Password hashes are cached to avoid asking for the password
- Gives rise to devastating attack (Pass the Hash)
    - Obtain user credentials for one host in the domain (e.g. phishing)
    - Exploit vulnerability to become local administrator
    - Install process which waits for domain admin to log into this achine
    - Extract cached hash for domain admin
    - Login as domain admin
- Defence mechanisms exist but are painful to use
- `ssh` much better: public key on untrusted machine, private key on trusted machine

### Password crackers

- John the Ripper
    - Most common brute force cracker
    - Open source
- Hashcat
    - Claims to be the fastest/best
- Ophacrack
    - State of thh art, free, rainbow table software

**Phishing:** Username and password captured by attackers via malicious links (e.g. fake bank website)

- Used to login and then for attacks (ransomware, theft of credit card details, IP…..)
- Best protection: MFA (another level of security, e.g. one time password, SMS code, hardware token…)
- `ssh` with public key auth only protects against phishing

### Password Injection

- Want access to the system without cracking the password?
- Have access to the hard disk?
- Add your own account, or replace the hash with one you know

### Better Security: BIOS

- Set a password in the BIOS to stop the computer booting from anything but the hard disk
- It is very hard to brute force the BIOS
- Workaround: remove the hard disk from the computer or reset BIOS password
- BIOS password can be reset by opening the box

### Best Security

- Encryption of important file
- Whole disk encryption
    - Encrypt the whole hard drive
    - Key can be brute forced
    - Not safe if the computer is in sleep mode
- Eg. BitLocker, FileVault, Luks