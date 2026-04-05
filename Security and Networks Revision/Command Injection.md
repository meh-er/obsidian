#SaN 

A simple vulnerable PHP example
Backend PHP code --> Takes IP address from user --> Executes ping command on the server -> Displays result in browser

```
<?php
$ip = $_GET['ip'];

/* attempt to sanitise input */
$ip =  str_replace(";", "", $ip);
$ip = str_replace("&", "", $ip);

$output = shell_exec("ping -c 4 ", $ip);
echo "<pre>$output</pre>";
?>
```

Why is this vulnerable?
- User input is directly concatenated into a shell command:
`shell_exec("ping -c 4 " . $ip);`
- The system sees:
`ping -c 4 [USER INPUT]`
- If attacker enters:
`8.8.8.8; cat /etc/passwd`
- The server executes:
`ping -c 4 8.8.8.8; cat /etc/passwd`


 ### Input Sanitization
 - Removing or filtering dangerous characters
 - Trying to make input "safe" before using it
 - Attempts to prevent multiple command execution by removing common command separators such as ; and &
 - Blacklisting characters doesn't work - cannot predict every possible attack variation. Attackers only need one bypass

### Shell
Interprets:
- Quotes
- Variables
- Subcommands
- Encodings
Simple string replacement is not real security
### Effective Solutions
- Strong input validation (whitelisting)
- Instead of blocking bad characters: allow only valid format.
- This ensures only legit IP addresses are accepted.
- filter.var() checks whether the input is a valid IP address format.

**Summary**
- Treat all input as untrusted
	- User input = attacker-controlled input.
- Prefer whitelisting over blacklisting
	- Allow known-good input
	- Don't try to block bad input
- Minimise use of system commands
	- Every call to system(), exec(), shell_exec() increases risk
- Principle of least privilege
	- Reduce impact of compromise: even if exploited, the server process should have minimal permissions.
 
 