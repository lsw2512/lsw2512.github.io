---
title: "Incident response Lessons Learned and reporting"
permalink: /Incident_Response_LLR/
layout: single
author-profile: true
---
## What Went Well
- While reflecting on the response to the incident it is important to concentrate on how it went well.
- Staff should be appraised for responding to the incident
- This helps combat imposter syndrome and burnout.

## What can be improved
- Identifying weaknesses in the response can help the team perform better against a future incident
- This is not just what went wrong but why. Did everyone have the resources they needed?
- Did the tools or equipment have any limitations?
- Does the budget for incident response or forensics need increasing?

## Importance of Documentation
- Incident response case notes can be recorded with a tool, this needs to be kept updated so it contains everything it needs to 
- Incident response plan should be kept updated for new threats or tools
- Reviewing run-books for the type of incident can help improve future responses by providing better guidance
- Policies should be updated to stop new incidents

## Incident Response Metrics
- Metrics are numerical values for quantitative assessment.
- Can highlight where your team has responded efficiently or effectively

### Impact Metrics
- Service level Agreement - an agreement with the customer to determine expectations with uptimes. Usually in percentage
- Service level objective - determines the specific metic being measures in a SLA
- Escalation rate - measure how often alerts in your SIEM are being assigned to the correct member

### Time based metrics
- Mean Time to detect - average time for the security team to take notice an incident has occurred.
- Mean time to response - the mean time to repair , resolve or recover from the incident.
- Incident over time - average incidents over a length of time
- Remediation time. - how long it takes for the situation to be remediated.

### Incident type metrics
- Cumulative number of incidents - total number of incidents based on their type ( put into categories)
- Alerts created per incident - how many alerts were created for one incident
- Cost per incident - the cost a incident cost the company

## Reporting Format
- Executive Summary
- Incident Timeline
- Incident Investigation
- Appendix

### Executive Summary
- High-level overview of the incident
- Non technical
- Clearly states business impact
- Should be one page and focus on areas like: business risk, financial cost, damage occurred, damage prevented. 
- Highlight the work of the security team and how they prevented more damage and cost from happening.
- The cost of running a security team is less than the incident.

### Incident Timeline
- The timeline will provide the date, time and short description of all key events
- Order of actions taken or discovered.
- Use either local timezone or universal time coordinated.

### Incident Investigation
- Main bulk of the report
- Step by step documentation of actions that were conducted
- All stages of the incident response lifecycle should be considered and reported on.

### Appendix
- Used as storage for the report
- Will include images, graphs and tables, IP address list. Anything that takes up alot of space

### Report template
- One template will not work for everyone
- https://www.paloaltonetworks.com/resources/whitepapers/incident-response-reporting-template

## Reporting Considerations
### Audience
- Think about what audience will be reading each section
- Executive summary - short, sweet, talk about the incident at a whole
- Rest of report - technical, alot of detail is included.

### Incident Investigation
- Really detailed
- Any points need backing up with evidence 
- Make a point then provide evidence
- Also important to include the MITRE ATT&CK tactic which was used

### Screenshot and captions
- Use screenshots to provide evidence
- Take as many screenshots as you can 
- All images should be captioned with a summary   about one or two sentences
