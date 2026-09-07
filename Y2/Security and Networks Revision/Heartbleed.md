#SaN 


### The Heartbeat Extension
- Allows clients and servers to check if the connection is still open.
- Works by sending a small request and expecting the same response.
- Meant to prevent unnecessary re-nogation in TLS.

**Normal Heartbeat Exchange**
1. **Client** -> **Server** `HeartbeatRequest` ("hello", length=5)
2. **Server** -> **Client** `HeartbeatResponse`("hello", length=5)

**The Exploit**:
1. **Client** -> **Server** `HeartbeatRequest`("hello",length=**64KB**)
2. **Server** -> **Client** `HeartbeatResponse`(**Leaked memory up to 64 KB**)

- OpenSSl did not verify that the **length** field matched the actual data size.
- This meant the server would copy and send **whatever was in memory** up to 64KB.
- Attackers could repeatedly send malicious requests to **extract private keys, passwords, etc**

### Defences
1. **Proper Bounds Checking**
	- The length field must be checked against actual input size
	- If the length is greater than provided data, reject teh request
2. **openSSl Patch**
	- OpenSSL 1.0.1g introduced proper bounds checking
	- Disabled heartbeat extension unless explicitly enabled.
3. **Industry Response**
	- Websites had to revoke compromised certificates.
	- Users were advised to change passwords
	- Organizations moved away from OpenSSL.