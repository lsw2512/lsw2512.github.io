---
title: "MITRE ATT&CK Framework"
permalink: /MITRE_ATT&CK/
layout: single
author-profile: true
---

## Initial Access
- Drive-by Compromise
- Exploit public-facing application
- External remote services
- Hardware additions
- Phishing
- Replication through removable media
- Supply chain compromise
- Trusted relationship
- Valid accounts

### Phishing T1566
- T1566
- T1566.001 - Spear Phishing Attachment
- T1-566.002 - Spear Phishing Link
- T1566.003 - Spear Phishing via Service

- NIDS and email gateways can detect phishing emails in transit
- Detonation chambers may identify malicious attachments
- URL inspection within email
- Detonation chambers can be used to identify malicious URLs
- SSL/TLS inspection can detect in the initial delivery
- Antivirus can detect malicious attachments

### External remote Services T1133
- VPNs
- Remote Desktop Protocol
- SSH
- Citrix
- Highly likely they will also use T1078 Valid Account
- Authentication logs and analyze for unusual access or activity

### Removable Media T1091
- Uses USB to transport malware
- Requires physical access
- Can be used to attack air - gapped systems
- Monitor file access on removable media
- Events after opening are likely to occour

## Execution
This describes how adversaries will execute malicious code

### Scheduled task/jobs T1053
- Can schedule tasks like wen to run malware or when to send a network connection to a command and control server to maintain persistence
- T1053.001 - at (linux)
- T1053.002 - at (windows)
- T1053.003 - cron
- T1053.004 - launchd
- T1053.005 - scheduled task
- At is used to schedule specific events

### Windows management Instrumentation T1047
- Admin feature which facilitates the management of devices and applications in a network
- Can be used in an attack for lateral movement or discovery
-Used WMI service for local and remote access, SMB and remote procedure call service
- APT 41 uses this for execution of commands via WMIEXEC and powersploit
- Astaroth uses it to execute payloads
- Emotet uses to execute powershell.exe
- Fin 6 uses it to automate the remote execution of powershell scripts
- FIN8 uses malicious spear phishing payloads to use WMI to launch malware

- Monitor network traffic for WMI Connections
- Perform process monitoring to capture command line arguments of WMIC

### User Execution T1204
- T1204.001 - Malicious Link
- T1204.002 - Malicious File
- Very closely ties to phishing
- Can achieve execurition on a system without having initial access

- Monitor for execution for applications that may be used to gain initial access.
- Anti virus can detect malicious documents
- Endpoint sensing or network sensing can potentially detect malicious events

## Persistence
Ways to maintain a foothold by hiding from defenders

### Boot or Logon Autostart Execution T1547
- Can be achieved by adding a program to a startup folder or referencing it with a registry run key
- APT 18,19 and 29 utilise the registry run key method

- Monitor for additions to things that can trigger autostart executions
- Sysinternals autoruns can be used to detect system autostart configuration changes
- Suspicious program execution as autostart programs can be compared to history to see if it has been used before

### Eternal Remote Services T1133
- If a system has internet facing remote services and an attacker has valid credentials they could maintain persistence
- If an attacker gets valid VPN credentials they can connect via VPN from anywhere
- APT18, APT41, Dragonfly 2.0 and FIN5 have reused valid credentials to maintain access

- Collect logs and analyze for suspicious patterns

### Privilege Escalation
Used to gain higher privileges

### Valid Accounts T1078
This can either be done immediately as result of an exploitation attack or as a next stage in an attack

### Privilege Escalation Exploits T1068
- Exploiting software or system functions can give an attacker more access than a user account
- APT28 has used CVE-2017-0263 - allows attackers to run malicious code in kernel mode.
- APT32 has used CVE-2016-7255 - this is similar to the one above but also has a executable file to help execute this CVE

- Look for abnormal behaviour 
- Look for activity that indicates that higher privileges have been gained

## Defense Evasion 
### Impair Defenses T1562
- T1562.001 - Disable or Modify Tools
- T162.002 - Disable Windows Event Logging
- T1562.003 - HISTCONTROL
- T1562.004 - disable or Modify System firewall
- T1562.006 - Indicator Blocking
- T156.007 - Disable or modify cloud

- Disable of Modify Tools – “Adversaries may disable security tools to avoid detection. This can take the form of killing security software or event logging processes, or other methods to interfere with security tools scanning or reporting information.”
- Disable Windows Event Logging – “Adversaries may disable Windows event logging to limit data that can be leveraged for detections and audits. This data is used by security tools and analysts to generate detections. By disabling Windows event logging, adversaries can operate while leaving less evidence of a compromise behind.”
- HISTCONTROL – “Adversaries may configure HISTCONTROL to not log all command history. The HISTCONTROL environment variable keeps track of what should be saved by the history command and eventually into the ~/.bash_history file when a user logs out."
- Disable or Modify System Firewall – “Adversaries may disable or modify system firewalls in order to bypass controls limiting network usage. Changes could be disabling the entire mechanism as well as adding, deleting, or modifying particular rules.”
- Indicator Blocking – “An adversary may attempt to block indicators or events typically captured by sensors from being gathered and analyzed. These settings may be stored on the system in configuration files and/or in the Registry as well as being accessible via administrative utilities such as PowerShell or Windows Management Instrumentation.”
- Disable or Modify Cloud Firewall – “Adversaries may disable or modify a firewall within a cloud environment to bypass controls that limit access to cloud resources.”

- Monitor process and command line arguments
- Look for security tools or logging services which have been killed or stop running
- Lack of log events may be suspicious

### Indicator Removal - T1070
- T1070.001 - Clear Windows Event Logs 
- T1007.002 - Clear Linux or Mac System Logs
- T1070.003 - Clear Command History
- T1070.004 - File Deletion
- T1070.005 - Network Share Connection removal
- T1070.006 - Timestomp

File system monitoring may be used to detect improper deletion or modification

### RootKits T1014
- Malicious programs that work to hide existence of malware
- Intercept and changing operating system API calls that supply system information
- Malicious elements do not get reported
- Can be found at user or kernel level

## Credential Access
### OS Credential Dumping T1003
Local access can allow for password retrieval.

#### LSASS Memory - T1003.1
- Retrieve credentials which are stored in memory
- Uses Local Security Authority Subsystem Service (LSASS)
- Can be accessed by admin or SYSTEM-Level user
- Once credentials are retrieved, hashes can be brute forced offline

####/etc/passwd /etc/shadow - T1003.8
- Dump contents of /etc/passwd and /etc/shadow
- Bruteforce hashes with john
- /etc/shadow can only be accessed by a root level user

- Monitor for unexpected processes interacting with lsass.exe
- Use AuditD on linux to detect malicious processes

#### Brute Force - T1110
- Either to guess credentials or go through every possible combination
- Another way to use this is to brute force hashes

- Monitor for login failures

## Discovery
### Account Discovery - T1087
#### T1087.001 - Local Account
- May get local account listing using a command like net user or net localgroup
- Or id and groups on mac or linux
- Local users can also be enumerated through reading the /etc/passwd file with commands like cat strings and head

#### T1087.002 - Domain Account
- Attackers may attempt to get get a listing of domain accounts
- Netuser /domain
- Net group /domain
- Dscacheutil -q group (MAC)
- Ldpsearch (linux)

#### T1087.003 - Email Account
- Attackers may attempt to get a listing of email addresses by dumping exchange email lists
- This is a technique emotet uses to send malicious emails from the compromised account

#### T1087.004 - Cloud Account
- Attackers can navigate to popular console windows to look for cached credentials

- Data and events should be viewed as a chain instead of individually to look for related activities like lateral movement 
- Monitor process and command line arguments for actions that could be taken to gather system and network information
- Information can also be acquired through windows system management tools

### Network Discovery - T1046
- Vulnerability scanning or port scanning may be used to detect devices on the network

- Network intrusion detection systems have the ability to flag this activity

### File and Directory Discovery - T1083
- Looking for files and important data
- Impossible to mitigate since every user does it
- Monitor processes and command line arguments
- Look for remote access tools and tools which are automatically scanning the file system

## Lateral Movement
### Internal remote Services - T1021
- Using credentials to log into a service which accepts remote connections.
- Correlate use of login activity with unusual behaviour to spot suspicious connections

### Internal Spear Phishing - T1534
- Once a actor has access tey can send internal emails to gain access to more accounts on the network
- NIDS and email gateways should scan internal attachments as well

## Collection
### Email Collection - T1114
- T1114.001 - local email collection
  - C:\Users\<username>\Documents\Outlook Files or C:\Users\<username>\AppData\Local\Microsoft\Outlook.
- T1114.002 - Remote Email Collection
  - Usually an online exchange server or office 365
- T1114.003 - Email Forwarding Rule
  - Forwarding rules an be set up to silently forward emails to an attacker owned mailbox

- Look at email server logs
- Monitor processes

## Audio Capture T1123
An attacker can utilise peripheral devices to collect audio. This could be confidential information.
APT37 uses soundwave to capture audio information like this.

Difficult to detect
Look for unusual use of recording software compared to the users role
Screen Capture T1133
Taking screen captures can help gather information
Look for CopyFromScreen, XWD or screen capture
Agent Tesla is a famous Remote Access Trojan which is used for this
Look for unusual processors which can be used to correlate with other events
Data From local system T1005
Attackers can search through any attached local or network drives to find interesting or sensitive information
To help this commands like find tree locate and dir will help
GravityRAT steals files with extensions: .docx, .doc, .pptx, .ppt, .xlsx, .xls, .rtf and .pdf
Inception uses a file hunting plugin to collect .txt, .pdf, .xls or .doc

Monitor processes and command line arguments can be collected 

Command and Control
Application Layer Protocol T1071
T1071.001 - web protocols
T1071.002 - File Transfer Protocols
T1071.003 - Mail Protocols
T1071.004 - DNS

Adversaries use application layer protocols to blend in with standard traffic
Cobalt strike is a popular attack platform for both penetration testers and malicious actors.
SMB is common for this

Analyze network for uncommon data flows
Processors utilizing the network which do not normally have network communications
Analyze packet contents that do not follow standards
Web Service T1102
Adversaries may use an existing legitimate external web service as a means of relaying data
Popular websites can give a good cover for C2
Look for unusual network connections or network connections that happen at strange times
Look for uncommon data flows
Non-Standard Port T1571
Adversaries may use a non standard port to try and bypass filtering.
APT33 uses HTTP over 808 and 880 instead of 80.
BADCALL malware uses 443 and 8000 using FakeTLS
Exfiltration
EXFIL over C2 Channel T1041
Extracting data using the C2 channel
Use a NIDS to detect
Analyze network data for uncommon data flows
Processes utilizing the network that do not normally have communications are suspicious
Scheduled Transfer T1029
Adversaries may schedule data exfiltration to only occur at specific times to evade NIDS.
ADVSTORESHELL malware collects data, compresses it, encrypts it and uploads it every ten minutes 
Cobalt strike can set the beacon payload to random intervals making it harder to spot.
Monitor network
Impact
Account Access Removal T1531
Removing access to accounts
Can be done by deleting, locking or changing passwords
Very noisy so most likely done after the attackers objectives are complete unless their objective is to disrupt business
Monitor for changes to user accounts: Event ID 4723, 4724, 4726 and 4740
Defacement T1491
T1491.001 - Internal Defacement
T1491.002 - External Defacement
Change content
Do this to deliver message, intimidation or to claim intrusion or make it look like someone else is responsible for the attack
Monitor for unplanned content changes.
Data Encryption T1386
Ransomware
Work to encrypt files and data and withhold the encryption key.
Since this affects local accounts, there needs to be a way for it to spread
Use process monitoring to look for execution of binaries involved in data destruction like vssadmin, wbadmin or bcdedit.
Look for large quantities of file modifications
Uses of ATT&CK
Threathunting - keep track of what has manually been searched for in a hunt
adversary emulation - use to track what methods APTS use to simulate specific APT attacks
Threat Detection - go through and check for alerts for each one to see which ones need detection rules improving
 https://mitre-attack.github.io/attack-navigator/enterprise/
