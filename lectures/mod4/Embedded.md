# Embedded Operating Systems: The Hidden Threat

Objectives
---
- Explain what embedded operating systems are and where they’re used
- Describe Windows IoT (Internet of Things) and other embedded operating systems
- Identify vulnerabilities of embedded operating systems and best practices for protecting them


Introduction to Embedded Operating Systems
---
- Embedded system 
  - Any computer system that isn’t a general-purpose PC or server
    - GPSs and ATMs
    - Electronic consumer and industrial items
  - Are in all networks
  - Perform essential functions
    - Route network traffic; block suspicious packets
- Embedded operating system (OS) 
  - Small program developed for embedded systems
    - Stripped-down version of OS commonly used on general-purpose computers
    - Designed to be small and efficient
  - Real-time operating system (RTOS)
    - Typically used in devices such as programmable thermostats, appliance controls, and spacecraft
- Corporate buildings 
  - May have many embedded systems
    - Firewalls, switches, routers, Web-filtering appliances, network attached storage devices, etc.


Windows and Other Embedded Operating Systems
---
- Recycling common code and reusing technologies
  - Sound software engineering practices
  - Also introduce common points of failure
    - Viruses, worms, Trojans, and other attack vectors
- Windows and Linux vulnerabilities
  - Might also exist in embedded version
- Windows CE 
  - Some source code is available to the public
    - Code sharing is not common
    - Microsoft believed it would increase adoptions


Practice✏️ 
---
- Get an overview of [Windows 10 IoT](https://learn.microsoft.com/en-us/windows/iot-core/windows-iot)
  - Raspberry Pi
  - MinnowBoard
  - NXP devices
  - DragonBoard
  - Qualcomm devices
  - Intel devices


Other Proprietary Embedded OSs
---
- [VxWorks](https://www.windriver.com/products/vxworks) 
  - Widely used embedded OS 
    - Developed by Wind River Systems
  - Used in spacecraft
  - Designed to run efficiently on minimal hardware
- [Green Hill Software embedded OSs](https://www.ghs.com/)
  - F-35 Joint Strike Fighter
  - Multiple independent levels of security/safety (MILS)
    - OS certified to run multiple levels of classification
  - Embedded OS code 
    - Used in printers, routers, switches, etc.
- [QNX Software Systems QNX](https://blackberry.qnx.com/en)
  - Commercial RTOS 
    - Used in Cisco’s ultra-high-availability routers and Logitech universal remotes
- [Real-Time Executive for Multiprocessor Systems (RTEMS)](https://www.rtems.org/)
  - Open-source embedded OS 
  - Used in space systems 
    - Supports processors designed to operate in space
- Using multiple embedded OSs
  - Increases attack surface


Microkernel OS vs. Monolithic kernel OS
---

![Microkernel OS vs. Monolithic kernel OS](https://upload.wikimedia.org/wikipedia/commons/6/67/OS-structure.svg)

- [Microkernel OS](https://en.wikipedia.org/wiki/Microkernel)
- [Monolithic kernel OS](https://en.wikipedia.org/wiki/Monolithic_kernel)


*Nix Embedded OSs
---
- Embedded Linux 
  - Monolithic OS 
    - Used in industrial, medical, and consumer items
  - Can be tailored for devices with limited memory or hard drive capacity
  - Supports widest variety of hardware 
  - Allows adding features 
    - Dynamic kernel modules
- Real Time Linux (RTLinux) 
  - OS microkernel extension
  - Turns “regular” Linux into an RTOS 
    - Suitable for embedded applications requiring a guaranteed response in a predictable manner
- Linux [OpenWrt](https://openwrt.org/) / [dd-wrt](https://dd-wrt.com/)
  - Embedded Linux OS
  - Used in Linksys WRT54G wireless router 
    - Found in home offices and small businesses


Vulnerabilities of Embedded OSs
---
- Practice✏️ 
  - [Nasty New Worm Targets Home Routers, Cable Modems](https://www.pcworld.com/article/528111/nasty_worm_targets_home_networks.html)
    - [Psyb0t or Network Bluepill](https://en.wikipedia.org/wiki/Psyb0t)
  - Find Windows mobile vulnerabilities on [securityfocus](https://bugtraq.securityfocus.com/)
- Impact of attacks have become more serious
  - Embedded OSs are no exception
- Easiest way to profit from hacking 
  - Attack devices that store and dispense cash (e.g., ATMs)
    - Involves use of card skimmers or stealing the machines


Embedded OSs Are Everywhere
---
- Embedded systems with Y2K software flaw
  - Billions located everywhere
- Today
  - Many more embedded devices
    - Under attack from hackers and terrorists
    - Attackers want to further financial or political causes
  - Addressing security early in design phase is essential


Embedded OSs Are Networked
---
- Advantages of connecting to a network
  - Efficiency and economy
  - Ability to manage and share services
    - Keeps human resources and expertise minimal
    - Reduces costs
- Any device added to a network infrastructure
  - Increases potential for security problems


Embedded OSs Are Difficult to Patch
---
- General-purpose desktop OSs
  - Simple to patch
    - Wait for vulnerability to be identified
    - Download and install patch
- Embedded OSs
  - Must continue operating regardless of threat
  - Lack familiar interfaces
  - Buffer overflow attacks might be successful 
    - Few updates released to correct vulnerabilities
    - Manufacturers typically prefer system upgrades
- Open-source software 
  - Cost of developing and patching shared by open-source community
- Patching Linux kernel 
  - Estimated at tens of billions of dollars
    - Total cost of developing and patching it, in programmer hours
  - Offers flexibility and support 
    - Large; has many code portions
- Fixing a vulnerability 
  - Weigh cost of fixing against importance of information the embedded system controls


Practice✏️ 
---
- Read the articles and discuss the challenges 
  - [Defcon: Excuse me while I turn off your pacemaker](https://venturebeat.com/security/defcon-excuse-me-while-i-turn-off-your-pacemaker/)
  - [Reverse Engineering A D-Link Backdoor](https://hackaday.com/2013/10/14/reverse-engineering-a-d-link-backdoor/)


Embedded OSs Are in Networking Devices
---
- Networking devices
  - Usually have software and hardware designed to transmit information across networks
- General-purpose computers 
  - Originally performed routing and switching
    - High-speed networks now use specialized hardware and embedded OSs
- Attacks that compromise a router
  - Can give complete access to network resources
    - Attackers follow usual methods of footprinting, scanning, and enumerating the target
- Authentication bypass vulnerability
  - Common vulnerability of routers
  - Specially crafted URL bypasses normal authentication mechanism
- Router Hacking Contest
- After bypassing authentication
  - Attackers can launch other network attacks 
    - Use access gained through compromised router


Embedded OSs Are in Network Peripherals
---
- Common peripheral devices: 
  - Printers, scanners, copiers, and fax devices
- Multifunction devices (MFDs) 
  - Perform more than one function
    - Rarely scanned for vulnerabilities or configured for security
  - Have embedded OSs with sensitive information
    - Information susceptible to theft and modification
    - Attackers may use malware or insert malicious links 
    - Social-engineering techniques may be used to gain access


[Hacking into a printer](https://www.cybervie.com/blog/how-to-hack-printers/)
---
- [We hijacked 28,000 unsecured printers to raise awareness of printer security issues](https://cybernews.com/security/we-hacked-28000-unsecured-printers-to-raise-awareness-of-printer-security-issues/)
- Taking control of a printer gives you
  - Access to stored print jobs
  - You can use the printer as a gateway into a secure LAN
  - You could also alter the messages the printer produces to send malicious links to desktops 


Supervisory Control and Data Acquisition Systems
---
- Used for equipment monitoring in large industries (e.g., public works and utilities)
  - Anywhere automation is critical
- May have many embedded systems as components
  - Vulnerable through data fed in and out or embedded OSs
- Systems controlling critical infrastructure
  - Usually separated from Internet by “air gap”


Practice✏️
---
- Read the article [How 30 Lines of Code Blew Up a 27-Ton Generator](https://www.apintlcorp.com/articulos/articulo-how-30-lines-of-code-blew-up-27-ton-generator.html)
  - [Aurora Generator Test](https://en.wikipedia.org/wiki/Aurora_Generator_Test)
  - [Throwback Attack: Lessons from the Aurora vulnerability](https://www.controleng.com/articles/throwback-attack-lessons-from-the-aurora-vulnerability/)
- [Stuxnet](https://en.wikipedia.org/wiki/Stuxnet)
  - Infected Siemens Programmable Logic Controller cards in nuclear power plants
  - Suspected to be a targeted military attack against one Iranian nuclear plant
  - Very sophisticated attack, using four 0-day exploits
  - Infected thousands of Iranian systems


Supervisory control and data acquisition (SCADA) systems
---
- [One Flaw too Many: Vulnerabilities in SCADA Systems](https://www.trendmicro.com/vinfo/us/security/news/vulnerabilities-and-exploits/one-flaw-too-many-vulnerabilities-in-scada-systems)
  - [0-Day SCADA Exploits Released, Publicly Exposed Servers At Risk](https://www.darkreading.com/risk/0-day-scada-exploits-released-publicly-exposed-servers-at-risk)
  - [Hackers earn $400K for zero-day ICS exploits demoed at Pwn2Own](https://www.bleepingcomputer.com/news/security/hackers-earn-400k-for-zero-day-ics-exploits-demoed-at-pwn2own/)



[Dell Remote Access Controller (DRAC)](https://en.wikipedia.org/wiki/Dell_DRAC)
---
- [iDRACula Vulnerability Impacts Millions of Legacy Dell EMC Servers](https://www.servethehome.com/idracula-vulnerability-impacts-millions-of-legacy-dell-emc-servers/2/)
  - [Find vulnerable DRAC systems](https://www.shodan.io/search?query=%22remote+access+controller%22+)
  - [How to access the out-of-band management of a Dell server](https://www.servers.com/support/knowledge/dedicated-servers/how-to-access-the-out-of-band-management-interface-of-a-dell-server-called-idrac)



Cell Phones, Smartphones, and PDAs
---
- Conversations over traditional phones 
  - Considered protected
    - Tapping used to require a lot of time, expensive equipment, and a warrant
  - Many have the same security expectations of cell phones, smartphones, and PDAs
    - PDAs have additional vulnerabilities associated with PDA applications and services
    - Smartphones combine functions; have even more vulnerabilities
- Cell phone vulnerabilities 
  - Attackers listening to your phone calls
  - Using the phone as a microphone
  - “Cloning” the phone to make long-distance calls
  - Get useful information for computer or network access
    - Steal trade or national security secrets
    - Java-based phone viruses


Practice✏️
---
- Read the articles
  - [Cell phone rootkit](https://en.wikipedia.org/wiki/Rootkit)
  - [Powerful backdoor/rootkit found preinstalled on 3 million Android phones](https://arstechnica.com/information-technology/2016/11/powerful-backdoorrootkit-found-preinstalled-on-3-million-android-phones/)



Rootkits
---
- Modify OS parts or install themselves as kernel modules, drivers, libraries, and applications
  - Exist for Windows and *nix OSs
- Rootkit-detection tools and antivirus software
  - Detect rootkits and prevent installation
    - More difficult if OS has already been compromised
    - Rootkits can monitor OS for anti-rootkit tools and neutralize them
- Biggest threat
  - Infects firmware
- Trusted Platform Module (TPM)
  - Defense against low-level rootkits
    - Ensures OS hasn't been subverted or corrupted
    - ISO standard ISO/IEC 11889
- Firmware rootkits 
  - Hard to detect 
    - Code for firmware often isn't checked for corruption
- Insider hacking 
  - Harder to detect
    - Malicious code hidden in flash memory
- Systems compromised before purchased
  - May function like normal
  - Must flash (rewrite) BIOS, wipe hard drive, and reload OS
    - Expensive and time consuming
- LoJack for Laptops
  - Laptop theft-recovery service
  - Some design-level vulnerabilities rootkits can exploit
    - Infection residing in computer’s BIOS
    - Call-home mechanism


Countermeasures against rootkits
---
- [Secure the Windows boot process](https://learn.microsoft.com/en-us/windows/security/information-protection/secure-the-windows-10-boot-process)
- [Understanding UEFI Secure Boot Chain](https://edk2-docs.gitbook.io/understanding-the-uefi-secure-boot-chain/)


Best Practices for Protecting Embedded OSs
---
- Identify all embedded systems in an organization
  - Prioritize systems or functions that depend on them
- Follow least privileges principle for access
  - Restrict network access and reduce attack surface
- Configure embedded systems securely
  - Use cryptographic measures
    - Use data transport encryption
- Install patches and updates
  - Upgrade or replace systems that can’t be fixed or pose unacceptable risks


# References
