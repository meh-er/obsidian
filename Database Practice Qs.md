#DAWP 

## Scenario 1
You are designing a database for a local clinic. You have two tables:
- Doctors (DocID, DocName, Specialty)
- Patients (PatientID, PatientName, Age, AssignedDocID)

1. **Write the SQL statement to create the Doctors table. Ensure that DocID is teh PK, the DocName cannot be left blank, and the Specialty defaults to 'General Practice' if nothing is entered**

- **My Answer:** `CREATE "Doctors" (DocID  Integer (PK), DocName varchar NOT NULL, Specialty varchar DEFAULT (General Practice)`
- **Correct:** 
```
CREATE TABLE Doctors (
	DocID INT PRIMARY KEY,
	DocName VARCHAR(100) NOT NULL.
	Specialty VARCHAR(100) DEFAULT 'Genera; Practice'
);
```


---

2. **Write an SQL query to retrieve the names of all patients alongside the names of their assigned doctors. The final list should be displayed in alphabetical order based on the patients name.**

- **My Answer**: `SELECT (Doctors.DocName, Patients.PatientName UNION Patients.AssignedDocID=Doctors.DocID FROM Patients, Doctors ORDER BY PatientName`
- **Correct**: 

```
SELECT d.DocName, p.PatientName
FROM Patients p
JOIN Doctors d ON p.AssignedDocID = d.DocID
ORDER BY p.PatientName;
```
---

3. **The clinic wants a report showing how many patients are assigned to each doctor. Write an SQL query that displays the DocID and the total count of patients assigned to them**

- **My Answer**:  `SELECT COUNT(PatientID), AssignedDocID FROM Patients GROUP BY AssignedDocID`

- Correct, formatted better below:

```
SELECT AssignedDocID, COUNT(PatientID)
FROM Patients
GROUP BY AssignedDocID
```
---

4. **Write an SQL query to add a new constraint to the existing Patients table to ensure that no two patients can have the exact same PatientID**

Correct answer:
```
ALTER TABLE Patients
ADD PRIMARY KEY (PatientID);
```

---

---

## Scenario 2
- Members (MemberID, FirstName, LastName, JoinDate)
- Classes (ClassID, ClassName, TrainerName, Capacity)
- Bookings (BookingID, MemberID, ClassID, BookingDate)

1. **Write the SQL to create the Bookings Table: Booking id is a primary key, memberid and classid are foreign keys, booking date defaults to current date**

-  Answer:
```
CREATE TABLE Bookings (
		BookingID INT PRIMARY KEY),
		MemberID INT,
		ClassID INT,
		BookingDate DATE DEFAULT CURRENT_DATE,
		FOREIGN KEY (MemberID) REFERENCES Members(MemberID),
		FOREIGN KEY (ClassID) REFERENCES Classes(ClassID)
	);
```



---
2. **Write an SQL query to list all ClassNames asnd the lastname of every member who has booked into that class. Sort the results alphabetically by the Classname, if a class has multile people, the last names should be sorted alphabetically within that class**

- My answer:
```
SELECT c.ClassName, m.LastName
FROM Classes c
JOIN Bookings b ON c.ClassID = b.ClassID
JOIN Members m ON b.MemberID = m.MemberID
ORDER BY c.ClassName ASC, m.LastName ASC
```




---
3. **The Manager wants to know which classes are actually being used. Write a query that shows the ClassName and the total number of bookings for each class, but only include classes that have more than 5 bookings**
- My response:
```
SELECT c.ClassName, b.COUNT(BookingID) AS TotalBookings
FROM Classes c
JOIN Bookings b ON c.ClassID = b.ClassID
GROUP BY c.ClassName
HAVING COUNT(b.BookingID) > 5;

```

---
4. **Write an SQL statement to add a CHECK constraint to the existing Classes table to ensure that Capacity is always greater than 0**
- Answer
```
ALTER Classes
ADD CONSTRAINT Pos CHECK (Capacity < 0);
```


---

---

## Scenario 3
- Movies (MovieID, Title, Genre, ReleaseYear, DirectorID)
- Directors (DirectorID, DirectorName, Nationality)
- Reviews (ReviewID, MovieID, Score (1-10))

1. **Write a query to find the DIrectorID and the total number of movies they have directed. Only display the directors who have directed more than 2 movies**
Answer:
```
SELECT d.DirectorID, COUNT(m.MovieID)
FROM Directors
JOIN Movies m ON d.DirectorID = m.DirectorID
GROUP BY DirectorID
HAVING COUNT(m.MovieID) > 2;
```


---
2. **Write a query to list the movietitle, directorname, and average score**
Answer
```
SELECT m.Title, d.DirectorName, AVG(r.Score) 
FROM Movies m
JOIN Directors d ON m.DirectorID = d.DirectorID
JOIN Reviews r ON m.MovieID = r.MovieID
GROUP BY m.Title, d.DirectorName;
```


---

3. **Write a query to show the Genre and the Average Score for that genre. Exclude movies released before 2000, only show genres if their average score is > 7**
Answer
```
SELECT Genre, AVG(Score)
FROM Movies m
JOIN Reviews r ON m.MovieID = r.MovieID
WHERE ReleaseYear >= 2000
GROUP BY Genre
HAVING AVG(Score) > 7;
```


---
4. **Write the create statement for the reviews table - add a check constraint to ensure the score is never higher than 10, and a constraint so that if a movie is deleted, all its reviews are deleted too**
Answer:
```
CREATE TABLE (
	ReviewID INT PRIMARY KEY,
	MovieID INT,
	Score INT CHECK (Score <= 10),
	FOREIGN KEY MovieID REFERENCES Movies(MovieID) ON DELETE CASCADE,
	);
```


---
---

# PART 2
## Scenario 1
A bakery uses a single, massive spreadsheet to track its wholesale orders. The columns are: `OrderID, Date, RestaurantName, RestaurantAddress, DeliveryDriver, ItemBaked, Quantity`

1. **The bakery decides to stop making "Sourdough Loaves". They delete every row in the spreadsheet where `ItemBaked` is "Sourdough Loaves". However, it turns out "The Corner Cafe" had only ever ordered Sourdough. What specific anomaly just occurred, and what data was lost?**
Answer: Lost a customer idk bro

--- 




### **art 2: Database Anomalies**

**Scenario B:** A bakery uses a single, massive spreadsheet to track its wholesale orders. The columns are: `OrderID`, `Date`, `RestaurantName`, `RestaurantAddress`, `DeliveryDriver`, `ItemBaked`, `Quantity`

**Question 5:** The bakery decides to stop making "Sourdough Loaves". They delete every row in the spreadsheet where `ItemBaked` is "Sourdough Loaves". However, it turns out "The Corner Cafe" had only ever ordered Sourdough. What specific anomaly just occurred, and what data was lost?

**Question 6:** "Bistro 99" moves to a new location. The bakery manager updates their `RestaurantAddress` on the most recent order row, but forgets to update it on their 50 previous past orders. What specific anomaly is this, and why is it a problem?

**Question 7:** The bakery hires a new delivery driver, Sarah, but she hasn't been assigned to any orders yet. The spreadsheet uses a composite primary key made of (`OrderID`, `ItemBaked`). Why can't the manager add Sarah to the spreadsheet yet, and what is this anomaly called?

---

---
# Normalisation
A
**partial** dependency -  depend on whole **primary** key 

1NF - all values are atomic

x relies on y, and y relies on z, so therefore x should rely on z - **relies on smth other than a key column**

EmployeeID
2NF - there r transitive dependencies (deplocation depends on smth other than pk)

1NF - atomic, no repeats

| StudentID | Studentname | CourseID | CourseName | Instructor | InstructorEmail | Grade |
| --------- | ----------- | -------- | ---------- | ---------- | --------------- | ----- |
| S1        | Alice       | C101     | Math       | Dr.Smith   | smith@uni.edu   | A     |

**Already in 1NF**
2NF - partial dependencies - dependent on whole pk
3NF - no transitive dependencies

| StudentID | StudentName |
| --------- | ----------- |
| S1        | Alice       |
| S2        | Bob         |

| CourseID | CourseName | Instructor |
| -------- | ---------- | ---------- |
| C101     | Math       | Dr. Smith  |
| C102     | Science    | Dr. Jones  |


| Instructor | InstructorEmail |
| ---------- | --------------- |
| Dr Smith   | smith@uni.edu   |
| Dr Jones   | jones@uni.edu   |


| CourseID | StudentID | Grade |
| -------- | --------- | ----- |
| C101     | S1        | A     |
- Deletion anomaly
- 3NF -> no x that is reliant on smth taht isnt a key


| EmpID | ProjectCode | EmpName | ProjectManager | HoursLogged |
| ----- | ----------- | ------- | -------------- | ----------- |
| E01   | P-ALPHA     | Dave    | Sarah          | 12          |
| E02   | P-ALPHA     | Anna    | Sarah          | 8           |
| E01   | P-BETA      | Dave    | John           | 15          |
|       |             |         |                |             |
 - in 1NF as no repeats, atomic
 - 2NF: reliant on whole PK: empid+ project code

| EmpID | EmpName | HoursLogged |
| ----- | ------- | ----------- |
| E01   | Dave    |             |
| E02   | Anna    |             |

| ProjectCode | ProjectManager |
| ----------- | -------------- |
| P-ALPHA     | Sarah          |
| P-BETA      | John           |

| EmpID | ProjectCode | HoursLogged |
| ----- | ----------- | ----------- |
| E01   | P-ALPHA     | 12          |
| E02   | P-ALPHA     | 8           |
| E01   | P-BETA      | 15          |
3.

OrderID | OrderDate | CustomerID | ShippingCost

CustomerID | ShippingCost

ShippingCost | ShippingCost

