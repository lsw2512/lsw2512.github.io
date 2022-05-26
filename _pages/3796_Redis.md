---
title: "3796 - Redis"
permalink: /3796_Redis/
layout: single
author-profile: true
---

redis 6379

Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache, and message broker.

msf> use auxiliary/scanner/redis/redis_server



```redis-cli -h host

info #list all info

#look for key databases
key
db0=4

#select database using keys
select 4```
