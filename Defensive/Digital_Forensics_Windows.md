---
title: "Digital Forensics on Windows"
permalink: /Digital_Forensics_Windows/
layout: single
author-profile: true
---

## Program artifacts
### LNK FILES
- LNK files are used by windows to link one file to another
- You can collect a lot of data like when the link was created, modified, last accessed, file size and more.
- LNK files can be found at: C:\Users\$Users$\AppData\Roaming\Microsoft\Windows\recent
- Use windows file analyzer

### Prefetch Files
- Can provide information about programs including the name of the application, executable file path, when it was last run and when it was installed/created.
- Can be found at C:\Windows\Prefetch
- Use prefetch explorer command line

### Jump list
- Using the jump feature we can find two files: automaticDestionation-ms and customDestination-ms
- These contain information about application pinned to the taskbar
- Can be found at; C:\Users\% USERNAME%\AppData\ Roaming\Microsoft\Windows\Recent\AutomaticDestinations
- C:\Users\%USERNAME%\AppData\ Roaming\Microsoft\Windows\Recent\CustomDestinations
- Use Jump List Explorer to analyze these files.

### Internet Browser Artifacts
- Cookies
- Favorites
- Downloaded Files
- URLs
- Searches
- Cached Web Pages
- Cached Images

### KAPE
- Choose output destination
- Choose target browsers
- Go to the output folder and there should be a lot of information.

### Browser History Viewer
- Run browser history capturer to capture files.
- Use browser history viewer to view these files
