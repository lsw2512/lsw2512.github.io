---
title: "139/445 SMB"
permalink: /139-445-SMB-Samba/
layout: single
author-profile: true
---

Samba is a service that enables the user to share files with other machines. It has interoperability, which means that it can share stuff between linux and windows systems. A windows user will just see an icon for a folder that contains some files. Even though the folder and files really exist on a linux-server.

# Connecting
For linux-users you can log in to the smb-share using smbclient, like this:
smbclient -L 192.168.1.102
smbclient //192.168.1.106/tmp
smbclient \\\\192.168.1.105\\ipc$ -U john 
smbclient //192.168.1.105/ipc$ -U john  

-L retrieve list of shares
-N suppress password prompt

If you don't provide any password, just click enter, the server might show you the different shares and version of the server. This can be useful information for looking for exploits. There are tons of exploits for smb.
So smb, for a linux-user, is pretty much like an ftp or a nfs.

Here is a good guide for how to configure samba: https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20(Command-line%20interface/Linux%20Terminal)%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!

mount -t cifs -o user=USERNAME,sec=ntlm,dir_mode=0077 "//10.10.10.10/My Share" /mnt/cifs

# Connection with PSExec
If you have credentials you can use psexec you can easily log in. You can either use the standalone binary or the metasploit module.

use exploit/windows/smb/psexec

# Scanning with nmap

nmap -p 139,445 <ip>/24 

There are several NSE scripts that can be useful, for example:

ls -l /usr/share/nmap/scripts/smb*

nmap -p 139,445 192.168.1.1/24 --script smb-enum-shares.nse smb-os-discovery.nse

# nbtscan

nbtscan -r <ip>/24

It can be a bit buggy sometimes so run it several times to make sure it found all users.

# Enum4linux

Enum4linux can be used to enumerate windows and linux machines with smb-shares.

The do all option:

enum4linux -a <ip>

For info about it ere: https://labs.portcullis.co.uk/tools/enum4linux/

# rpcclient

You can also use rpcclient to enumerate the share.
Connect with a null-session. That is, without a user. This only works for older windows servers.

rpcclient -U "" <ip>

Once connected you could enter commands like
  
srvinfo
enumdomusers
getdom hwinfo
querydominfo
netshareenum
netshareenum all
