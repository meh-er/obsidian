# 2
findById() - find the name of something by its id - when id is a pk
getReferenceById()  - get a referernce to something in another table by its id - when id is a fk

findById() vs getReferenceById()
queries DB and returns optional vs lazy proxy
# 3
@Entity 
- so that JPA can know it is a persistent entity method as an entity
- if no name specified then inherits table's name

@Table
- if entity name and table name are different, this will be table name
- Can also specify the schema used - good for differentiating  different sets of tables

@Id
- defines the primary key in the table

@GeneratedValue
idk yet

# 4
Auto inherits 
**JPA maps the field to a column with the same name by default**

# 6
v1/ap/wtv

- Headers
- URL
- Controller mapping

# 7
motherfucking **requestmapping**
@Deprectated("/api/v1/orders")
@Restcontroller("/api/v2/orders")

# 8
Content-Type: application/api/v2/+.json

# 9 
Still works with older versions of the API

# 10
Deprectation is when an api has become obsoete - need warnings and a replacement to developers ASAP
Can be communicated through headers or @Deprecated

