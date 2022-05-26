---
title: "Reactive Measures to Phishing"
permalink: /Phishing_Reactions/
layout: single
author-profile: true
---

## Immediate Response Process
1. Retrieve an original copy of the phishing email
2. Gather artefacts from the phishing email
3. Inform the recipients that received the email
4. Investigate malicious artefacts to collect indicators of compromise that can be blocked to protect the organisation
5. Take defensive measures
6. Complete the investigation report, documenting all of the above steps

## Inform Email Recipient

When Informing recipients include:

- The date and time the email was sent (allows the recipients to find the email easier by looking at the times of emails that they have received)
- The subject line of the malicious email (allows the recipients to find the email easier by looking at the subject lines of emails that they have received)
- Clear instructions on what to do with the email (this will depend on how the organisation deals with phishing emails. This could either be instructing the recipients to delete the email or forward it to a security-owned mailbox)
- Contact details for if the recipient is unsure what to do (typically a security-owned mailbox, so the user can get support from the security team

## Blocking Email-Based artefacts

Email based artefacts:
- Email Sender (mailbox@domain)
- Sender Domain (@domain)
- Sending Server IP
- Subject Line

what to do:
- Block the email sender (or domain if you don't normally get emails from this domain)
- If the reply-to address is different to the sending address, then you can block the reply-to address since this is usually owned by the malicious actor.
- You can also block the sending server IP, however this can only be done if this is a rogue IP. If you blocked Google's server IP then it would stop a lot of legitimate emails.
- Attackers often use one or few subject lines since editing them can be a lot more work. If it's an unusual subject then this will be a good thing to block.

## Blocking Web-Based Artefacts
- Use a web proxy or perimeter firewall to block malicious websites.
- When using a web proxy you can either block the URL or Domain
- If you block URL you can block from the first directory that looks malicious
- If you block an entire domain, this will prevent any access to the website. (if you do this for Google.com your fucked)

### DNS Blackholing
This is when you put a DNS entry so if a user tries to access a specific site, they will be redirected to a different one.

So if there is a known malicious site, you could create a DNS entry so the user gets directed to a safe site, and educated about malicious links.
This can be paired to SIEM or EDR alerts so you can view who clicks the link.

## Blocking File-Based Artefacts
When blocking files, you can either block file hashes or file names.

- When you block a file hash, if this hash is present on a system it will be deleted.
- Dues to hash collisions MD5 and SHA1 have been deprecated. SHA256 is the current standard for hashing.
- Blocking filenames can be risky unless the file name is very unique
- Filenames are often used to generate watch lists to generate alerts instead of delete files.

## Informing Threat Intel Team

### Sustained campaign
If you inform the threat intel team of a continuous attack, they may beable to predict how the campaign will continue, and to take actions to stop or outsmart the attacks. 

### Targeted attack
If the threat intel team is made aware of targeted attacks, they can work with the specific employee to decrease the likelihood of it being successful. Or they can conduct public exposure assessments to determine how much information is publicly available.
