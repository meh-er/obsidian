### SQL
Template
```
CREATE TABLE TableName (
	id INT PRIMARY KEY,
	name VARCHAR(255),
	value DECIMAL(10,2).
	FOREIGN KEY (other_id) REFERENCES OtherTable(id)
);
```

Aggregation
```
SELECT column, SUM(column2)
FROM table
GROUP BY column
HAVING SUM(column2) > value
ORDER BY SUM(column2) DESC;
```

### Web/API
- REST uses nouns not verbs
- Endpoints should represent **resources**

Endpoints:
- POST /api/resource
- GET /api/resource
- PUT /api/resource/{id}
- DELETE /api/resource/{id}

Authentication = verifying identity
Authorization = checking permissions

##### JWT
[[JWT]] contains: 
- user ID
- roles/perms
- expiry time

### Debugging
Backend:
- Wrong query/ empty database
- Incorrect filtering logic

Frontend
- Data not rendered properly