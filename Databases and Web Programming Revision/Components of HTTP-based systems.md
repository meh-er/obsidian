#DAWP

HTTP is a client-server protocol: requests are sent by one entity, the user-agent (or proxy on behalf of it). Most of the time the user-agent is a **Web browser**, but it can be anything. 
Each individual request is sent to a **server** which handles it and provides a **response**. Between the client and the server there are numerous entities, collectively called **proxies**, which perform different operations and act as gateways or **caches** for example.

### Client - The user-agent
The *user-agent* is any tool that acts on behalf of the user. The browser is **always** the entity initiating the request (it is never the server). 

To display a web page, the browser sends an original request to fetch the HTML document that represents the page. It then **parses** this file, making additional requests corresponding to execution scripts, layout information (CSS), and sub-resources contained within the page (e.g. images, videos). The Web browser then combines these resources in later phases and the browser updates the Web page accordingly. 

A web page is a hypertext document. This means some parts of the displayed content are links, which can activated (usually by a click of the mouse) to fetch a new Web page, allowing the user to direct their user-agent and navigate through the web.


### The HTTP Request-Response Cycle
1. **You Make a Request**
	When you click a link or type a URL, your browser creates a HTTP request:
```
GET /products/shoes HTTP/1.1
Host: shop.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html, application/json
Accept-Language: en-US, en;q=0.9
```

This requests says: `Please send me the page at 'products/shoes` from `shop.example.com`

2. The Server Responds
The server processes your request and sends back a response:

```
HTTP/1.1 200 OK
Content-Type: text.html; charset=utf-8
Content-Length: 4523
Cache-Control: max-age=3600

<!DOCTYPE html>
<html> 
<head></head>
<body></body>
</html>
```

The **200 OK** status tells your browser the request succeeded, and the HTML content follows.

3. **Your Browser Renders the Page**
Your browser receives the HTML, then makes additional HTTP requests for images, CSS files, JavaScript, and other resources needed to display the complete page.

### HTTP Methods

| **Method** | **Purpose**           | **Has body** | **Safe** | **Idempotent** (same result when repeated) |
| ---------- | --------------------- | ------------ | -------- | ------------------------------------------ |
| [[GET]]    | Retrieve data         | No           | Yes      | Yes                                        |
| [[POST]]   | Create new data       | Yes          | No       | No                                         |
| PUT        | Replace existing data | Yes          | No       | Yes                                        |
| PATCH      | Partially update data | Yes          | No       | No                                         |
| DELETE     | Remove data           | Optional     | No       | Yes                                        |
| HEAD       | Get headers only      | No           | Yes      | Yes                                        |
| OPTIONS    | Check allowed methods | No           | Yes      | Yes                                        |

### Common Request Header

| **Header**       | **Purpose**                | **Example**                      |
| ---------------- | -------------------------- | -------------------------------- |
| [[Host]]         | Target server              | `Host: api.example.com`          |
| [[User-Agent]]   | Client identification      | `User-Agent: Mizilla/5.0...`     |
| [[Accept]]       | Preferred response format  | `Accept: application/json`       |
| Authorization    | Authentication credentials | `Authorization: Bearer token123` |
| [[Content-Type]] | Request body format        | `Content-Type: application/json` |
| [[Cookies]]      | Session Data               | `Cookie: session=abc123`         |

### HTTP Status Codes
Status codes are three-digit numbers that tell you the result of your request. They're grouped into five catagories

#### 100s: Informational
The server received your request and is processing it.
- **100 Continue** - Keep sending the request body
- **101 Switching Protocols** - Changing to WebSocket
- **103 Early Hints** - Preload resources while waiting

#### 200s: Success
Your request was received, understood, and accepted
- **200 OK** - Request succeeded
- **201 Created** - New resource created 
- **204 No Content** - Success, but no body to return

#### 300s: Redirection
You need to take additional action to complete the request.
- **301 Moved Permanently** - Resource moved forever
- **302 Found** - Temporary redirect
- **304 Not Modified** - Use your cached version

#### 400s Client Errors
Something was wrong with your request.
- **400 Bad Request** - Malformed request syntax
- **401 Unauthorized** - Authentication required
- **403 Forbidden** - You don't have permission
- **404 Not Found** - Resource doesn't exist
- **429 Too Many Requests**- Rate limit exceeded

#### 500s: Server Errors
The server failed to fulfill a valid request.
- **500 Internal Server Error** - Generic server error
- **502 Bad Gateway** - Invalid response from upstream
- **503 Service Unavailable** - Server temporarily overloaded
- **504 Gateway Timeout** - Upstream server didn't respond
