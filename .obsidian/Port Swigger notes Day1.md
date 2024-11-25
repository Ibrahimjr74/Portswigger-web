- Some Types of Vulnerability labs that are found most in Portswigger.
     - Common types of injections (xss,SQL Injection, SSRF ... etc)
     - File upload
     - Business Logic
     - Broken Access control
     - Directory traversal
- Attacking CMS(Content management System).
- Deep web Reconsence(subdomain,content Discovery,DNS Reconsence )
- Web Assesment tool(nuclie, nessus, nikto)

##### Hackers different attacking methodology
- zseano methodology
- jason haddix methodology
- 





# SQLi
- is a type of vulnerability that allows the hacker to interfere with queries that the application makes to its database.
-  a success full SQLi can lead to the following breaches like:
		- Passwords
		- Credit cards
		- Personal user information
## How to detect SQL injection vulnerabilities
- we typically submit the  ' sign and wait for error response
## SQL injection in different parts of query
- Most SQL injection vulnerabilities occur within the `WHERE` clause of a `SELECT` query.
 Some other common locations where SQL injection arises are:
- In `UPDATE` statements, within the updated values or the `WHERE` clause.
- In `INSERT` statements, within the inserted values.
- In `SELECT` statements, within the table or column name.
- In `SELECT` statements, within the `ORDER BY` clause.
##### TO do so
we first open burpsuite and intercept the connection change the query we want and forward it .