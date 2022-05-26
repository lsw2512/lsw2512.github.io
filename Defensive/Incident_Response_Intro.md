---
title: "Incident Response Introduction"
permalink: /Incident_Response_Intro/
layout: single
author-profile: true
---

Incident response is the methodology an organization uses to respond to and manage a cyber attack.

- Benefits wider business by reducing the impact of successful attacks and allowing business operations to remain as uninterrupted as possible.
- Companies can suffer due to data breaches so it is important to have a good incident response strategy 
- Uber was fined £385000, Equifax £500000, Marriott £99 Million and British Airways £183 Million.
- Smaller companies may close or change how they operate due to this. 
- Incident response is not just about data breaches but any IT or data incident which could pose a risk to the company.

## Events vs Incidents

- All security incidents are security events, but not all events become incidents.
- A security event is anything that could have security implications.
- These could include: Spam, vulnerability scans, reconnaissance scans, an explained anomaly, a user downloading software or a brute force attack.
- A security incident is an event which has resulted in damage to the organization.
- Spam email - if it contains malware which is used this would be a security incident
- If a actor exploits a vulnerability after a scan this is a incident
- An unexplained anomaly is classed as an incident until is has been properly scoped
- A user downloads software, this turns out to be malware, this will then be an incident
- A successful brute force attack is also an incident, an unsuccessful one is an event.

## NIST I.R Lifecycle
- Procedure of handling incidents.
- Split into: preparation, detection and analysis, containment eradication and recovery and post incident activity.

### Preparation
#### Activities for preparing for incidents: 
- Contact information for stakeholders
- War room for central communication and coordination
- Documentation
- Baselines on running systems
- Equipment which can be used (forensics toolkit)

#### Activities for preventing incidents
- Having current risk assessments
- Utilizing client and server security
- Having a user awareness and training program

### Detection and Analysis
- Set up SIEM, IDS IPS log monitoring, ect to automatically notify people of anomalies
- Record baseline information to identify anomalies
- Responders need to effectively document findings when analyzing the network, as well as prioritize the next steps
- A plan also needs to be created to outline who needs contacting in the case of an event.

### Containment, Eradication and Recovery
- Contains two sub-phases: containment, eradication & recovery

#### Containment
- Should include:
- Potential damage to and theft of resources
- Need for evidence preservation
- Service availability
- Time and resources needed
- Effectiveness
- Duration of the solution
Also important to keep a detailed log of all evidence you find regarding the attack. This could be information used to prevent further tactics or next steps in the attack.

#### Eradication & recovery
- Act of returning systems back to normal
- Rebuilding machines from good backups, deleting malware or resetting credentials.
- Restoring systems to pre-attack state
- Eliminating vulnerabilities which were exploited

### Meeting
After hold a meeting to address these questions:
- Exactly what happened and when did it happen?
- How well did staff and management perform in dealing with the incident?
- What information was needed sooner?
- Were any steps or actions taken that might have inhibited the recovery?
- What would staff and management do differently the next time a similar incident occurs?
- How could information sharing with other organizations have been improved?
- What corrective actions can be taken?
- What indicators should be watched for in the future?
- What additional tools or resources are needed to mitigate future incidents?

## CSIRTS and CERTS
- Team of specialised people who can respond to incidents.
- CERT - Cyber Emergency Response Team
- CSIRT - Cyber Security Incident Response Team
- Responsible for coordination and responding to IT security incidents.
- CSIRTs often contain key stakeholders.
- Have a central communication point for incident information
- Promote security awareness and training
- Act as emergency contact for cyber security 
- Investigate new security vulnerabilities
- Determine MTTR and MDT for company assets
- Provide useful information to the cybersec community 

###  Public vs Private
- Cert is usually for teams in countries and csirt is associated with businesses
