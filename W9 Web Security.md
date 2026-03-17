#SaN 

SQL Injections are not beaten by rust :)

Avoiding SQLI:
- Use prepared statements
- Use frameworks - likely to be correct + easier to patch

Phishing protection is important!!
Input validation is useless as attacker can read code and modify it!

- Code that doesn't work in environments has been broken to start with?
- Content-security policy

Padlock on website
- What guarantees a padlock connection? Nobody knows :(
- Belief that padlock offers an assurance of honesty and correctness


### xss
Inject client-side code into web pages viewed by other users
Underlying issue: input/output validation - never trust user's input!!!!!
- **Stored [[XSS]]**
- Reflected [[XSS]] - occurs when injected malicious code is not stored on the server, but is immediately is played on the visited page
#### Session Hijacking with [[XSS]]
document.location.replace => redirect using javascript - redirects victim's browser to attacker's site, passing cookie
Might
also pass currently visited website

### Cookie Authentication
- MAC - shouldn't allow malleability
- Cookie not as good as an encrypted credential, (difficult to revoke but opaque)
- Not as good as plaintext credential with a MAC (difficult to revoke, hard to get right, length extension attacks)
- The old dictum that you should not roll your own crypto
- 

### XSS Protections
- Validate user input (can be beaten very easily)
	- Need to understand data flow through app: quoting, encoding, passed to/from functions, databases etc
- Output filtering
	- Plain output: HTML encoding
		- Stored data values need to be encoded to represent in HTML
	- Marked up output: Encoding + domain specific language (DSL)
		- Use a dedicated syntax (e.g. Markdown) and convert it to a safe subset of HTML
- Use HTTPOnly cookies: [[Cookies]] with HttpOnly flag are not accessible via JavaScrupt, preventing theft via `document.cookie`
- Enable **Content Security Policy**: A strict CSP can prevent inline scripts and limit which domains can be requested.
--> Outsourcing security, assuming the attacker's browser has these things right

Unicode makes everything harder because you need to parse the sequences yourself

### Broken Access Control
- remote users can potentially visit any file on the system
- mistake motivates defence in depth
	- http server should not serve just any file
	- user internal web server condig (Separate apps)
	- and external CS condig (e.g. nobody user, chroot)
	- use of allow-lists (filter inputs against known, safe options)
- A well-written app should only allow access to its own resources.

- Check authorisation again (e.g. does the suer have access to that account)
- Obvious solution but duplicates effort
- **Add a data indirection**
	- Session specific server side array of account numbers
	- Use of databases/hashtables
- Passing potentially unnecessary information to the client  and expecting it unmodified
- 
### Length Extension Attacks
- Truncated hashes are usually more secure, and easier to get right thanf ull length siblings
- If i have secret S and a plaintext P, why is computing SHA512(S,P) dangerous?
- All of the state of a hash funciton is in the hash: the finalise step is just an identity function
- A lot of standard constructions for securin web forms absolutely rely on instead of using SHA512(P,S), but its easy to mess up
- **Best hash is SHA512/256**
- 
- 