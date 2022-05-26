---
title: "Digital Forensics Fundermentals"
permalink: /Digital_Forensics_Fundamentals/
layout: single
author-profile: true
---

## Data representation
### Binary
- Represented with 1’s and 0’s.
- This represented the flow of electricity in computing devices
- Boolean
- One bit - single binary value
- One byte - contains 8 bits
- Large files can contain several thousand bytes

### Base64
- Reversable encoding algorithm
- This can change things into a text string. Which can be reversed to retrieve its original data

### Hexadecimal
- AKA - hex, base16
- Uses 0-15  and uses 0-9 numbers then 10-15 is represented by the letters A-F

### Octal
- Uses numbers 0-7

### ASCII
- ASCII is the american standard code for information interchange.
- UNIX and DOS-based operating systems use ASCII for text files.
- Windows NT and 2000 use unicode.

## Hard Disk Drive Basics
- Non-volatile memory hardware device
- Commonly used as the main storage in a desktop computer or laptop
- Usually connected to motherboard or in an external caddy
- Platters are the circular disks where magnetic data is stored in a hard disk drive
- A sector is a subdivision of a track on a magnetic disk.
- Each sector stores 512 bytes, newer ones can store 4096 - byte sectors
- A cluster is a group of sectors
- Slack Space is the leftover storage which exists on a computer's hard disk
- Slackspace can contain remains of deleted files.

## SSD
- New generation storage device
- Data is written to pages and once there's enough, it's written to a block on the drive
- Garbage collection is a process used by SSDs to optimize space and improve efficiency
- The goal of garbage collection is to keep as many blocks as possible
- The controller looks for deleted or modified sata and moves the used pages to a new block.; It then erases the old block removing the deleted/unused data.
- If you collect an SSD it has to be removed immediately to stop garbage collection.  Either perform a hard shutdown or remove the cable from the physical drive
- Moving files to the recycling bin does not delete them. It tells the OS that these files are ok to be overwritten.
- Trim is similar to garbage collection, where it selects data and clears it
- The same precautions should be taken as dealing with garbage collection
- Wear levelling is a technique that some SSDs utilize to increase the lifetime of the memory.
- They distribute writing on all block of an SSD so they wear evenly
- A blocks receive the same number of writes to avoid writing too often

## File Systems
Set of data types which are for
- Data storage
- Hierarchical categorization
- Data management
- File navigation
- Accessing the data
- Recovery of data

### FAT16
- Original filesystem for DOS and Windows 3
- Very small partitions

### FAT32
- First introduced in win98
- Uses 32 bits for data identifying
- Compatible with a huge variety of devices
- Cross compatible with almost all OS’s release after 1995
- Can only work with files less than 4GB
- Only works with partitions less than 8TB
- No data protection in case of power loss
- No built in file compression features
- Not designed to be secure

### NTFS
- Proprietary journaling file system developed by microsoft
- Improved support for meta data and advanced data structures
- Supported by other OS like linux

### EXT3/4
- These are divided into userspace, kernel space and disk space.
- Ext3 is commonly used by linux kernel
- Uses journaling (keeping track of changes in the filesystem.
- EXT4 - max volume size of data is 1exbibyte
- Maximum 56 byte filename.

## Digital Evidence and Handling 
- Trace evidence is often left behind.
- This evidence can easily be tampered with so all evidence needs to be verified before it can be trusted.

### Types of digital evidence:
- E-mails
- Digital Photographs
- Logs
- Documents
- Messages
- Files
- Browser History
- Databases
- Backups
- Disk Images
- Video/audio files

### Handling
- Handling and securing of evidence is critical
- Actions taken by digital forensic teams should not alter the original evidence
- Proper documentation and justification of actions can help prevent evidence from being dismissed if evidence is altered.
- Use both hardware and software write blockers to stop data being altered.
- Everything should be documented

### Order of Volatility
- Volatile evidence is evidence that can be lost if a system is powered down.
- Registers and cache - contents of CPU is very volatile, nano seconds could be the difference between retrieving or losing data
- Routing table, ARP Cache, Process Table, Kernel Statistics, Memory - highly volatile
- Temporary File Systems -  less volatile, but very important
- Disk - less volatile but processes could overwrite data
- Remote logging and monitoring data - High volatile but not as important
- Physical configuration, network topology and archival media - either not vital or not volatile.

### Metadata and File carving
- Metadata is data about data
- File carving is a process of searching for files in a data steam and is used to retrieve deleted files from disk images

#### Metadata
- Look under the details tab in properties (windows)
- Use either “ls -lisap <file>” or “stat <file>”
- Exiftool is also an amazing tool to use

#### File Carving
- Tool: scalpel
- First tell scalpel what to detect: /etc/scalpel/scalpel.conf
- Uncomment the files you want to detect
- Use scalpel by the following command: “scalpel -b -o <output> <disk image file>”

## Memory, Pagefile and Hibernation file
### Memory
- A device used to store information for immediate use in a computer
- This is an analysis of volatile data to find data which is not easily detectable on a hard drive
- A memory dump is a snapshot or capture of computer memory from a specific instant
- Attack data can often only exist in system memory instead of file memory.

### Pagefile
- Pagefile.sys is used within windows OS to store date from RAM when it becomes full
- Can change size or be deleted which will change the speed of the computer.
- If deleted the system will not operate properly but it can be configured to store it on a different hard drive

### Swapfile
- Linux version of page file
- Traditionally this is a partition but can be set up as a swapfile
- Easier to change size of swapfile than partition
- Sudo fallocate -l [filesize] /swapfile   changes size of swapfile once swapfile is temporarily disabled
- To work out how much space is available use free -h
- Swapon -show can identify is its a file or partition
- Can also adjust how frequently the swap space gets used

### Hibernation file
- Introduced in windows 2000
- Allows OS to store current state of operation when computer is turned off
- This copies everything from memory to a file called hiberfil.sys on the disk

### Hashing and Integrity
- Hash values are text strings
- They provide a unique identifier for a file
- In forensics, a hash will be taken before a system is copied. A hash of the copied system will then be taken. If both are the same then these are exact copies.
- Hashcat can be used to perform dictionary attacks against hashes
- This is most often used against credentials
- Hashcat -m 0 <hashfile.txt> <wordlist.txt>
