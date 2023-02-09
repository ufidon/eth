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
  ```


Enumerating Microsoft Operating Systems
---
- Study OS history
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
  - download and run process explorer
    - view, show lower pane
    - view, lower pane view, dlls
    - view, select columns, dll tab, base address
  - select explorer.exe and find ntdll.dll, take a note of its base address
  - reboot to see base address change


# References
* _old OSes_
  * [WinWorld](https://winworldpc.com/library/operating-systems)
  * [Old versions of Linux](https://soft.lafibre.info/)
  * [archiveos](https://archiveos.org/)