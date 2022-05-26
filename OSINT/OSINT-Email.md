---
title: "Email OSINT"
permalink: /OSINT-Email/
layout: single
author-profile: true
---

## Discovering Email Addresses

- Hunter.io - https://hunter.io/
- Phonebook.cz - https://phonebook.cz/
- VoilaNorbert - https://www.voilanorbert.com/
- Email Hippo - https://tools.verifyemailaddress.io/
- Email Checker - https://email-checker.net/validate
- Clearbit Connect - https://chrome.google.com/webstore/detail/clearbit-connect-supercha/pmnhcgfcafcnkbengdcanjablaabjplo?hl=en
- Email and breached data OSINT
- breach-parse - https://github.com/hmaverickadams/breach-parse

## The harvester

used to gather a lot of information

If you search too much some sources will stop working

`theHarvester -d domain.com -b google -l 500`

## Breach Parse

`./breach-parse.sh @tesla.com tesla.txt h8mail -t shark@tesla.com -bc "/opt/breach-parse/BreachCompilation/" -sk`

## H8mail

Looks at specific target

`H8mail -t target@domain.com`
