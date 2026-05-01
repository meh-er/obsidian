
# 1
## a
CREATE Products (ProductID Int PRIMARY, ProductName String Required, category Category, Price Float, Stock Int)

CREATE enum Category (Accessories, Display)

## b
### i
Deletion Anomaly - If you delete a user you could be deleting a whole model of cars as they are reliant
Insertion Anomaly - have to insert the same user's details multiple times

### ii
1NF: no repeats, atomic, 
2NF: relies on whole PK
3NF: no transitive dependencies

Booking: ID (PK),  cID (FK), CarModel, RentalDays, DailyRate
Customer: cID (PK), CustomerName, CustomerEmail

## c
### i
SELECT c.Name, o.OrderDate, o.TotalAmount
FROM Orders
JOIN Customers ON o.CustomerID = c.CustomerID

### ii
SELECT TotalAmount FROM Orders GROUP BY OrderDate ASC HAVING count(TotalAmount) < 100

# 2
## 1
### a
The first endpoint is a path variable - meaning it will return the song associated with that id
The second endpoint is a query parameter - meaning that it will only return songs that meet the parameters, i.e. have a genre of jazz

### b
1. APpropriate for users looking for a specific song/note/student
2. Appropriate for users looking for a range of results e.g. students in one specific class

## 2
### a
This will return a list of users that meet the minimum requirement of having an age over whatever the given age that is input. - filters out users who don't meet that
Spring automatically implements it as boilerplate idk

### b
uh

## 3
### a
Authentication - Identifying who the user is
Authorization - Identifying what a given user is permitted to do - e.g. role based access

### b
Authorisation fails - you have authorised the user to be able to access other people's work
Backend could prevent this by implementing tighter access controls and the idea of **least privilege** - only given the perms needed to carry out what you are allowed


# 3
## 1
### a
entity Order {
	orderNumber String required,
	 totalPrice Double,
	 orderDate Instant
}

### b
orderNumber String required max(20)

### c
relationship ManyToOne {
	Order{user} to User{order(orderNumber)}
}

## 2
### a
curl -X DELETE http://localhost:8080/api/orders/900
### b
403  forbidden access?

## 3
### a
Use full numbers (change endpoints to api/v2/orders)

### b
Deprecated?

### c
Warnings when used / at tuntime
