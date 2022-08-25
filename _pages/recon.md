---
title: ""
layout: single
permalink: /recon/
author-profile: true
---

# Recon

This will mostly fall under the OSINT section of with webpage, but here are some command line techniques.

## Sublister

```
_Sublister3er -d <domain>
```

## WhatWeb

```
_Whatweb http://<domain>
```

## Amass

### Installation
```
go get -u http://github.com/OWASP/Amass/…
amass enum –list
```

### Running
```
basic command - amass enum -d <URL>

active recon - amadd enum -d <URL> -active
```

more complex commands can be found [here](https://allabouttesting.org/owasp-amass-quick-tutorial-example-usage/)
