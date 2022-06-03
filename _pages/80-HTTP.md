---
title: ""
permalink: /80-HTTP/
layout: single
author-profile: true
---

# HTTP - Web Vulnerabilities.
We usually just think of vulnerabilities on the http-interface, the web page, when we think of port 80. But with .htaccess we are able to password protect certain directories. If that is the case we can brute force the following way.
Password protect directory with htaccess.

## Step 1
Create a directory that you want to password-protect. Create a .htaccess file inside that directory. Content of .htaccess:
- AuthType Basic
- AuthName "Password Protected Area"
- AuthUserFile /var/www/html/test/.htpasswd
- Require valid-user

- Create .htpasswd file
- htpasswd -cb .htpasswd test admin
- service apache2 restart

This will now create a file called .htpasswd with the user: test and the password: admin

If the directory does not display a login-prompt, you might have to change the apache2.conf file. To this:
```
<Directory /var/www/html/test>
    AllowOverride AuthConfig
</Directory>
```
# Brute force it
Now that we know how this works we can try to brute force it with medusa.
```
medusa -h <ip> -u admin -P wordlist.txt -M http -m DIR:/test -T 10
```
## General
`ctrl+U`  View page source (in Firefox) 

## Gobsuter
`gobuster dir -u http://10.10.10.121/ -w /usr/share/dirb/wordlists/common.txt`  Run a directory scan on a website 

`gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt`  Run a sub-domain scan on a website 

## Dirbuster
```
Dirbuster &
Add php.txt.html
```
## curl
 `curl -IL https://www.inlanefreight.com`  Grab website banner 
 `curl 10.10.10.121/robots.txt`  List potential directories in `robots.txt` 

## Web certs
 `whatweb 10.10.10.121`  List details about the webserver/certificates 

## SQLmap
(capture burp request on search function) 
```
Sqlmap -r request.txt –dbms=mysql –dump
```
- -r uses request file
- –dbms specify what type of database
- –dump outputs entire database

## Nikto
```
Nikto -h https://<IP>
```
(if doesn’t work try with http)

## Davtest
```
Davtest -url <url>
```

## Joomla
joomscan

``joomscan -u <URL>``

# BurpSuite

## Credential stuffing
- Use burp suite
- Go to webpage
- Go to sign in page
- Intercept a login request
- Right click Send to intruder
- Clear positions
- Highlight email parameter and press add, do the same as password.
- Use pitchfork
- Go to payloads
- Paste emails into 1st payload
- Paste passwords into 2nd payload
- Run attack
- Look for status or change in length

# Buffer Overflow
https://github.com/johnjhacking/Buffer-Overflow-Guide

# Useful commands
```  
/etc/hosts
```
You can append the IP address of the box to a domain name by going to /etc/hosts and adding domain-name target-ip
  
At the end of a URL, you can add 
```
{{1+1}}
```
if this comes back with 'page 2 cannot be found', it means that python can be used to execute commands between these brackets {{}}.

# Feroxbuster
used to brute force recursive directories

https://github.com/epi052/feroxbuster.git
