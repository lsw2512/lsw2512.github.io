---
title: "SIEM Logging"
permalink: /SIEM_Logging/
layout: single
author-profile: true
---

## What is logging?
- Detailed lists of application information, system performance statistics and user activity
- Can be useful to keep track of computer use, network activity, security issues and error reports

## Syslog
- Actions generate events which are logged on many devices
- Impractical to review these locally
- Available on unix and linux
- Can be used on windows
- Uses UDP 514 by default  TCP 514 can be used for more reliability
- Some more secure standards require TCP 6514 is used
- Made up for 3 components: priority value, header and message.

## Priority value
- Derived from facility code and severity level
- Use   (facility code * 8 ) + Severity Value = PRI 

Facility Code Numbers:

0. Kernel Messages
1. User-Level Messages
2. Mail System
3. System Daemons
4. Security/Authorization Messages
5. Nessages Generated by syslog
6. Line Printer Subsystem
7. Network News Subsystem
8. UUCP Subsystem
9. Clock Daemon
10. Security/Authorization Messages
11. FTP Daemon
12. NTP Sybsystem
13. Log Audit
14. Log Alers
15. Clock Daemon
16-23 Local Use 0-7

Severity Levels:
0. Emergency
1. Alert
2. Critical
3. Error
4. Warning
5. Notice
6. Informational
7. Debug

### Header
Contains information like timestamps, hostnames, application names, message IDs.

### Message
- Each message can either be plane text or machine readable
- First label is function/facility. For example, mail servers usually use the mail facility.
- Second label specifies the severity level. 
- The action is then specified which is usually a file in /var/log.

## Windows event Logs
- Binary files with the .evtx extension
- Stored locally in the windows directory of an operating system.
- %WinDir%\system32\Config*.evt
- %WinDir%\system32\WinEVT\Logs*.evtx
- Keep a detailed log of the majority of events
- Registered events include: Application, System, Security, Directory service, DNS and File Replication.

### Security Event logs
- Information about events which relate to the Windows Security Audit Policies
- Account logon events
- Account Management
- Privilege use
- Account Management
- Resource Usage

important Event IDs
- 4624 - An account Successfully logged in
- 4625 - An account failed log on
- 4647 - user initiated logoff
- 4648 - a logon attempt was attempted using explicit credentials
- 4649 - a replay attack was detected
- 4706 - a new trust was created to a domain
- 4720 - a user account was created
- 4726 - a user account was deleted
- 4732 - a member was added to a security enabled local group
https://www.andreafortuna.org/2019/06/12/windows-security-event-logs-my-own-cheatsheet/

## Sysmon
- Windows system service and device driver.
- Monitor and log system activity
- Logs process creation with fill command line for both current and parent processes
- Includes session GUID
- Logs loading of drivers and DLLs with their signatures and hashes
- Optionally logs network connections.
- Detects changes in file creation time.
- Rule filtering to include or exclude certain events
https://www.youtube.com/watch?v=9qsP5h033Qk&t=491s

### Installing Sysmon
Download sysmon, go to directory and run sysmon -i

## Other Logs
- Azure is usually monitored through Azure monitor and Log Analytic Workspace.
- Can automatically acquire logs from lots of devices
- Azure can be connected to lots of different siem platforms
- Uses kusto query language (KQL)

- Osquery is a universal and open source project developed by facebook
- Its an open source project
- Uses sql to explore data
- Creates one agent for multiple OS

## Aggregation
- Process of collecting logs, parsing them, extracting structured data then putting them in a format that's easy to understand
- Syslog - standard logging protocol, syslog server can be set up which receives logs from multiple sources
- Event Streaming -  Protocols like SNMP, Netflow adn IPFIX allow network devices to provide standard information about their operations.
- Log Collectors - software agents which run on network devices which capture logs parse it and send it to a centralized aggregator.
- Direct access - log aggregators that can directly access devices
- Structured data - usually logs for Apache, IIS, Windows events, cisco logs and some other manufacturers. They have clearly defined fields/
- Unstructured data -  usually from custom built applications. Most likely the majority of data being sent to siem