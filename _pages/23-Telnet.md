---
title: ""
layout: single
permalink: /telnet/
author-profile: true
---
# Port 23 - Telnet

Telnet is considered insecure mainly because it does not encrypt its traffic. Also a quick search in exploit-db will show that there are various RCE-vulnerabilities on different versions. Might be worth checking out.
Brute force it

You can also brute force it like this:

hydra -l root -P /root/SecLists/Passwords/10_million_password_list_top_100.txt <ip> telnet
