---
title: "password OSINT"
permalink: /OSINT-password/
layout: single
author-profile: true
---

## Hunting Breached Passwords
- https://github.com/hmaverickadams/breach-parse
- WeLeakInfo - https://weleakinfo.to/v2/
- LeakCheck - https://leakcheck.io/
- SnusBase - https://snusbase.com/
- Scylla.sh - https://scylla.sh/
- HaveIBeenPwned - https://haveibeenpwned.com/
- Dehashed - https://dehashed.com/

## Gathering Breach Credentials with breach parse

Tool for parsing breached passwords.

Download breached password list from magnet located here (put into beachparse folder): magnet:?xt=urn:btih:7ffbcd8cee06aba2ce6561688cf68ce2addca0a3&dn=BreachCompilation&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A80&tr=udp%3A%2F%2Ftracker.leechers-paradise.org%3A6969&tr=udp%3A%2F%2Ftracker.coppersurfer.tk%3A6969&tr=udp%3A%2F%2Fglotorrents.pw%3A6969&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337

- Cd to breach-parse folder
- Run      ./breach-arse.sh @domain domain.txt

## Hunting Breached credentials with DeHashed

- DeHashed - costs money
- Can search for anything in the screenshot below.
- Hashes can be searched at hashes.org

## Other tips

If you find a breached password, search for the password to find other compromised accounts.
