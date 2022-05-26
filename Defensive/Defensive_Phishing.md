---
title: "Defensive Phishing"
permalink: /Defensive_Phishing/
layout: single
author-profile: true
---
## Marking External Emails
### EXCHANGE
- Go to admin centre
- Go to mailflow
- Create new rule
- Name External email
- Apply rule if the sender is outside the organisation
- AND the recipient is inside the organisation
- Prepend the subject of the message with: EXTERNAL

## Email security technology
### SPF records
- Sender policy framework
- Used to stop attackers spoofing your domain by specifying IP or Hostnames that are authorised to send emails
- The basic syntax of the record is: `v=spf1 <IP> <enforcement rule>`

### DKIM
- Domain Keys Identified Mail
- Uses cryptography to verify if an email has been sent by its trusted servers
- The basic syntax of the record is:  `V=DKIM1 <key type> <public key>`

### DMARC
- Domain Based Message Authentication, reporting and conformance
- This allows domain owners to specify what happens if a email fails SPF AND DKIM
- The three basic options are: none, quarantine and reject
- The basic syntax of the record is:  v=DMARC1 <action> <report address>

## Spam filter
- Gateway spam filter - sits behind a on-premises firewall on a network (Barracuda email security gateway)
- Hosted Spam FIlter- these are hosted in the cloud and work similarly to gateway spam filters. However sometimes these can update more quickly.
- Desktop spam filters - these go on the host computer, these are often freeware so can sometimes be risky to install.

## Types of spam filters
- Content Filters - uses information in the header and body to determine if the email is legitimate or spam.
- Rule-based filters - create rules in exchange to mark as spam if the email meets a specific rule.
- Bayesian Filters - uses machine learning to detect spam depending on emails which have been marked. However can require a large amount of spam to be most effective

## Attachment Filtering
- Best way to do this is to block file types which aren’t commonly used by the company
- Most common formats to block are: .exe, .vbs, .js, .iso, .bat, .ps or .html

## Attachment sandboxing
- Attachments that do not get blacked, are opened in a sandbox environment before they get delivered.
- They are then analysed and do not get delivered if something malicious is detected.
- A report can be generated to detail what the attachments do.
  
## Security Awareness training
- User awareness training is crucial in preventing a phishing attack.
- There are two methods: awareness training or simulated phishing attack.

## Awareness training
Make users aware to be wary of:
- Coming from an unknown sending address.
- Improper grammar and spelling mistakes.
- Poor styling.
- Trying to get the recipient to click on a button or complete an action.
- Suspicious URLs and attachments.

## Simulated Phishing Attacks
- Send simulated emails to see how likely a phishing attack would succeed
- If a user clicks on a “malicious” link then it can take them to a safe website, making them aware of what has just happened.
- This can allow for improvements to be made to staff training or make directors aware of how important security is.
- Some platforms to do this on are: Sophos Phish Threat, GoPhish open-source, trend micros phish insight or PhishingBox.
