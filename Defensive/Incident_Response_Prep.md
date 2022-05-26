---
title: "Incident Response Preperation Phase"
permalink: /Incident_Response_Prep/
layout: single
author-profile: true
---
## Incident Response Plan
Split into six sections: Preparation, Identification, Containment, Eradication, Recovery, Lessons Learned.

### Preparation
- Requires most attention
- Develop response plans for different incidents
- Run simulated scenarios 
- Ensure all resources are approved and ready to use (laptops, notebooks, software, forensic equipment, training and ability to abandon normal responsibilities)
- Continually train and evaluate performance of incident response team

### Identification
- Ability to identify and analyze incidents
- Guidance on how to report an incident
- When did the incident occur?
- Who discovered it?
- How was it discovered?
- What systems or business units have been affected?
- Does it affect the organization's ability to operate?
- Scope of the incident?

### Containment
- Crucial to contain an incident
- Outline actions which need to be taken to contain the incident 
- This is also when evidence is collected
- Backups should be kept to replace the affected systems

### Eradication
- Analysis needs to be conducted to work out exactly what has happened
- MITRE ATT&Ck can be used to work backwards
- Work towards finding the route cause
- Guidelines should guide this process
- List of appropriate resources should be provided
- Once things are found start to remove malicious artifacts
- Make sure vulnerabilities are patched so they cannot be used again
- Defensive measures should be updated 

### Recovery
- All about returning business operations to normal
- Guidelines should be provided to ensure systems are no longer infected.

### Lessons Learned
- Once the investigation and response is complete a meeting should take place.
- Recap what happened
- How the response could be improved
- Lessons learned from simulated and real events

## Incident Response Teams
- We need them to ensure continuity and reduce the cost as a result of an attack
- Incident Commander - individual in charge of dealing with an incident
- Security Analyst - deep technical understanding of security
- Forensic Analyst - retrieve evidence so it is clear how the attack was conducted.
- Threat Intelligence Analyst - provide context
- management/ c-suite - responders will have resources they need
- Human Resources - incase an employee is involved
- Public Relations - incase the incident affects the public, employees or customers (law to be announced as soon as possible)
- Legal - provide legal advice

## Asset Inventory and Risk Assessments
Need these so we know what we have to protect and what is the most important to protect.

### Asset inventory
- Inventory of IT systems, servers, desktops, laptops, network equipment and mobile devices.
- Will allow for thorough risk assessment
- Ask IT staff to make a list of all equipment
- Conduct passive reconnaissance using a network sniffer
- Conduct an active reconnaissance scan

### Risk Assessment
- Works to determine what systems are most critical to the business
- When a risk is identified protective measures should be taken to protect it
- But only take measures to the amount of risk
- 4 approaches to risk- transfer the risk (insurance) accept the risk ( not spend any resources on a low impact risk) mitigate the risk (apply security controls) Avoid the risk ( taken offline to cannot be exploited)

## DMZ
- Use multiple layers of security to slow down the attacker
- DMZ - physical or logical subnet that separates an internet local area network from an untrusted network.
- Resources are directly accessible from the network and the lan
- Used to protect sensitive organizational systems and resources
- Isolate and keep potential target systems separate from internal networks
- Reduce and control access
- Any service provided to users on the public internet should be placed here
- Web servers, proxy servers, email DNS FTP and VoIP should be in DMZ
- Allows for access control for organizations
- Prevent attackers from performing network reconnaissance ( even from a compromised device in the DMZ)
- Can protect against IP spoofing

## Host Defenses
- HIDS - software installed on an endpoint to allow for detection of suspicious activity
- HIPS - installed on endpoint like HIDS but can prevent attacks as well
- Anti virus - detects malware
- Event monitoring - send logs to a centralized location
- EDR- like HIDS but reports back to SIEM platforms
- Local Firewall - can provide tighter security

### Group Policies
- Used for data security
- Collection of settings sysadmins create with microsoft management console group policy editor
- Can be associated with one or more of AD containers
- Applies GPO in this order: local, site, domain and then OU
- Can help with ease of management
- One stop administration (easily deploy updates)
- Password Policy Enforcement
- Folder Redirections
- GPOS randomly update ever 90 - 120 minutes
- If you set gpo update too low it will kill network traffic
- Learning to do this in powershell could be easier

## Network Defenses
### Network Intrusion Detection
- NIDS - can come in form of software or physical
- Can be positioned inline - sat directly in the path of network traffic
- Network tap - connected by tapping into physical connection
- Passive - using a SPAN port 
- Used to generate alerts so that human analysts can investigate and take action
- Snort - world leading and free to use
- Suricata - free but works at application layer
- Zeek - free 

### Network intrusion Prevention
- Similar to NIDS but takes defensive measures
- All NIDS listed above can work as prevention systems

### Firewall
- Used to separate parts of a network
- Traditional - used to filter IP addresses and protocols
- Next gen - can inspect packets, use OSI model
- Webapp firewall - this is a proxy server that stands between an application running on a server and users who access the application from outside the corporate network

### Event Monitoring
- Siem can be used to provide a dashboard for a large number of logs
- These can include web proxy logs and perimeter firewall logs

### Network Access Control
- Pre admission - NAC can work to prevent rogue or non-compliant devices from connecting to a private network. Could require any device connecting needs the most recent patches most common on BYOD or guest networks
- Post admission - the ability to enforce restrictions once a device joins the network, this could be defining what resources the device can access.

### Web Proxy
- Decides if a client can connect to a specific website or not
- Can block sites which are known to be malicious

## Email Defenses
- SPF - Sender Policy Framework - type of DNS TXT record which can help prevent an email address from being forged
- DKIM is a method of email authentication that cryptographically verifies if an email has been sent by its trusted employers, can verify if the contents of the email has been tampered with or not
- DMARC - Domain based message authentication reporting and conformance -  email authentication, policy and reporting protocol. Built off concepts of SPF and DKIM aswell as adding several improvements
- Allows the domain owner to specify what should happen if the email fails.
- Marking external emails -  Employees must understand the risk of external emails marking them could make them think twice
- SPAM Filter - can filter emails from known spam addresses or layouts/content
- Data loss prevention - name given to security controls that work to prevent business information leaving an organisation. Can monitor at different levels: body, head attachments. Can stop emails being sent out
- Sandboxing - can extract attachments and run them in virtual environments to determine if they are malicious or not. 
- Can restrict attachments which are unlikely to be used by the organisation, e.g. EXE
- Security awareness training -  most important security defence against phishing

## Physical Defences
- If an attacker gets physical access to the system it's game over.
- Deterrents: Warning Signs, Fences, Guard dogs, security Guards and security lighting.
- Access Control: mantraps, Turnstiles, gates, electronic doors and security guards
- Monitoring Controls: CCTV, Security Guards and Intrusion detection systems.

## Human Defences
- Security Awareness Training
- Security Policies - used to protect the business from humans, state what employees can and cannot do with company equipment.
- Incentives - rewards for people who are security concious
- Phishing simulations - done quarterly, test how effective the current awareness program is, sophos phish threat, gophish open source, trend micros phish insight and phishing box.
- Whistle blowing, anonymous tips on security incidents provided to employees,
