---
title: "Incident Response Containment, Eradication and Recovery Phase"
permalink: /Incident_Response_CER/
layout: single
author-profile: true
---

## Incident Containment
- There are several ways to contain incidents
- Strategy to contain incidents
- Determines what tools and techniques can be used to contain the incident 
- Short term containment is a quick fix, used to prevent further damage.
- Long term containment is an enterprise wide fix. 
- Perimeter containment - block inbound/outbound traffic, ids/ips filter, web application firewall policy and Null route DNS.
- Network Containment - vlan isolation, router based segment isolation, port blocking, ip or MAC address locking, Access control list.
- Endpoint Containment - disconnection of the infected system from any network connections, powering off the infected system, blocking rules in firewall, HIPS action.

## Removing Malicious Artifacts
- Malicious artifact is an object with malicious purposes.
- Sysinternals process explorer can help with finding malicious processes
- Netstat and process monitor can help detect malware which uses network connections
- Sysinternals rootkit revealer can help detect rootkits or malware
- If there is a back up this can be used to restore the pc to an uninfected state
- Antiviruses can scan the computer to find and remove malware
- Some antivirus solutions have standalone tools which dont require installation to run

## Root cause and recovery
- Take a forensic image to find the root cause so it can be analyzed later and the infected computer can be recovered and put back online. 
- Patching systems with program, operating system, and security updates to ensure that any vulnerabilities are fixed. Manual testing should be conducted after patching to ensure the fix has worked.
- Disabling services that are not needed on a system.
- Update endpoint detection and response (EDR), anti-virus (AV), intrusion detection and prevention system (IDPS), and SIEM rules to allow for monitoring and alerting of similar activity that occurred during the incident.
- Share intelligence regarding the incident, such as indicators of compromise, with other organizations to allow them to improve detection and perform threat exposure checks across their environments.
