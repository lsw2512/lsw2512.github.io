---
title: "Types of Phishing"
permalink: /Types_of_Phishing/
layout: single
author-profile: true
---

## Reconnaissance
- Attacker is trying to find if the email is active.
- Can tell this without the recipient replying to the email.
- Recon emails can either contain random letters in the header (check for error codes being sent back)
- Use social engineering to get the recipient to respond
- Use tracking pixels to see if the email has been viewed
```
<img style="position: absolute;" src="Tracking">
<img style="display:none";"src="Tracking">
<img src="Tracking" width="0" height="0">
```
The following data can potentially be acquired and analysed using a tracking pixel.

- The operating system used (gives information on the use of mobile devices).
- Type of website or email used, for example on mobile or desktop.
- Type of client used, for example, a browser (webmail) or mail program (email client).
- Client’s screen resolution.
- Date and time the email was read.
- IP address (gives information on the Internet Service Provider and location).

## Spam
- Often harmless
- Signed up to mailing lists without permission or hidden in terms and conditions when signing up to a website
- Be careful it's not malspam (malicious emails sent to a lot of recipients)

## Credential harvester
Malicious URL in email, taking victim to a webpage (often designed to look like a legitimate company) and prompted to enter login information.

- Imitates commonly-used websites and services (such as Outlook, Amazon, HMRC, DHL, FedEx, and many more).
- Entices the recipient to enter credentials into a fake login portal.
- Uses social-engineering tactics including; creating a sense of urgency, and using false authority.
- URLs may be completely random or attempt to copy the legitimate domain name of the organisation they are masquerading as.
- Often have small spelling or styling mistakes, something that is extremely rare with legitimate emails coming from big brands and organisations.

## Social Engineering
- Manipulating people to think the email is from someone they know
- Making people think there's a sense of urgency, this is to make them panic and do something without thinking too much into it, or checking if it's true.
- Convincing the recipient to reply to an attacker’s initial email (recon emails).
- Convincing the recipient to transfer money by posing as the CEO, CTO, CFO, or another employee on the executive board.
- Convincing the recipient to provide the attackers with information that is confidential or private by posing as the data subject or someone in a higher position within the company.

## Microsoft macro attacks
- Make sure macros are disabled in your Microsoft Office applications. In enterprises, IT admins set the default setting for macros: Enable or disable macros in Office documents
- Don’t open suspicious emails or suspicious attachments.
- Delete any emails from unknown people or with suspicious content. Spam emails are the main way macro malware spreads.
- Enterprises can prevent macro malware from running executable content using ASR rules.
