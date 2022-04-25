---
title: "135-MSRPC"
permalink: /135-MSRPC/
layout: single
author-profile: true
---

This is the windows rpc-port. https://en.wikipedia.org/wiki/Microsoft_RPC

Enumerate


nmap 192.168.0.101 --script=msrpc-enum

msf > use exploit/windows/dcerpc/ms03_026_dcom

Impacket: rpcdump.py <ip>
Impacket: samrdump.py <ip>
