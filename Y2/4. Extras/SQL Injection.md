#Theory #SaN 

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

**Typical vulnerability in PHP code**

```
$username = $HTTP_POST_VARS['username'];
$password = $HTTP_POST_VARS['passwd'];

$query = "SELECT * FROM logintable WHERE user = '" . $username . "' AND pass = '" . $password . "'";


$result = mysql_query($query);

if (!$results)
die_bad_login();
```

Best defences are:
- Use of Prepared Statements (with Parametrized Queries)
- Use of Properly Constructed Stored Procedures
- Allow-list input Validation

Network vs Local Injections
- Network is usually considered the bigger risk:
	- Access by many, unknown users
	- Network is a gateway, crossing physical boundaries
	- Risk in privileged servers (setuid, etc)
- **Local** inputs: should they be considered
	- Local users can only deny access to themselves
	- Desktop apps run as a plain user, only risking their own data
However, this trust assumption can be wrong:
- *Drive-by-exploits* attack locally (or use escalation)
- Growing concerns over *insider threats*


### Common Injections
https://portswigger.net/web-security/sql-injection/cheat-sheet

![[Pasted image 20260315163041.png]]
![[Pasted image 20260315163323.png]]


' OR 1=1 --
Can be used in:
- Login Forms
- Search Bars
- URL parameters (e.g. `www.store.com/item?id=5 OR 1=1`)
- Contact Forms

#### Injection Routes
- **user input** e.g. web forms via HTTP GET or POST
- **cookies** used by web apps to build queries
- **server variables** logged by web apps (e.g. HTTP headers)
- **second-order injections** where the injection is separated from attack

**Primary Motives**
- Extracting data
- Adding or modifying data
- Mounting a denial-of-service attack
- Bypassing authentication
- Executing arbitrary commands
**Auxiliary Motives**
- Finding injectable parameters
- Database server fingerprinting
- Finding database schema
- Escalating privilege at the database level

### Forms of SQL Code Injected
1. Tautologies
2. Illegal/incorrect queries
3. Union query
4. Piggy-backed queries
5. Inference pairs
6. Stored procedures and other DBMS features

Additionally, the injection may use **alternate encodings** to try to defeat sanitation routines that don't interpret them 

#### Tautologies
Inject code into condition statements so they always evaluate to **true**
```
SELECT accounts FROM users WHERE
login='' or 1=1 AND pin=
```

#### Illegal/Incorrect Queries
Cause a run-time error, hoping to learn information from error responses.

```
SELECT accounts FROM users WHERE
login='' AND=pin=convert(int,(select top 1 name from sysobjects where xtype='u'))
```

- Assumes MS SQL Server
- sysobjects is a server table of metadata
- Attempts to find first user table
- Converts name into an integer -> runtime error

#### Union Query
Inject a second query using UNION:

```
SELECT accounts FROM users WHERE
login='' UNION SELECT cardNo from CreditCards where acctNo=10032 -- AND pin=
```

Effect
- Suppose there are no tuples with login=''
- May reveal cardNo for account 10032

#### Piggy-Backed Queries
```
SELECT accounts FROM users WHERE
login='doe'; drop table users -- 'AND pin='
```

- Database parses second command after;
- Executes second query. deleting users table
- Some servers don't require the ; character!

#### Inference Pairs
Even if error responses are **not** visible to the client, information can still be extracted by observing subtle differences between outputs.
**Two common techniques**
- **Blind Injection** - exploits visible differences in responses
- **Timing Attack** - exploits variations in response time based on boolean conditions (e.g. using WAITFOR)
With unlimited access, these techniques allow automated differential analysis.

**Blind Injection Example**
Discover whether the login parameter is injectable
**Step 1**: Always true
`login='legalUser' and 1=1 -- '`
Response: Invalid Password

**Step 2**: Always false
`login='legalUser' and 1=0 --'`
Response: Invalid Username and Password

means login parameter is injectable!

#### Stored Procedures
Stored procedures are custom sub-routines that provide support for additional operation.
```
CREATE PROCEDURE DBO.isAuthenticated
@userName varchar2, @pin int
AS
EXEC("SELECT accounts FROM users WHERE login='" +@userName+ "' and pass='" + @pin+ "' ");
GO
```

Risk: if improperly sanitized, can allow SQL injection inside the stored procedure


##### How to Prevent Vulnerabilities
Choice of stages (as usual):
1. **Eliminate before deployment**:
	- Use programming language support; object-relational mapping (ORM)
	- Manual code review or automatic static analysis
2. **In testing or deployment:
	- Pen testing tools
	- Instrumented code
3. **After deployment**:
- Wait until attacked, manually investigate
- Use dynamic remediation plus alarms (app firewall or specialized technique)