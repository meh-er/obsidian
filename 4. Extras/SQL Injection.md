#Theory 

Attackers can use SQL Injection on an application if it has dynamic database queries that use string concatenation and user-supplied input. To avoid SQL injection flaws, developers need to:
1. Stop writing dynamic queries with string concatenation
2. Prevent malicious SQL input from being included in executed queries

A common SQL injection flaw in Java is shown below. Because its unvalidated 'customerName' parameter is simply appended to the query, an attacker can enter SQL code into that query and the application would take the attacker's code and execute it on the database.

```
String query = "SELECT acount_balance FROM user_data WHERE user_name = " + request.getParameter("customerName");
try{
	Statement statement = connection.createStatement(...);
	ResultSet results = statement.executeQuery( query );
}
```


Best defences are:
- Use of Prepared Statements (with Parametrized Queries)
- Use of Properly Constructed Stored Procedures
- Allow-list input Validation

