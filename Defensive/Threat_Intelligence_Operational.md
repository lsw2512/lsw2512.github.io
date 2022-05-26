---
title: "Operational Threat Intelligence"
permalink: /Threat_Intelligence_Operational/
layout: single
author-profile: true
---

## Precursors Explained
- Precursors are elements of the incident identification and response process.
- This allows you to determine the existence of flaws and vulnerabilities in a system.
- By identifying precursors, organisations can prevent cyber attacks.

### Issues
These are extremely hard to detect, since it is very hard to spot a sign of an attack before it happens.

### Types of precursors
#### Port scanning, Operating system and application fingerprinting
- Both an attacker and a security professional can learn about vulnerabilities through port scanning.
- Another way to get these precursors is to monitor firewall connections and other logs.

#### Social engineering and Reconnaissance
- Using social techniques you can learn alot about how secure a company is.
- Techniques like dumpster diving and eavesdropping are very useful for this.
- For this you'd either need staff to report unusual incidents.
- Another way is to look for suspicious events on CCTV cameras.

#### OSINT Sources and Bulletin Boards.
- We can view OSINT data to see if there's anyone specifically talking about the organisation
- Another thing we can look for is new vulnerabilities that have been found and patches that have been released. These can be used to improve our defences.

## Indicators of Compromise Explained.
Used by automated defence software and analysts to perform exposure checks.

### Examples
- Email Addresses
- IP Addresses
- Domain Names
- URLs
- File Hashes
- File Names

### IOC Formats
#### STIX
- Structured Threat information eXpression
- Developed by MITRE and OASIS Cyber Threat
- It is a standardised language for sharing threat information
- Shares IOCs, Motivations, Abilities, Capabilities and responses

#### TAXII
- Trusted Automated eXchange of Intelligence Information
- Used as a platform to handle STIX information

### Mitre Att&ck Framework
- Adversarial Tactics, Techniques and Common Knowledge
- Knowledge base and model for cyber adversary behaviour
- Used for identifying APT behaviour

### Lockheed Martin Cyber Kill Chain
- Intelligence driver defence model
- Used for identification and prevention of cyber attacks.
- Does not fit with every attack type.


#### [1] Reconnaissance:

Attackers: Malicious actors will conduct research on the target organisation typically using both active and passive reconnaissance methods such as domain record lookups, public IP range port and vulnerability scanning, scouting out employees on social media, and more.

Defenders: Activity conducted by the attackers at this stage will come in the format of precursors, such as IPs that are performing port or vulnerability scanning, employees being approached by individuals that they do not know, and employees potentially receiving connection/friend requests on social media.

#### [2] Weaponization:

Attackers: Malicious actors create their own backdoor instead of purchasing commodity malware, and host this file on a domain they own. They then write a macro within a Microsoft Word document which connects to the attacker-owned domain and downloads the malware to the system where the file was opened.

Defenders: It is extremely hard for the security team to detect this stage, as it is not happening within their environment therefore they have no visibility of what happens outside the organisation (with the exception of cyber threat intelligence). Typical defences should be employed such as anti-virus, email security, and system hardening.

#### [3] Delivery:

Attackers: Malicious actors have crafted a spear-phishing email using information gathered on the target from OSINT sources. The email contains a Microsoft Office document with a malicious macro that will run malware in the context of the currently signed-in user.

Defenders: The security team should have email defences in place such as attachment sandboxing which should be able to detect any malicious attachments such as immediately malicious binaries or malicious Word documents or PDFs.

#### [4] Exploitation:

Attackers: Malicious actors have identified a vulnerability that, if exploited, can provide them with higher privileges than the current compromised account has, providing them with more access and the ability to perform more actions.

Defenders: The security team can prepare for this stage by hardening systems and performing vulnerability management processes to identify and remediate vulnerabilities that are both internal and externally present.

#### [5] Installation:

Attacker: Malicious actors install a backdoor and deploy persistence tactics and techniques to ensure that they can keep a foothold within the infected system, allowing continuous access.

Defenders: The security team can deploy endpoint detection and response (EDR) software agents to potentially infected hosts to allow for the detection, investigation, and eradication of a malicious presence.

#### [6] Command and Control:

Attackers: The malicious actor install malware that opens a channel between the malicious actor and remote machine, allowing them to send commands to the malware and attempt to gain the ability to complete step 7, actions on objectives.

Defenders: The defenders last step to fully stop the threat, prevention of command execution is key
#### [7] Actions on Objectives:

Attackers: The malicious actor was successful in their attack and has obtained keyboard-access, they are now able to attempt to complete any objectives they have.

Defenders: The defender must detect this stage as quickly as possible to prevent further damage and minimise the time that the attacker can complete their objectives.

## Attribution and its limitations.
Attribution is the determination of a cause or origin of an action

### Machine attribution
- Identifying which machines were used in an attack
- Log files are helpful with this
- Could involve multiple machines

### Human Attribution
- Finding the identity of the person responsible for an attack
- Very hard to do since credentials can be stolen.
- These are normally compared to a database so if the database is comprised the data cannot be trusted

### Ultimately Responsible Attribution
Finding the ultimately responsible party is usually the answer to most questions. You can find out who they are and their motives.

### Key Indicators to attribution
- Tradecraft – Frequently used behaviours such as an attacker’s techniques, tools and procedures used to conduct cyber-attack.

- Infrastructure – The physical machines or networks used in the attack; these are often compromised by other means before an attack.

- Malware – Malware can be specific to a threat actor; it can be reused or it can be modified quickly if a compromise is suspected to avoid attribution.

- Intent – The intent behind the attack, the motivation or reasoning.

- External sources – External reports from organisations like cyber security companies, media even students

### Cyber Attribution Techniques
Investigators use many different tools and programs to reveal information about attacks. Some distinctive techniques can identify different groups or individuals who perform attacks.

### Issues with Attribution
The main issue is working out which information is reliable. All information is good but alot of it has the possibility it could have been faked.
Some groups may try and copy a different attack so the intelligence researchers think it is someone else doing the attack.

## Pyramid of Pain
A visual representation of the amount of pain we can cause a malicious actor

- Hash values- trivial - can provide highest indicator of attack but can be easily modified
- IP Addresses - Easy - can easily change through VPNs Tor or proxies
- Domain names - Simple - These are easy to change but take a lot longer than IP Addresses
- Network/Host Artefacts - Annoying - it is much harder to change malware to get round of a defence than it is to change an IP
- Tools - Challenging - By stopping a tool working effectively, it can easily stop a hacker from breaking into your system.
- TTPs - Tough - These are not just tools but behaviour patterns, Forcing attackers to change their patterns could be time consuming for them since they are human and follow a certain pattern when carrying out an attack.
