#SaN #Theory 

Some state is highly desirable between requests:
- Remember user's preferences, navigation point,
- Web applications: **user logged in**

However:
- Advertising network **tracking IDs**
- May be shared within websites
- Thus can profile user browsing behaviour
- Hence **compromise privacy**
- Also **risk of theft**
	- If browser/machine compromised or cookies passed

#### Cookies in HTTP Headers
- Specified in RFC265
- Just ASCII plain text
	- Sent by server
	- **Stored in client** (database, filesystem, ...)
	- Returned by client when visiting page again
- Cookies can be set by the server for a particular path/domain
	- Then sent for any page matching
- Multiple cookies may be set and returned
- Cookies may have a **limited lifetime**
	- Set by 'Expires' or 'Max-Age'
	- (Setting expiry date in past deletes it)

#### Setting Cookies
![[Pasted image 20260315234355.png]]

#### Secure Cookies
- Provided the browser **obeys** the **secure** **attribute**, the user agent will include the cookie in a HTTP request only if the request is transmitted over a secure channel (typically [[4. Extras/HTTP]] over [[TLS]]).

#### Expiry Dates
![[Pasted image 20260315234547.png]]

#### Removing Cookies
![[Pasted image 20260315234745.png]]

To remove a cookie, the server returns a **Set-Cookie** header with an expiration date in the past. The server will be successful in removing the cookie only if the **Path** and the **Domain** attribute in the **Set**-**Cookie** header match the values used when the cookie was created.

#### Session Hijacking
Web apps use session IDs as a credential
**If an attacker steals a SID, she is logged in!**
This is **session hijacking**.
Many possible theft mechanisms
- XSS, sniffing, interception
- Calculate, guess, brute-force
- Also **session fixation** 
	- Using the same SID from unauthenticated to logged in
	- Attacker grabs/sets SID before user visits site
##### Defences
Web apps (or frameworks) should implement and discard SIDs if something suspicious happens.
- Link SID to IP address of client
	- Problems if behind NAT, transparent proxies
	- ISP proxy pools mean need to use subnet, not IP
	- Subnet may be shared with attacker!
- Link SID to HTTP Headers, e.g. User-Agent
	- Can be trivially faked, and usually guessed
	- Or captured (trick victim to visit recording site)

Poor Session ID (SIDs) management by:
- Exposing SIDs in the URL (e.g. URL rewriting)
- SIDs are vulnerable to session fixation attacks
- SIDs don't timeout, or sessions/tokens aren't invalidated in logout
- SIDs are weak (small entropy, or predictable)
- Session IDs aren't rotated after a new login.
