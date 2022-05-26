---
title: ""
permalink: /scanning/
layout: single
author-profile: true
---

# Scanning

## Nmap

`nmap <ip>`

`nmap -sV -sC -p- <ip>`

`locate scripts/citrix`                                            
List various available nmap scripts

`nmap --script smb-os-discovery.nse -p445 10.10.10.40`             
Run an nmap script on an IP 

`-sC`
scripts should be used

`-sV`                                                               
perform a version scan

`-p-`                                                                
all ports

`-sV –script=banner`
banner grab

`-sS`                                                                
Stealth Scan

`-sn`                                                              
ping scan

`-sU`                                                                
UDP scan
  
## Netcat

`netcat 10.10.10.10 22`                                            
Grab banner of an open port 

`Nc -nv     <ip> <port>`                                             
grabs banner with netcat

## SS

`ss -tulpn`
Tell us what socket connections are running.
```
-t display TCP sockets
-u display UDP sockets
-l display listening sockets
-p show the process
-n doesn’t resolve service name
```
`Ssh -L 10000:localhost:10000 <username>@<ip>`
Connects to a socket we fi=ound from ss scan

Fullhunt.io
https://fullhunt.io/

# Port XXX - Service unknown
  
If you have a port open with unknown service you can do this to find out which service it might be.
  
`nmap -d <ip> 8000`
