---
title: "Password Cracking"
permalink: /Password-Cracking/
layout: single
author-profile: true
---


## Types of hashes

### Cisco
```
Hash	                                                                      Hash Type
enable secret 5 $1$pdQG$o8nrSzsGXeaduXrjlvKc91	                            Cisco Type 5 salted md5

username rout3r password 7 0242114B0E143F015F5D1E161713	                    Cisco Type 7 Custom, reversible

username admin privilege 15 password 7 02375012182C1A1D751618034F36415408   Cisco Type 7 Custom, reversible
```
#### Cracking cisco hashes
##### Type 5
The type 5 password can be decrypted with john:

``root@kali# /opt/john/run/john --wordlist=/usr/share/wordlists/rockyou.txt level5_hash ``      

```                      
Using default input encoding: UTF-8
Loaded 1 password hash (md5crypt, crypt(3) $1$ [MD5 256/256 AVX2 8x3])
Will run 3 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
stealth1agent    (?)
1g 0:00:00:15 DONE (2019-08-20 19:54) 0.06631g/s 232443p/s 232443c/s 232443C/s steaua17..steall3
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

##### Type 7
There are online tools to crack type 7 hashes, but it’s more interesting to understand what’s going on. The paper I mentioned above goes into detail as to how the Type 7 scheme works. Basically, string in the config is hex characters. The first two characters is the offset into the static key to start at (indexed starting at one, eww). The rest are the hex bytes that when xored by successive characters from the password, produce the plaintext password. The static encryption key is `“tfd;kfoA,.iyewrkldJKD”.`

So if I start with “0242114B0E143F015F5D1E161713”, I know the password is 13 characters long. I also know that the first byte is 2, so start at the second letter in the key, f. Then xor it with the next hex byte, 42 to get $:

```
root@kali# python3
Python 3.7.3 (default, Apr  3 2019, 05:39:12)
[GCC 8.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> chr(ord('f') ^ int('42',16))
'$'
```

I found a quick python script to decrypt it:
```
#!/usr/bin/env python3

import sys
from binascii import unhexlify

if len(sys.argv) != 2:
    print(f"Usage: {sys.argv[0]} [level 7 hash]")
    exit()

static_key = "tfd;kfoA,.iyewrkldJKD"
enc = sys.argv[1]
start = int(enc[:2], 16) - 1
enc = unhexlify(enc[2:])
key = static_key[start:] + static_key[:start]

plain = ''.join([chr(x ^ ord(key[i % len(key)]))  for i, x in enumerate(enc)])
print(plain)
```

## password backup

to decrypt a password backup you need to use xxd

`xxd -r passwordbackup`

