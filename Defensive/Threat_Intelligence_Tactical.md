---
title: "Tactical Threat Intelligence"
permalink: /Threat_Intelligence_Tactical/
layout: single
author-profile: true
---

## Threat Exposure check
- Using multiple tools to look for IOCs they have retrieved from intelligence vendors.
- This is considered a tactical task since it requires deep technical understanding.

## IOC Watchlists
Watch lists are often used in SEIM environments to continuously scan for IOCs. This automates the process to free up time for the analyst

## Public Exposure checks
This is using OSINT techniques to find what information is publicly available about the company.

These can include:
- Image metadata
- Leaked information
- Warning signs of insider threats
- Brand abuse/impersonation
- Data Breach dumps

## Threat Intel Platforms
### What are tips?
- Can be deployed as a Saas or on-premises solution.
- Can contain: actors, campaigns, signatures, bulletins, and tools techniques and procedures (TTP)
- TIPS can do: Aggregation and normalisation  of intelligence, integration with existing security controls, and analysis and sharing of threat intelligence.

### Why use tips
- Puts all intelligence in one place
- Can automatically provide reports

### Data Aggregation
####Sources
- Open source
- 3rd Party paid
- Government
- Trusted Sharing Communities
- Internal

#### Formats
- STIX/TAXII
- JSON, XML
- Email
- .csv,.txt, PDF, word

#### TIP products
- Malware Information Sharing Platform (MISP)(Opensource)
- Threat Connect
- Anomali
- Threat Q

## MISP
- Malware information sharing platform
- Open-source
- Support sharing with network intrusion detection systems (NIDS), Host Intrusion Detection Systems (HIDS), and log analysis tools like SIEM

### What does MISP do
- Facilitate the storage of technical and non-technical information about seen malware and attacks
- Create automatically relations between malware and their attributes
- Store data in a structured format (allowing automated use of the database to feed detection systems or forensic tools)
- Generate rules for Network Intrusion Detection System (NIDS) that can be imported on IDS systems (e.g. IP addresses, domain names, hashes of malicious files, pattern in memory)
- Share malware and threat attributes with other parties and trust-groups
- Improve malware detection and reversing to promote information exchange among organisations (e.g. avoiding duplicate works)
- Create a platform of trust – trusted information from trusted partners
- Store locally all information from other instances (ensuring confidentiality on queries)

### How does MIPS work
- Efficient IOC database
- Automatic correlation finding
- Built in data sarong functionality
- GUI - advanced filtering
- Structured data storing
- Easy export features
- Easy import with a range of formats
- Flexible text import tool
- STIX support
