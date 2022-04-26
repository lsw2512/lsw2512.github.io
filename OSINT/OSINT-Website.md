---
title: "Website OSINT"
permalink: /OSINT-Website/
layout: single
author-profile: true
---

## Website OSINT
- BuiltWith - https://builtwith.com/
- Domain Dossier - https://centralops.net/co/
- DNSlytics - https://dnslytics.com/reverse-ip
- SpyOnWeb - https://spyonweb.com/
- Virus Total - https://www.virustotal.com/
- Visual Ping - https://visualping.io/
- Back Link Watch - http://backlinkwatch.com/index.php
- View DNS - https://viewdns.info/

## Search for website
- Domain dossiers can be used to scan domains.
- Who is record - who owns the website
- DNS records - find where email may be hosted
- reddit.com/domain/domain.com

## Website OSINT Tools
- Subfinder - https://github.com/projectdiscovery/subfinder
- Assetfinder - https://github.com/tomnomnom/assetfinder
- httprobe - https://github.com/tomnomnom/httprobe
- Amass - https://github.com/OWASP/Amass
- GoWitness - https://github.com/sensepost/gowitness/wiki/Installation
- Wappalyzer
- photon

whois tcm-sec.com 

nano ~/.bashrc 

'export GOPATH=$HOME/go  
export GOROOT=/usr/lib/go  
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin 

source ~/.bashrc'

- go get -u github.com/tomnomnom/httprobe 
- go get -u github.com/tomnomnom/assetfinder 
- GO111MODULE=on go get -u -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder 
- go get -u github.com/sensepost/gowitness 
- export GO111MODULE=on 
- go get -v github.com/OWASP/Amass/v3/... 

- subfinder -d tcm-sec.com 
- assetfinder tcm-sec.com 
- amass enum -d tcm-sec.com 
- cat tesla.txt | sort -u | httprobe -s -p https:443 
- gowitness file -f ./alive.txt -P ./pics --no-http 
- SubDomains
- Pentest-Tools Subdomain Finder - https://pentest-tools.com/information-gathering/find-subdomains-of-domain#
- Spyse - https://spyse.com/
- crt.sh - https://crt.sh/

- Site:tesla.com
- Site:tesla.com -www
- Site:tesla.com -www inurl:dev
- Crt.sh  %.domain.com
- Other methods
- Shodan - https://shodan.io
- Wayback Machine - https://web.archive.org/
- Shodan
- Can be used to webcams which are exposed to the internet
- Can search for different types of strings.
- City:city
- City: city port:xxx

## Wayback machine
View older web pages and changes to websites before they happen.

Can also look at cached version on google.
