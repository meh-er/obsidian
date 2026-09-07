# Q1
## a)

```
CREATE TABLE Books (
	book_id INT PRIMARY KEY,
	title String,
	author String,
	price Float,
	stock Int
	CHECK price > 0
	CHECK stock > -1
)
```

## b)
### i)
1. It has repeated information - e.g. CustomerName and Email, eventName and EventLocation
2. It would cause anomalies - e.g. if Bob Jones got deleted, Concert B would also be completely removed from the system as it's all in one table.

### ii)
Normalise this table into 3NF:
Reminder: 1NF = no repeats, atomic, pk
2NF = no composite PK, 1NF
3NF = no transitive dependencies, 2NF

Tables
Bookings: BookingID (PK), CustomerEmail (FK), EventName (FK)
Customers: CustomerEmail (PK), CustomerName
Event:  eventName(PK), EventLocation, TicketPrice

- ticketprice and eventlocation are reliant on pk event name
- customername is dependent on email
- bookings joins the other two together to represent single orders

## c)
### i)
```
SELECT customer_id, AVG(total)
FROM Orders
```
### ii)
```
SELECT customer_id, AVG(total)
FROM Orders
HAVING AVG(total) > 100
```

# Q2
## a)
### i) 
According to good REST API design, GET should be stateless and not make changes, but only return a response from the server to the client for the requested information. 

### ii)
The method used should be POST, which should send the sensitive data across to the server to in this case create a new user account.

## b)
### i)
Controller - controls the REST API responses for an associated class. For example, a StudentController would contain the @GetMapping and @PostMapping methods etc for a Students class. 
Service - contains the business logic for the application, for example the student's personal information that is being added
Repository - where the database is accessed, often using JPA. This will be involved in spinning up the database and updating the tables and sequences within as well as getting information from it. 


### ii)
Putting the logic inside the controller may cause security violations or complications with updating as the program will no longer be object oriented.

## c)
### i)
By enforcing role-based access, a system will ensure that only users with the given admin role have the associated privileges in the system, separating them from regular users. By implementing this to the role rather than individual, it minimises the room for error e.g. by giving the wrong user privileges.

### ii)
If not implemented properly, an attacker could use privilege escalation to modify parts of the system they shouldn't have access to, for example if they had a regular user account and there was a broken access control, they may be able to delete other people's bookings.

# Q3
## a)
### i)
- GET api/books
- POST api/books/borrow
- PUT api/books/return

## ii)
- Get | Post | Put

### iii)
could use 409 - conflict


## b)

1 user can have multiple orders
1 order can have 1 user
user is FK on orders

1 order can have multiple products
1 product can have multiple orders

Tables
Users: uid (PK), username, useremail
orders: oid (PK), uid (FK), pid (FK), cost
Products: pid (PK), pname, price

Relationships
relationship ManyToMany {
	Orders{Products(pid)} to Products{Orders(oid)}
}

relationship ManyToOne {
	Orders{Users(uid)} to Users{Orders(oid)} with BuiltInUserEntity
}


## c)
### i)
- Database cannot find that resource
- Wrong table?

### ii)
- If database can't find resource can add more code to instead create it partially??

### iii) 
Unsure -  the console on the website will show you the HTTP error codes.