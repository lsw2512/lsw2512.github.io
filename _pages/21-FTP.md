---
title: "21 - FTP"
permalink: /21-FTP/
layout: single
---

# Port 21 - FTP 

Connect to the ftp-server to enumerate software and version ftp nc 21

Many ftp-servers allow anonymous users. These might be misconfigured and give too much access, and it might also be necessary for certain exploits to work. So always try to log in with anonymous:anonymous.

Remember the binary and ascii mode! If you upload a binary file you have to put the ftp-server in binary mode, otherwise the file will become corrupted and you will not be able to use it! The same for text-files. Use ascii mode for them! You just write binary and ascii to switch mode.
