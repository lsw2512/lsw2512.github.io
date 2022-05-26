---
title: "Linux Digital Forensics"
permalink: /Digital_Forensics_Linux/
layout: single
author-profile: true
---
## Linux Artifacts
- /etc/passwd and /etc/shadow
- Used to keep track of every user who has access to the system.
- /passwd contains information about accounts
- /shadow contains information about passwords
- John the ripper can be used to decrypt password hashed in the shadow file.
- John <file> --wordlist=rockyou.txt

## /Var/Lib /Var/Log
On debian, if you go to /var/lib/dpkg/status, it lists all software packaged which are installed on the system

## User Files
### Bash History
- The .bash_history file is located in a user's home directory
- Reading the bash history file and using the history command could have the same output. However the history command can be cleared but this does not clear the bash history file.

### Hidden Files
- Files starting with a . are hidden from viewing.
- These can be viewer by using ls -la

### Clear files
These are files which can be viewed normally.

## Steganography
This is hiding text or data within other types of data

### Hiding Zip files within images
- Using the command: cat <image> <Secret zip file> > <image2>
- This will hide the zip inside the first image and output a new image
- To get this secret file out, simply unzip the image, which the secret file is hidden in

### Steghide
- Steghide can do the exact same thing as the thing above. However, its password protects the file we are hiding data inside of.
- Steghide embed -cf image.jpg -ef secretmessage
- To extract this sata you use: steghide extract -sf image.jpg

### Hiding strings in metadata
- Exiftool can be used to hide information in metadata
- Exiftool -comment=”Super Sneaky!” Dog.jpg
- View This by using: exiftool <file>

## Volatility
- Open-source memory forensics framework
- Written in python and supports windows, mac and linux

Features:
- List all processes that were running.
- List active and closed network connections.
- View internet history (IE).
- Identify files on the system and retrieve them from the memory dump.
- Read the contents of notepad documents.
- Retrieve commands entered into the Windows Command Prompt (CMD).
- Scan for the presence of malware using YARA rules.
- Retrieve screenshots and clipboard contents.
- Retrieve hashed passwords.
- Retrieve SSL keys and certificates.
- And lots more!

###  Usage
- First use the command “volatility -f memdump.mem imageinfo”
- When running commands of memory images use the suggested profile which is shown in the first command
- --profile=win..
### Command List

```
volatility -f memdump.mem imageinfo // Take memory image “memdump.mem” and determine the suggested profile for analysis. The profile is the operating system, version, and architecture.
volatility -f memdump.mem --profile=PROFILE pslist // Take memory image, provide the profile, then use the pslist plugin to print a list of processes to the terminal.
volatility -f memdump.mem --profile=PROFILE pstree // Use the pstree plugin to print a process tree to the terminal.
volatility -f memdump.mem --profile=PROFILE psscan // Use the psscan plugin to print all available processes, including hidden ones often used by malware (compare this to pslist to see if there’s any differences!).
volatility -f memdump.mem --profile=PROFILE psxview // Use the plugin psxview plugin to print expected and hidden processes. This is a combination of pslist and psscan plugins.
volatility -f memdump.mem --profile=PROFILE netscan // Use the plugin netscan to identify any active or closed network connections.
volatility -f memdump.mem --profile=PROFILE timeliner // Use the timeliner plugin to create a timeline of events from the memory image.
volatility -f memdump.mem --profile=PROFILE iehistory // Use the iehistory plugin to pull internet browsing history.
volatility -f memdump.mem --profile=PROFILE filescan // Use the filescan plugin to identify any files on the system from the memory image.
volatility -f memdump.mem --profile=PROFILE dumpfiles -n --dump-dir=./ // Use the dumpfiles plugin to retrieve files from the memory image. In this case our terminal is open in the Desktop (root@SBTLab2:~/Desktop) and we are using the output location ./ which tells Volatility to put the files in our current location, the Desktop.
```
