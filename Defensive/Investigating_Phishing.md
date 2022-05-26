---
title: "Investigating a Phishing Email"
permalink: /Investigating_Phishing/
layout: single
author-profile: true
---

## Artefacts to collect
- Sending Email Address (can be used to identify other emails that have been received)
- Subject Line (can be used to identify or block other phishing emails)
- Recipient Email Address 
- Sending server IP and Reverse DNS https://mxtoolbox[.]com/ReverseLookup.aspx
- Reply-to address (often an attacker controlled account)
- Date and Time
- Attachment Name
- SHA256 Hash Value (check against virus total and talos file reputation)
- Full URLs (copy and not written by hand) 
- Root Domain (can show if a site has been created for malicious purposes or if its a legitimate site that has been compromised).

## Email Artefacts
1. Subject line
2. Sending Addresss
3. Date + Time
4. Recipients

## Text Editor Extraction 

Sending server IP and Reply-to address

- Open email file in a text editor
- CTRL + F
- Search for IP and look for X-Sender-IP (record this)
- Look up this IP using whois http://whois.domaintools.com/
- Record Resolve Host field (if sending address and the host domain does not match up, it means the address has been spoofed)
- Now record Reply-to address > CTRL + F and search for ‘Reply’

## Web Artefacts
- Need to collect Full URL
- Right click and copy hyperlink
- Get screenshots from virus total, URLScan.io, ect.

## File Artefact
### Windows
`Powershell > get-filehash .\FILE`

The above will get a sha-256 hash

To get md5 or sha1 do this:
`Get-filehash -algorithm md5 .\FILE`

You can do multiple commands at once by using `;`

## Linux
```
sha256sum <file>
sha1sum <file>
md5sum <file>
```
Get filename and file size as well

Can use phish tool to automate the process

