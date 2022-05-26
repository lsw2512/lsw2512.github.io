---
title: "Digital Evidence Collection"
permalink: /Digital_Forensics_Collection/
layout: single
author-profile: true
---

## Equipment
- Forensic laptop of workstation 
- Electro-Static Evidence Bags with tamper proof stickers
- Labels to record evidence details
- Camera for photographs of crime scene
- Grounding bracelets 
- Hardware write blocker
- Blank hard drive to copy data on-site
- Wireless faraday boxes
- Specialized write blockers
- Phone jammer
- Dedicated flash drives ( contain tools like Encase, FTK CSILinux and MacQuisition)

## ACPO Rules
- These are guidelines on how evidence should be kept and presented
- A full-bit copy should be taken.
- A suitable hardware write-blocking unit should also be used where possible
- When providing evidence the examiner should display objectively and fair while being able to explain each process.
- This must include the acquisition and examination, so a third party could repeat the process and come to the same conclusion.
- The main principles are:
1. ACPO Principle 1

That no action is taken that should change data held on a digital device including a computer or mobile phone that may subsequently be relied upon as evidence in court.

2. ACPO Principle 2

Where a person finds it necessary to access original data held on a digital device, that the person must be competent to do so, and able to explain their actions and the implications of those actions on the digital evidence to a Court.

3. ACPO Principle 3

That a trail or record of all actions taken that have been applied to the digital evidence should be created and preserved. An independent third party forensic expert should be able to examine those processes and reach the same conclusion.

4. ACPO Principle 4

That the individual that is leading the investigation has overall responsibility to ensure that the ACPO principles are followed throughout the investigation.

## Chain of Custody
- Ensures all evidence has not been tampered with or accessed by unauthorised individuals.
- First thing to do is always create a HASH. This is the quickest and easiest way to ensure evidence integrity. Should always use at least two hash methods. Write blockers should be used when connecting to physical evidence
- Next is to make a forensic copy. If the hash value of the original is the same as a copy then the copy is an exact copy and can be analyzed.Evidence must be stored in antistatic bags and faraday cases. It must also be stored in locked containers. Only move when there is an authorized person to watch the transportation.
- Finally a chain of custody form should be kept. This should include a description of evidence, when and where it has been acquired or transferred.

## Disk Imaging: FTK imager
Can be used for:
- Dumping RAM and storing it in a .mem file, so we can output it to other tools such as Volatility for analysis purposes.
- Taking forensically-sound disk images that can be analyzed in tools such as Autopsy.
- Export files directly from disk images.
- Generate MD5 and SHA1 hashes for evidence files.
- Provide a read-only view of the contents of a disk image, exactly how the user would have seen it.
- And lots more!

### Capture Memory dump (on current system)
`File> Capture Memory`
Enter the location you want the memory dump to be stored, in the destination field.

### Hard Drive Imaging
`File > Create Disk Image`
Follow on screen prompt

## Live Forensics
- Focuses on investigating systems which are powered on.
- There are large amounts of RAM being used, once the system is powered off a lot of this data can be lost
- Some indicators can only be found in RAM or other volatile components
## Live Acquisition: KAPE
- Highly effective and configurable triage program.
- Used alongside disk image collection
 -Possible to deploy on a large scale
- TOPLEFT - can choose what information we want to retrieve from the target
- TOP RIGHT - modules to provide additional functionality
- Bottom -  builds command line query
- First provide target source
- Set location for where files will be saved
- Select targets like web browsers
- Click execute and a terminal will appear

##Evidence Destruction
After a case, evidence must be securely destroyed

### Degaussing
Uses magnets to wipe a hard drive

### File Shredding
Some programs can overwrite hard drive space with random letters to make sure files are not able to be recovered

### Physical Shredding
Physically shredding a hard drive to it cannot be put back together

### Hydraulic Crusher
Crushing a hard drive to make it unrecoverable
