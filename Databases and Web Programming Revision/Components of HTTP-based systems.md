#DAWP

HTTP is a client-server protocol: requests are sent by one entity, the user-agent (or proxy on behalf of it). Most of the time the user-agent is a **Web browser**, but it can be anything. 
Each individual request is sent to a **server** which handles it and provides a **response**. Between the client and the server there are numerous entities, collectively called **proxies**, which perform different operations and act as gateways or **caches** for example.

### Client - The user-agent
The *user-agent* is any tool that acts on behalf of the user. The browser is **always** the entity initiating the request (it is never the server). 

To display a web page, the browser sends an original request to fetch the HTML document that represents the page. It then **parses** this file, making additional requests corresponding to execution scripts, layout information (CSS), and sub-resources contained within the page (e.g. images, videos). The Web browser then combines these resources 