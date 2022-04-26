---
title: "3306 - MySQL"
permalink: /3306-MySQL/
layout: single
author-profile: true
---
Always test the following:

Username: root

Password: root

- mysql --host=<ip> -u root -p
- mysql -h <Hostname> -u root
- mysql -h <Hostname> -u root@localhost
- mysql -h <Hostname> -u ""@localhost

- telnet ip 3306

You will most likely see this a lot:

ERROR 1130 (HY000): Host '192.168.0.101' is not allowed to connect to this MySQL server

This occurs because mysql is configured so that the root user is only allowed to log in from 127.0.0.1. This is a reasonable security measure put up to protect the database.

## Configuration files

cat /etc/my.cnf

http://www.cyberciti.biz/tips/how-do-i-enable-remote-access-to-mysql-database-server.html

## Mysql-commands cheat sheet
  
http://cse.unl.edu/~sscott/ShowFiles/SQL/CheatSheet/SQLCheatSheet.html

## Escalating privileges

If mysql is started as root you might have a chance to use it as a way to escalate your privileges.

## MYSQL UDF INJECTION:

https://infamoussyn.com/2014/07/11/gaining-a-root-shell-using-mysql-user-defined-functions-and-setuid-binaries/

## Finding passwords to mysql

You might gain access to a shell by uploading a reverse-shell. And then you need to escalate your privilege. One way to do that is to look into the database and see what users and passwords that are available. Maybe someone is reusing a password?
So the first step is to find the login-credentials for the database. Those are usually found in some configuration-file on the web-server. 
  
For example, in joomla they are found in:

/var/www/html/configuration.php

In that file you find the file:

> <?php
> class JConfig {
>     var $mailfrom = 'admin@rainng.com';
>     var $fromname = 'testuser';
>     var $sendmail = '/usr/sbin/sendmail';
>     var $password = 'myPassowrd1234';
>     var $sitename = 'test';
>     var $MetaDesc = 'Joomla! - the dynamic portal engine and content management system';
>   var $MetaKeys = 'joomla, Joomla';
>    var $offline_message = 'This site is down for maintenance. Please check back again soon.';
>     }
