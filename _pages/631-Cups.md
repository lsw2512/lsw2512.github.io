---
title: "631 - Cups"
permalink: /631-Cups/
layout: single
author-profile: true
---

Common UNIX Printing System has become the standard for sharing printers on a linux-network. You will often see port 631 open in your priv-esc enumeration when you run netstat. You can log in to it here: http://localhost:631/admin

You authenticate with the OS-users.

Find a version. 
```
Test cups-config --version. 
```
If this does not work surf to http://localhost:631/printers and see the CUPS version in the title bar of your browser.

There are vulnerabilities for it so check your searchsploit.
