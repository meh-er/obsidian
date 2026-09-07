#Theory 

The `Host` header is a common target for injection attacks because many applications use it to **construct URLs**, generate links in emails, and set cookie domains. If an application blindly trusts the `Host` header without validation, an attacker can manipulate it to redirect users to malicious sites or poison password reset links.

**Password reset poisoning** is the most well-known attack. When a user requests a password reset, the application generates a rest link using the `Host Header`. 
`https://{req.headers.host}/reset?token=abc. 
An attacker who can control the `Host` header (e.g. sending request directly to server's IP address with custom header) can make the reset email contain a link to their own domain. When the victim clicks the link. the attacker captures the reset token. 
The defense is straightforward: never use the `Host` header to construct URLs in security-sensitive contexts. Instead, use a configured `BASE_URL` environment variable or a hardcoded domain. Validate the `Host` header against an allowlist of known domains and return 400 for unrecognised values.