#DAWP 

JHipster generates templates of **modern, production-ready apps**
- **Boilerplate**: sections of code that are repeated in multiple places with little/no variation.  Provides a standardized set of code or configuration files. Aims to save time by reducing setup tasks and ensuring consistency across projects.
- Includes admin interface, supports micro services, monoliths
- Spring Boot: Simplifies boilerplate via auto-configs, embedded servers, and pre-built components for quicker development.
- JHipster: Reduces boilerplate even more by generating entire Spring Boot-based applications with pre-configured settings, databases, and UI.
- Follows industry standards, saves hours, includes REST server CRUD UI, login and admin UI
### Technology stack on the client side
Single Web application:
- Angular or React or Vuew
- Responsive Web Design
- HTML 5 Boilerplate
- Compatible with modern browsers
- Full internationalization for CSS design
- Optional WebSocket support with Spring Websocket

### Technology stack on the server side
A complete Spring application:
- Spring Boot for application configuration
- Maven or Gradle configuration for building, testing and running the application
- 'development' and 'production' profiles (both for Maven and Gradle)
- Spring Security
- Spring MVC REST + Jackson
- Database updates with Liquibase
- Elasticsearch support if you want to have search capabilities on top of your database

#### Backend Tech
- Java/[[Spring Boot]]: classes, program logic, respond to requests via **REST**
- [[Hibernate]]/[[JPA]]: **Object Relational Mapping** SQL rows to Java objects
- [[Liquibase]]: **database changesets** to create/evolve the database schema
- FakerJS: random **dummy data** to populate our application
- Swagger: **Interface and documenting** our REST APi
- Authentcation and Authorisation: JWT, OAuth, tokens for REST
- CI/CD: for continuous integration and deployment to a **cloud/VM**
- Docker: to package our app to **easily run anywhere** and deploy.

#### Dev commands
- `jhipster`: generate new JHipster application. 
- `jhipster ci-cd`: generate a ci and cd pipelines JHipster answer questions about type of ci pipeline needed
- `jhipster jdl myapp.jdl`: generate all the entities and relationships specified in `myapp.jdl`
- `jhipster entity`: Generates a single new entity along with associated files: entity classes, database migration scripts, REST API endpoints, and Angular/React components

#### run commands
- `./mvnw`: Runs the application in development mode (port 8080)
- `npm install`: installs node needed packages
- `npm start`: starts front end only (port 9000)

