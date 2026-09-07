#DAWP 

When you request a webpage, here's what happens step by step:

#### 1. [[DNS]] Resolution (10-100ms)
Your browser converts the domain name to an IP address.
#### 2. [[TCP]] Connection (20-100ms)
Your browser establishes a connection using the TCP three-way handshake.

#### 3. [[SSL & TLS]] Handshake (50-200ms)
For HTTPS, encryption is negotiated.

#### 4. HTTP Request (1-10ms)
Your browser sends the HTTP request over the encrypted connection.

#### 5. Server Processing (10-1000ms)
The server:
- Parses the request
- Authenticates the user (if needed)
- Retrieves data from databases
- Generates the response
#### 6. HTTP Response (1-50ms)
The server sends back the response with status code, headers, and body.

#### 7. Rendering
Your browser parses HTML, requests additional resources (CSS, JS, images), and renders the page.