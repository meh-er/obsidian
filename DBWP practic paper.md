# 1
## a

```
CREATE TABLE Employees (
	employee_id Int PRIMARY KEY,
	email varchar(255) UNIQUE,
	salary Int, 
	department String NULL,
	CONSTRAINTS salary > 0, )
```

## b
### i
- SeatNumber is dependent on FlightNumber
- Passenger is dependent on BookingID
### ii

- Not in 3NF - 3NF is defined as no transitive dependencies + in 2NF, i.e. no columns are dependent on anything other than the Primary Key
- The SeatNumber is reliant on the flightNumber, which is not the primary key of this table, so it should be split into a separate table along with destination. BookingID should only contain passenger name and flightnumber as a FK
## c
### i
Given: 
Sales(SaleID, ProductName, Quantity, Price)
```
SELECT ProductName, SUM(Price) 
FROM Sales
GROUP BY ProductName
```

### ii
```
SELECT ProductName
FROM Sales
WHERE SUM(Price) > 500
ORDER BY SUM(Price)
```

# 2
## 1
### a
- You should not have a /create endpoint, it should just be users
- You should have a noun not a verb or sentence in the endpoint name, again should just be users

### b
- /api/users/
- /api/users

## 2
### a
This method returns products with a price greater than the minimum given

### b
Layers: Application, Service, Repository, Database

Repository?

## 3
### a
- Session-based authentication involves usage of a cookie or session id to verify the device for the length of a 'session'. You are not really given specific perms based on your auth?
- Token-based authentication can be used to authenticate the user rather than the device since you can manually input this

### b
- More secure, sids can be stolen

# 3
## 1
### a
POST
PUT/PATCH (partial vs full update)
DELETE

### b
idk i need to revise this


### c
Gves user insight into what is happening behind the scenes so they know why the error occurs

## 2

Member:name, email,
Class:title, instructor

Relationship OneToMany {
	Member{class} to Class{member}
}

## 3
idk bro
