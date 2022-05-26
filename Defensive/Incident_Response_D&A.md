---
title: "Incident Response Detection and Analysis"
permalink: /Incident_Response_D&A/
layout: single
author-profile: true
---
## Common events and incidents
- R2L port scanning - remote IP is scanning local IP, detected through logs. Rarely ever an impact but can lead to further attacks.
- R2L DOS/DDOS - denial of service, traffic larger than the normal baseline level of traffic. Can take systems offline and prevent users from using internet services
- L2L scanning - Siem rules can be made to detect this.security team vulnerability scanners should be whitelisted
- Login failures - can be a lot of false positives, can be detected in logs, most likely false positive but a high amount could detect malicious activity

## Baselines and Behaviour Profiles
- Recording what is meant to be normal on a network
- Can be anything that could signal an attack if it changes

## Introduction to wireshark
- Udp - display udp only
- Http.request - display http requests only
- Tcp.port - display tcp port
- Window_size_value - size of 8000 bytes or over
- && - and
- || - or
- Ip.dst_host - destination ip

## YARA rules
- Way of identifying specific files
- Three components to include: rule name, identification values and conditions.
- Rule HelloString : Hello
- HelloString is the name of the rule Hello is the shorthand name
- Strings: $a = “Hello”
- String shows that you're looking for a text string  $a is the variable name for the string
- condition : $a
- Since for the condition we put $a  if the file contains ‘Hello’, it will be flagged.
- Meta will add a human readable description to the rule
- Use -m in command line to display meta data

Yargen can be used to automatically generate rules for malicious files

- Malware can use strings in its code like IP addresses or bitcoin wallet ID
- Yara myrule.yar somedirectory
- Meta - used for description from the author of the rule
- ‘desc ‘ is shorthand for description
- Strings - can be used to search for specific text or hexadecimal in files or programs.
- You can use variables to met a condition
- Strings only match the exact text, you may need multiple strings if you want to search one work but with either a capital or not.
- Conditions - these are operators like <=, >=, !=. So you can search for if a string appears more than a specific number of times in a file.
- Combining keyworks - and, not, or   can search for multiple conditions 

## Cmd and powershell
- Ipconfig /ALL - outputs network information
- Tasklist - check running processes adn programs
- Wmic process get description, executablepath - display running processes and associated binary file
- Net user - print a list of all system users
- Net localgroup administrators - list users in the administrators group
- Sc query | more - list all services and detailed information
- Netstat -ab - list open ports on a system
