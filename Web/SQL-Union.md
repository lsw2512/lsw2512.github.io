---
title: "SQL Union Attacks"
permalink: /SQL-Union/
layout: single
author-profile: true
---

UNION allows you to execute one or more additional SELECT queries, then append this to the original query.

``SELECT a, b FROM table1 UNION SELECT c, d FROM table2``

This SQL query will return a single result set with two columns, containing values from columns a and b in table1 and columns c and d in table2.

For a UNION query to work, two key requirements must be met:
- The individual queries must return the same number of columns.
- The data types in each column must be compatible between the individual queries.

To carry out an SQL injection UNION attack, you need to ensure that your attack meets these two requirements. This generally involves figuring out:
- How many columns are being returned from the original query?
- Which columns returned from the original query are of a suitable data type to hold the results from the injected query?

Determining the number of columns required in an SQL injection UNION attack

There are two effective methods to determine how many columns are being returned. 

The first method involves a series of ORDER BY clauses. You then increment the column index until you get an error.
You will need to beagle to detect a difference in the applications response to infer how many columns are being returned. 

The second method involves submitting a series of UNION SELECT payloads specifying a different number of NULL values:
```
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
Etc.
```
If the number of nulls does not match the number of columns, the database will return an error.

## Notes
The reason for using NULL as the values returned from the injected SELECT query is that the data types in each column must be compatible between the original and the injected queries. Since NULL is convertible to every commonly used data type, using NULL maximises the chance that the payload will succeed when the column count is correct.

On Oracle, every SELECT query must use the FROM keyword and specify a valid table. There is a built-in table on Oracle called dual which can be used for this purpose. So the injected queries on Oracle would need to look like:
``' UNION SELECT NULL FROM DUAL--``

The payloads described use the double-dash comment sequence -- to comment out the remainder of the original query following the injection point. On MySQL, the double-dash sequence must be followed by a space. Alternatively, the hash character # can be used to identify a comment.
https://portswigger.net/web-security/sql-injection/cheat-sheet

Finding Columns with a useful data type in an SQL injection UNION attack
After finding the amount of columns in the table, you need to determine which is compatible with the data type you want to extract, these are usually in format string.

You can probe each column to test whether it can hold string data by submitting a series of UNION SELECT payloads that place a string value into each column in turn. For example, if the query returns four columns, you would submit:
' UNION SELECT 'a',NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL--
' UNION SELECT NULL,NULL,NULL,'a'--

If the data type is not compatible, you will get an error.
 
Using an SQL injection UNION attack to retrieve interesting data

Now you know how many columns there are and it can hold spring data, you can retrieve interesting data.
 
Suppose that:
The original query returns two columns, both of which can hold string data.
The injection point is a quoted string within the WHERE clause.
The database contains a table called users with the columns username and password.
 
In this situation, you can retrieve the contents of the users table by submitting the input:
' UNION SELECT username, password FROM users--
 
Retrieving multiple values within a single column
If the query only retrieves a single column, you can easily change this to retrieve multiple values in a single column.
 
On oracle you can use: 
' UNION SELECT username || '~' || password FROM users--
 
This uses the double-pipe sequence || which is a string concatenation operator in Oracle. The injected query concatenates together the values of the username and password fields, separated by the ~ character.
The results from the query will let you read all of the usernames and passwords, for example:
...
administrator~s3cure
wiener~peter
carlos~montoya
...
