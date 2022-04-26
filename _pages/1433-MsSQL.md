---
title: "1433 - MsSQL"
permalink: /1433-MsSQL/
layout: single
author-profile: true
---

Default port for Microsoft SQL.

sqsh -S ip -U sa

# Execute commands

To execute the date command to the following after logging in

- xp_cmdshell 'date'
- go

Many of the scanning modules in metasploit require authentication, But some do not.
 
use auxiliary/scanner/mssql/mssql_ping

# Brute force.

scanner/mssql/mssql_login

If you have credentials look in metasploit for other modules.
