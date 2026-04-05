#SaN 

See [[4. Extras/HTTP]].

#### Is the application vulnerable?
- Credentials can be guessed or overwritten through weak account management functions:
	- Default passwords
	- Broken account creation/recovery
- Automated brute-force attacks possible ('credential stuffing')
- Passwords or other credentials are sent over unencrypted connections
- Credentials aren't protected when stored (stolen entrues vulnerable to offline attack)
- Multi-factor (or recovery factor) broken/missing

#### Modern Password Reccommendations
- Avoid passwords if possible
- Don't require rotation unless compromise signs
- Recommend secure storage mechanisms
- Check for weak passwords, use (**sane**) password complexity rules
- Rate-limit logins to prevent automated attacks
- Use **multi-factor authentication** for recovery
