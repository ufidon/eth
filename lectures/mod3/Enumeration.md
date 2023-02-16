# Enumeration

Objectives
---
- Describe the enumeration step of security testing
- Enumerate Microsoft OS targets and services
- Enumerate *nix OS targets and services


What is enumeration?
---
- Enumeration extracts information about:
  - Network topology and architecture
  - Resources or shares on the network
  - Usernames or groups assigned on the network
    - Information about users and recent logon times
- Before enumeration, footprinting and Port scanning are used to
  - To Determine OS being used
- Intrusive process
  - not only identifying a resource, but also attempting to access it
  - get written permission first
    - have a Rules of Engagement (ROE) and a Statement of Work (SOW) in place


NBTscan
---
- NBT (NetBIOS over TCP/IP)
  - is the Windows networking protocol
  - used for shared folders and printers
- NBTscan
  - Tool for enumerating Microsoft OSs


Practice ✏️ 
---
- On Kali, use NBTscan to enumerate Windows VM
  ```bash
  # 1. find the usage of nbtscan
  nbtscan -h
  # 2. enumerate windows vm
  nbtscan windows_vm_ip # windows_vm_ip is found with nmap from Kali
  nbtscan nat_network_id/24 -r
  ```


Enumerating [Microsoft Operating Systems](https://microsoft.fandom.com/wiki/Microsoft_Windows)
---
- Study [OS history](https://en.wikipedia.org/wiki/Microsoft_Windows_version_history)
  - Knowing your target makes your job easier
- Many attacks that work for older Windows OSs still work with newer versions


Windows 95
---
- The first Windows version that did not start with DOS
- Still used the DOS kernel to some extent
- Introduced the Registry database to replace Win.ini, Autoexec.bat, and other text files
- Introduced Plug and Play and ActiveX
- Used FAT16 file system


Windows 98 and ME
---
- More Stable than Win 95
- Used FAT32 file system
- Win ME introduced System Restore
- Win 95, 98, and ME are collectively called "Win 9x"


Practice ✏️ 
---
- Read the article [TSA Carry-On Baggage Scanners Easy To Hack](https://www.darkreading.com/attacks-breaches/tsa-carry-on-baggage-scanners-easy-to-hack), explain why those scanners are easy to hack.


Windows NT 3.51 Server/Workstation
---
- No dependence on DOS kernel
- Domains and Domain Controllers
- NTFS File System to replace FAT16 and FAT32
- Much more secure and stable than Win9x
- Many companies still use Win NT Server Domain Controllers
- Win NT 4.0 was an upgrade


Windows 2000 Server/Professional
---
- Upgrade of Win NT
- Active Directory
  - Powerful database storing information about all objects in a network
    - Users, printers, servers, etc.
  - Based on Novell's Novell Directory Services
- Enumerating this system would include enumerating Active Directory


Windows XP Professional
---
- Much more secure, especially after Service Pack 2
  - Windows File Protection
  - Data Execution Prevention
  - Windows Firewall


Practice ✏️ 
---
- Read the article [Bill Gates: Trustworthy Computing](https://www.wired.com/2002/01/bill-gates-trustworthy-computing/), then make a summary.


Windows Server 2003
---
- Much more secure, especially after Service Pack 1
  - Network services are closed by default
  - Internet Explorer security set higher 


Windows Vista
---
- User Account Control
  - Users log in with low privileges for most tasks
- BitLocker Drive Encryption
- Address Space Layout Randomization (ASLR)


Practice ✏️ 
---
- Explore ASLR
  - download and run [process explorer](https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer)
    - view, show lower pane
    - view, lower pane view, dlls
    - view, select columns, dll tab, base address
  - select explorer.exe and find ntdll.dll, take a note of its base address
  - reboot to see base address change


Windows Server 2008
---
- User Account Control
- BitLocker Drive Encryption
- ASLR
- Network Access Protection
  - Granular levels of network access based on a clients level of compliance with policy
- Server Core
  - Small, stripped-down server, like Linux
- Hyper-V
  - Virtual Machines


Windows 7
---
- XP Mode
  - A virtual machine running Win XP
- User Account Control was refined and made easier to use


Windows 8
---
- Built-in antivirus
- SmartScreen protects against phishing and social engineering by using a URL and application reputation system
- Windows 8 secure boot using Unified Extensible Firmware Interface (UEFI) on ARM prevents rootkits


Windows Server 2012
---
- Authentication Silos to reduce the risk of pass-the-hash attacks
- DNSSEC which will someday make DNS resolutions more secure


Windows 10
---
- Brings back the Start button
- Forced automatic updates
- Device Guard allows only trusted apps to run
- Credential Guard uses virtualization to protect access tokens from theft
  - Reducing the risk of pass-the-hash attacks


Windows Server 2016
---
- Windows Containers
  - Like little virtual machines
  - Can isolate services from one another
- Windows Defender (malware protection) is now enabled by default
- telnet server is eliminated completely 
- Just Enough Administration (JEA) allows for more detailed access control settings on tasks


Windows Server 2019
---
- container services， shielded virtual machines
- storage spaces direct，storage migration services， storage replication  
- improved Windows Defender Advanced Threat Protection (ATP)


Network Basic Input Output System (NetBIOS)
---
- Programming interface
- Allows computer communication over a LAN
- NetBIOS listens on
  - UDP port 137 for NetBIOS Name service
  - UDP port 138 for NetBIOS Datagram service
  - TCP port 139 for NetBIOS Session service
- Used to share files and printers
  - requires an upper-level service called Server Message Block (SMB)
  - In Windows 2000 and later, SMB listens on TCP port 445 and doesn't need NetBIOS over TCP/IP unless support for older Windows versions is required



[NetBIOS names](https://en.wikipedia.org/wiki/NetBIOS)
---
- Computer names on Windows systems
- Limit of 16 characters
- Last character identifies type of service running
- Must be unique on a network


NetBIOS Null Sessions
---
- Null session
  - Unauthenticated connection to a Windows computer
  - Does not use logon and passwords values
- Around for over a decade
  - Still present on Windows XP
  - Disabled on Server 2003
  - Absent entirely in Vista and later versions
- A large vulnerability


Null Session Information
---
- Using these NULL connections allows you to gather the following information from the host:
- List of users and groups 
- List of machines 
- List of shares 
- Users and host SIDs (Security Identifiers)


[NetBIOS Enumeration Tools](https://en.wikipedia.org/wiki/NetBIOS_over_TCP/IP)
---
- [nbtstat command](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/nbtstat)
  - Powerful enumeration tool included with the Microsoft OS
  - Displays NetBIOS table
- net view command
  - Shows whether there are any shared resources on a network host
- [net use command](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/gg651155(v=ws.11))
  - Used to connect to a computer with shared folders or files


Practice ✏️ 
---
- On Windows VM, open a command prompt
- Practice command [nbtstat](https://www.computerhope.com/nbtstat.htm)
- Practice command [net view](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh875576(v=ws.11))

```cmd
:: 1. 
nbtstat /?
nbtstat -a Windows_VM_ip

:: 2.
net view /?
net view Windows_VM_ip

:: 3.
net use /?

:: assign drive letter E: to the shared directory on the \\server
net use v: \\server\shared 
```


Additional Enumeration Tools
---
- Windows tools included with Kali  
  - Smb4K, enum4linux
- DumpSec
  - Allows user to connect to a server and “dump”:
    - Permissions for shares, printers, and the registry
    - Users in column or table format
    - Policies, rights and services
- Hyena
  - Shows shares and user logon names for Windows servers and domain controllers
  - Displays graphical representation of:
    - Microsoft Terminal Services, Windows Network, Web Client Network
  - Finds user/group 
- [sparta](https://github.com/SECFORCE/sparta)
  - a python GUI application which simplifies network infrastructure penetration testing by aiding the penetration tester in the scanning and enumeration phase
- Nessus and OpenVAS
  - comprehensive tools


Practice ✏️ 
---
- On Kali vm, open a terminal windows
  ```bash
  # enum4linux - enumerate Windows computers in a network
  enum4linux -h
  enum4linux -U Windows_VM_ip
  ```


Enumerating the *nix Operating System
---
- Solaris and OpenSolaris
- HP-UX
- Mac OS X and OpenDarwin
- AIX
- BSD UNIX
  - FreeBSD, OpenBSD, NetBSD
- Linux, including several distributions


Simple Network Management Protocol (SNMP)
---
- Enables remote administration of servers, routers, switches, firewalls, and other devices
- Can be used on Windows and Linux


UNIX Enumeration
---
- Finger utility
  - a popular enumeration tool for security testers
  - Finds out who is logged in to a *nix system
  - Determines who was running a process
- Nessus and OpenVAS
  - more than a *nix enumeration tool


Practice ✏️ 
---
- on Kali VM
```bash
# 1. snmpwalk
snmpwalk -h
snmpwalk -v 2c -c public Kali_ip
# 2. finger
finger -h
finger
# 3. netdiscover - an ARP scanner
netdiscover
```


# References
* [What is new in Windows?](https://learn.microsoft.com/en-us/windows/whats-new/)
* [Where to Download Windows 10, 8.1, and 7 ISOs Legally?](https://www.howtogeek.com/186775/how-to-download-windows-7-8-and-8.1-installation-media-legally/)
* _old OSes_
  * [WinWorld](https://winworldpc.com/library/operating-systems)
  * [Old versions of Linux](https://soft.lafibre.info/)
  * [archiveos](https://archiveos.org/)