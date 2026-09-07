#DAWP 

- For entities (like Customer, Product), fields +types (price, name) and relationships between entities.
- Human-readable, visual and separate from the code
- **Generates app template**: JHipster auto generates [[Spring Boot]] classes, REST, database migration scripts, UI.
- **Also has**: app config, scroll, pagination or service layers, dto
- **The JDl file serves as central, documented blueprint for the entire data model**.

#### What is an Entity
- **In the Problem Domain**: An entity is a *type* or *domain concept* or *business object*
- **In the Database**:
	- A **JDl entity** maps directly to a SQL **table:**
		- Each **JDL field** becomes a **column** in that table.
		- Each **row** in that table is **an object of that type**
- **Backend:** [[Spring Boot]], database read/write, and REST API
- **Frontend and CRUD:** Angular compnents - views to create/edit/delete items

- `jhipster`: generate a new JHipster application. Answer questions about type of application, auth method, database, etc.
- `.mvnw`: start the JHipster application
- `jhipster jdl myapp.jdl`: generate all the entities and relationships specified in myapp.jdl
- `jhipster entityName:` Generates a single new entity along with associated files: entity classes, database migration scripts, REST API endpoints, and Angular/React components.

### Renegenerating from JDL
- JDL generation is generally one way
- Add entity or field: use jhipster jdl or jhipster entity command to modify entities e.g. to add an attribute
- Rename or remove entity, field or relationship: re-start from template:
	- Re-apply previous commits or files changed
	- Set jhipster command not to overwrite specific files.
	- Alternative: update only the entity with changes by running jhipster entity
	- **If an Entity changes**:
		- Use the jhipster entity EntityName command and the review the prompts about changes.
	- Rerunning JDl generation: can **overwrite custom code changes**
	- **If the JDL changes:**
		- Simple* changes to entities
		- Edit the JDL (`*`e.g. add a new entity, field or relationship)
		- Run: jhipster jdl
		- Interactively: either overwrite all files or keep some modified files.
		- Help and diff commands are very useful to find out what changes will be made