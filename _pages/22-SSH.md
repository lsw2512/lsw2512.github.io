---
title: "22 - SSH"
permalink: /22-ssh/
layout: single
author-profile: true
---
# Port 22 - SSH

SSH is such an old and fundamental technology so most modern versions are quite hardened. You can find out the version of the SSH either by scanning it with nmap or by connecting with it using nc.

nc <ip>

It returns something like this: SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu1

This banner is defined in RFC4253, in chapter 4.2 Protocol Version Exchange. http://www.openssh.com/txt/rfc4253.txt The protocol-version string should be defined like this: SSH-protocol version-software version SP comments CR LF Where comments are optional. And SP means space, and CR (carriage return) and LF (Line feed) So basically the comments should be separated by a space.
