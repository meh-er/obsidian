#SaN #Theory 

HTTP = Hyper Text Transfer Protocol
- Protocol used for web browsing
- Specifies messages exchanged
	- HTTP/1.1 specified in RFC 2616
	- Request methods: GET, POST, PUT, DELETE
- Messages are text-based, in lines
- **Stateless** client-side design
	- Quickly became a problem, hence [[cookies]]
- HTTP is entirely separate from HTML

#### HTTP Communication
HTTP is a **client-server** protocol
- **Client** initiates [[TCP]] connection (usually port 80)
- **Client** sends HTTP request over connection
- **Server** responds
	- May close connection (HTTP 1.0 default)
	- Or keep it **persistent** for a short time
- **Server never initiates a connection**
	- Except in newer HTML WebSockets
	- WebSockets allow low-latency interactivity
	- Upgrade: websocket handshake & switch to WS
	- Expect to see rise in use and security issues!

### HTTP GET Message (FULL)
![[Pasted image 20260315223556.png]]

#### Client != Browser
![[Pasted image 20260315223624.png]]

Referer Header
![[Pasted image 20260315223642.png]]

Inputs via GET Request
- Input encoded into **parameters** in URL

##### GET vs POST
- **GET** is a **request** for information
	- Can be (transparently) resent by browsers
	- May be cached, bookmarked, kept in history
- **POST** is an **update** providing information
	- Gives impression that input is hidden
	- Browsers may treat differently
- **NEITHER provide confidentiality** without HTTPS
	- Plain text, can be sniffed
- In practice, GET often changes state somewhere
	- User searches for something, gets recorded
	- User has navigated somewhere, gets recorded

- For **sensitive data, always** use POST
	- Helps with confidentiality but not enough alone
- For **large data**, use POST
	- URLs should be short
	- Longer URLs should cause problems in some software
- For actions with **major side effects**, use POST