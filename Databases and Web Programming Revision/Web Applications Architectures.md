#DAWP 

- Web Clients
	- FireFox, Safari, Edge, curl, some beds
	- Connects to a HTTP server & interprets HTTP, HTML, REST
- Web Servers
	- Cloud Virtual Machine (VM) vs self-hosted
	- Essentially: computer with a public IP address, open ports
	- Runs our web server and web applications

### Dynamic Web via MVC Frameworks
- Model/View/Control
- Model: data and business logic
- View: presentation of HTML templates with dynamic placeholders
- Controllers: links the models and view, calls code executed on server (php, python, JSP)
- Hardcoded depdendency frontend to backed: difficult to change/add frontends

### Dynamic Web via [[REST]] Frameworks
- Strongly **separate data & presentation**: backend for data & logic only
- **REST:** REpresentational State Transfer protocol for JSOn data
- **CRUD:** GET (read), POST (create), PUT/PATCH (update), DELETE
- **One REST API for:** Web browsers, Mobile app, external integrations
- **Resource-Oriented Design:** each entity = resource (user, item, order)
- **micro services:** separate server for each entity/resource (user, item)
- Standard: scalable architectures with multiple frontends


**Tech stacks - **∞, SpringBoot/Java, Postgres/SQL, Angular/TS