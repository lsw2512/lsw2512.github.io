---
title: "SIEM Correlation"
permalink: /SIEM_Correlation/
layout: single
author-profile: true
---

## Normalization and Processing
- Merges event containing different data into a reduced format
- Categorization is adding meaning to events
- Log Enrichment involves adding important information that can make the overall data more beneficial for security analysts. E.G adding geographical lookup information to logged IP addresses.
- Log Indexing - by indexing log data, you can search for specific attributes a lot quicker than having to scan every single bit of data.
- Log Storage - The amount of storage needed to support a SIEM can be a large amount, important to consider on premises to cloud storage.
- Process of changing log formats into a format that is as similar across all sources.

## SIEM Rules
- SIEM rules normally come in two forms: Provided by the SIEM provider, or human written by the defenders.
- Rules are queries that look for specific activity
- Certain alerts can be generated if a piece of data matches a rule

### Can monitor for:
Authentication/Account Activity:

- Failed logon attempts
- Successful (or failed) login attempts to disabled accounts
- Use of specific accounts (local administrator, administrator, domain administrator)
- SID (Security Identifier) changes to an account (a potential indicator of privilege escalation)

Process Execution:

- Execution from unusual locations (such as temporary directories or browser caches – may indicate malware execution or persistence mechanisms)
- Suspicious process relationships (such as Microsoft Word spawning a child process of CMD or PowerShell window (potentially a malicious macro that is executing code))
- Known bad hashes (MD5, SHA1, SHA256 hashes that are generated from confirmed malicious files)

Network Activity:

- Port scans
- Service enumeration
- Host discovery

### False Positive reduction and tuning
- Create rules that only show data if they match a specific criteria. E.G. only flag failed logins if someone failed over ten times within 10 minutes
- Another example would be telling the SIEM to ignore a specific IP which uses a vulnerability scanner to test the network

## SIGMA
- Way to share SIEM rules between different platforms
- Putting a SIEM rule into sigma will make it easier to change the SIGMA into a different vendor rule.
- Splunk, QRadar, ArcSight, Elasticsearch or logpoint support sigma

## REGEX
- REGEX stands for regular expression
- Its a text string which can be used to express a search pattern
- The can be used in: text editors, search engines, APIs, Data Entry Software, user input data validation, data analytics or web scraping
- Have a basis of perl programming language. But there are different variations
- Using -E you can use regular expression with GREP
- *(but)” would match with the exact work “but”
- “(g | f) at” would match any word with f or g in.
- [a-z]                        Match all characters from a to z (small letters)
- [A-Z]                       Match all characters from A-Z (capital letters)
- [0-9]                       Match all numbers from 0-9
- [a-zA-Z]                  Match all letters (any small or capital letter)
- [a-zA-Z0-9]            Match all letters and numbers (any small or capital letter or number)
- [^a-z]                      Match anything that is not between a to z(small letters) = No small letters
- [^A-Z]                     Match anything that is not between A to Z (capital letters) = No capital letters
- [^0-9]                     Match anything that is not between 0-9 = No numbers
- [^a-zA-Z]                No alphabets = Match only numbers
- [^a-z0-9]                Match anything except small letters and numbers = Match only capital letters and other characters.

### Character class
Matches any one of a set of characters
- /s            matches any whitespace characters such as space and tab
- /S            matches any non-whitespace characters
- /d            matches any digit character
- /D           matches any non-digit characters
- /w           matches any word character (basically alpha-numeric)
- /W          matches any non-word character
- /b            matches any word boundary (this would include spaces, dashes, commas, semi-colons, etc)
- ( )            Used to group elements of an expression together.
Eg.           ([a-z]\d+) will match any lowercase letters followed by a number “btl1”
- (*)           Matches the preceding character or set of characters for 0 or more times.
Eg.           (12*3) would match: 12, 123, 1223, 122333444 …
- (+)           Matches with repeating character or set of characters for at least 1 or more times.
Eg.           (1+23) would match: 123, 1223,
- { }        Curly braces are used to repeat the preceding character or set, for as many times as specified.
Eg.        \w{2} will match oo in Book.
- (.)           Wildcard                Can be used to match any symbol.
Eg.          .*  Matches any symbol any number of times.
- ^              Match at the start of the lines or string.
Eg.           ^\d  will match with  “0” in “07123 12345”.
- $              Match at the end of the line or string or before \n
Eg.           \w{2}$  will match with  “OO” in “BOO”.
- ?              Optional Character              denotes the preceding character may or may not be present
Eg.           “docx?” would match docx or doc

## Real world Regex
- Matches website hostname: www.[a-z]+\.(\.?[a-z]+)+
- Matches email addresses: ^([a-zA-Z0-9_\-\.]+)@([a-zA-Z0-9_\-\.]+)\.([a-zA-Z]{2,5})$
- Matches US phone numbers (123-123-1234): ^\([0-9]{3}\)[0-9]{3}-[0-9]{4}$
- Matches UK phone numbers (07123456789): (((\+44)? ?(\(0\))? ?)|(0))( ?[0-9]{3,4}){3}

Splunk
```
Index = dataset you want to search against
earliest = look for first event
AllTime = finds all data
Sampling - edits how many events splunk searched through
Fields - can look for specific information
sourcetype= the logs source e.g. syslog
Search src=  search by the source of the packet
Search dst= search by packet destination
Search src= OR dst=  search source or destination
* wildcard to mean anything
Search pass* AND fail* - searched for logs with pass and fail in them
top/rare = displays most/least common
```
`index="botsv1" earliest=0 Image="*\\cmd.exe" | stats values(CommandLine) by host`

The above search query is using a new parameter, “Image=”. This is derived from Sysmon logs, such as Event ID 1, ‘New Process Created’. The Image field in Sysmon events shows the executable that has generated the process, in this example, cmd.exe, which should be located at C:\Windows\System32\cmd.exe (but we can wildcard the path). After the search for cmd.exe, we’re retrieving the events using values(CommandLine) to show what commands were used, and finally sorting it per host. Let’s see how this search looks once it has been run (with no event sampling):

### Creating Alerts
- Alerts trigger when log criteria meet specific criteria
- Creating alerts can be split into 4 stages: search query, search timing, Alert Triggers, Alert Actions
- Search Query - work out what you want to detect
- Search timing - Set how often splunk will run this search
- Alert Trigger - create a trigger e.g. only alert if there are over 10 login failures in a row
- Alert Action - set an action (send email, add an alert)

### Creating own rules
- First write a query then save as alert
- Give title
- Choose permission - private (only you can access) or shared in app (all users can view)
- Select alert type -  scheduled alert (will search at defined intervals) or real time alerts
- Select trigger action - what you want to happen

### Creating Dashboards
- Collection of panels displaying different data
- Important information - firewall graph, number of alerts/offences, number of alerts closed, traffic flow, attack map, event types per alert over 24 hours
- To create a dashboard first create a report
- Name with <group>_<object>_<description>
- group: the name of the group or department using the knowledge object such as sales, IT, finance, etc.
- object: report, dashboard, macro, etc.
- description: WeeklySales, FailedLogins, etc.
- Go to report and press add to dashboard
- Dashboard Title – Set an optional human-readable name for the dashboard.
- Dashboard ID – Set an identification number for the dashboard.
- Dashboard Description – Set an optional description of what the dashboard’s intended purpose is.
- Dashboard Permissions – It’s usually a good idea to keep the permissions set to Private until the dashboard has been tested.
- Panel Title – Set an optional name for the panel within a dashboard.
- Panel Powered By – Select the search query that powers the panel, either by writing a query in the ‘Inline Search’ box, or clicking on ‘Report’ and finding your saved report.
