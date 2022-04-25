---
title: "25 - SMTP"
permalink: /25-SMTP/
layout: single
author-profile: true
---
# Port 25 - SMTP

SMTP is a server to server service. The user receives or sends emails using IMAP or POP3. Those messages are then routed to the SMTP-server which communicates the email to another server. The SMTP-server has a database with all emails that can receive or send emails. We can use SMTP to query that database for possible email-addresses. Notice that we cannot retrieve any emails from SMTP. We can only send emails.

Here are the possible commands:
HELO - 
EHLO - Extended SMTP.
STARTTLS - SMTP communicated over unencrypted protocol. By starting a TLS-session we encrypt the traffic.
RCPT - Address of the recipient.
DATA - Starts the transfer of the message contents.
RSET - Used to abort the current email transaction.
MAIL - Specifies the email address of the sender.
QUIT - Closes the connection.
HELP - Asks for the help screen.
AUTH - Used to authenticate the client to the server.
VRFY - Asks the server to verify if the email user's mailbox exists.

## Manually

We can use this service to find out which usernames are in the database. This can be done in the following way.

nc ip                                                                              

telnet ip

## Automated
This process can of course be automatized

Check for commands

nmap -script smtp-commands.nse <ip>

smtp-user-enum
The command will look like this. -M for mode. -U for userlist. -t for target

smtp-user-enum -M VRFY -U /root/sectools/SecLists/Usernames/Names/names.txt -t <ip>

  
## Metasploit

It can also be done using metasploit
msf > use auxiliary/scanner/smtp/smtp_enum 

## SMTP documents
  
https://cr.yp.to/smtp/vrfy.html
http://null-byte.wonderhowto.com/how-to/hack-like-pro-extract-email-addresses-from-smtp-server-0160814/
http://www.dummies.com/how-to/content/smtp-hacks-and-how-to-guard-against-them.html
http://pentestmonkey.net/tools/user-enumeration/smtp-user-enum
https://pentestlab.wordpress.com/2012/11/20/smtp-user-enumeration/
