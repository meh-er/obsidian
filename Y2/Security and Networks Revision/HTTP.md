#SaN 

HTTP = Hyper Text Transfer Protocol
- Protocol used for web browsing etc
- Specificies messages exchanged
	- Request methods: GET, POST, PUT, DELETE
- Messages are text-based, in lines
- **Stateless** client-side design
	- Quickly became a problem, hence use of cookies
- **client-server** protocol
	- **Client** initiates TCP connection (port 80)
	- **Client** sends HTTP request over connection
	- **Server responds**
		- May close connection
		- Or keep it **persistent** for a short time
	- **Server never initiates a connection**
		- Except in newer HTML5 WebSockets (allows low-latency interactivity)
### Inputs via GET Request
- Input encoded into **parameters** in URL: e.g. `http://www.shop.com/products.asp?name=Dining+Chair&material=Wood`
- **BAD** for several reasons
	- SEO optimization fails: URL not canonical
	- Cache behaviour (not relevant for login)

## GET vs POST
- **GET** is a **request** for information
	- Can be (transparently) resent by browsers
	- May be cachedm bookmarked, kept in history
- **POST** is an **update** providing information
	- Gives impression that input is hidden
	- Browsers may treat it differently
	- **NEITHER provide confidentiality** without HTTPS
- In practice, GET often changes state somewhere
	- User searches for something, gets recorded
	- User has navigated somewhere, gets recorded
- For **sensitive data, always** use POST
	- Helps with confidentiality but not enough alone
- For **large data**, use POST
	- URLs should be short
	- Longer URLs cause problems in some software
- For actions with **major side effects**, use POST
- 