# Network and Computer Attacks

Objectives
---
- Describe the types of network attacks
- Identify physical security attacks and vulnerabilities
- Describe the different types of malicious software
- Describe methods of protecting against malware attacks


Malicious Software (Malware)
---
- Network attacks prevent a business from operating
- Malicious software (Malware) includes
  - Virus
    - Ransomware locks a target system until a ransom is paid
  - Worms
  - Trojan horses
- Goals
  - Destroy data
  - Corrupt data
  - Shutdown a network or system


[Viruses](https://en.wikipedia.org/wiki/Computer_virus)
---
- Virus attaches itself to an host executable file
- Can replicate itself when the host program executes
  - Needs a host program to replicate
- No foolproof method of preventing them
- [Top 10 most destructive computer viruses](https://www.advancedcpc.com/top-10-most-destructive-computer-viruses-of-all-time/)


Macro Viruses
---
- Virus encoded as a macro
- Macro
  - Lists of commands
  - Can be used in destructive ways
- Example: [Melissa](https://www.f-secure.com/v-descs/melissa.shtml)
  - Appeared in 1999
  - Secretly integrates itself into Outlook or Word files
  - It is very simple, check its [source code](https://www.cs.miami.edu/home/burt/learning/Csc521.061/notes/melissa.txt)


Writing Viruses
---
- Even nonprogrammers can create macro viruses
  - Instructions posted on [Web sites](https://www.blackmoreops.com/2018/11/06/124-legal-hacking-websites-to-practice-and-learn/)
  - [Virus creation kits](https://www.informit.com/articles/article.aspx?p=366890&seqNum=7) available for download
    - [Angler Exploit Kit](https://www.malwarebytes.com/blog/threats/angler)
    - [AutoSploit](https://github.com/NullArray/AutoSploit)
- Security professionals can learn from thinking like attackers
  - But don’t create and release a virus!  
  - People get long prison terms for that


Worms
---
- Replicates and propagates without a host, often through email
- Infamous examples
  - [Code Red](https://en.wikipedia.org/wiki/Code_Red_(computer_worm))
  - [Nimda](https://en.wikipedia.org/wiki/Nimda)
- Can infect every computer in the world in a short time
  - At least in theory
- [Top 10 worms](https://www.secpoint.com/top-10-worms.html)


ATM Machine Worms
---
- Cyberattacks against ATM machines
  - [Slammer](https://www.theregister.com/2003/01/27/atms_isps_hit_by_slammer/) and [Nachi](https://www.theregister.com/2003/11/25/nachi_worm_infected_diebold_atms/) worms
  - Nachi was written to clean up damage caused by the Blaster worm, but it got out of control
  - Diebold was criticized for using Windows for ATM machines, which they also use on voting machines
- [Trend Micro](https://www.atmmarketplace.com/news/trend-micro-intros-virus-protection-for-atms/) produces antivirus for ATM machines


Trojan Horse Programs
---
- Insidious attack against networks
- Disguise themselves as useful programs
  - Hide malicious content in program
    - Backdoors
    - Rootkits
  - Allow attackers remote access


Firewalls
---
- Identify traffic on uncommon ports
- Can block this type of attack, if your firewall filters outgoing traffic
  - Windows Firewall in XP SP2, Vista, and Win 7 does not filter outgoing traffic by default
- Trojan programs can use known ports to get through firewalls
  - HTTP (TCP 80) or DNS (UDP 53)
- [Trojan ports](https://docs.trendmicro.com/all/ent/officescan/v10.6/en-us/osce_10.6_sp1_olh/gls_trojan_port.html)


Spyware
---
- Sends information from the infected computer to the attacker
  - Confidential financial data
  - Passwords
  - PINs
  - Any other stored data
- Can register each keystroke entered (keylogger)
- [List of spyware programs](https://en.wikipedia.org/wiki/List_of_spyware_programs)


Adware
---
- Similar to spyware
  - Can be installed without the user being aware
- Sometimes displays a banner
- Main goal
  - Determine user’s online purchasing habits
  - Tailored advertisement
- Main problem
  - Slows down computers


Protecting Against Malware Attacks
---
- Difficult task
  - New viruses, worms, Trojan programs appear daily
- SpyBot and Ad-Aware
  - Help protect against spyware and adware
  - Windows Defender is excellent too
- Antivirus programs offer a lot of protection
  - Update virus signature database automatically
- Firewalls
  - Hardware (enterprise solution)
  - Software (personal solution)
  - Can be combined
- Intrusion Detection System (IDS)
  - Monitors your network 24/7
- Educate your users about these types of attacks
  - Includes all employees and management
  - E-mail monthly security updates


Antivirus Software
---
- Detects and removes viruses
- Detection based on virus signatures
- Must update signature database periodically
  - Use automatic update feature
- For example,
  - Windows security
  - Norton


FUD
---
- Fear, Uncertainty and Doubt
  - Avoid scaring users into complying with security measures
  - Sometimes used by unethical security testers
  - Against the [Open Source Security Testing Methodology Manual(OSSTMM)](https://www.futurelearn.com/info/courses/ethical-hacking-an-introduction/0/steps/71522) ’s Rules of Engagement
- Promote awareness rather than instilling fear
  - Users should be aware of potential threats
  - Build on users’ knowledge


Intruder Attacks on Networks and Computers
---
- Attack
  - Any attempt by an unauthorized person to access or use network resources
- Network security
  - Security of computers and other devices in a network
- Computer security
  - Securing a standalone computer--not part of a network infrastructure
- Computer crime
  - Fastest growing type of crime worldwide


Denial-of-Service Attacks
---
- Denial-of-Service (DoS) attack
  - Prevents legitimate users from accessing network resources
  - Some forms do not involve computers, like feeding a paper loop through a fax machine
- DoS attacks do not attempt to access information
  - Cripple the network
  - Make it vulnerable to other type of attacks
- Testing for DoS Vulnerabilities
  - Performing an attack yourself is not wise
  - You only need to prove that an attack could be carried out


Distributed Denial-of-Service Attacks
---
- Attack on a host from multiple servers or workstations
- Network could be flooded with billions of requests
  - Loss of bandwidth
  - Degradation or loss of speed
- Often participants are not aware they are part of the attack
  - They are remote-controlled "zombies"

Buffer Overflow Attacks
---
- Vulnerability in poorly written code
  - Code does not check predefined size of input field
- Goal
  - Fill overflow buffer with executable code
  - OS executes this code
  - Can elevate attacker’s permission to Administrator or even Kernel
- Programmers need special training to write secure code


Ping of Death Attacks
---
- Type of DoS attack by exploiting buffer overflow
- Not as common as during the late 1990s
- How it works
  - Attacker creates a large ICMP packet
  - More than 65,535 bytes
  - Large packet is fragmented at source network
  - Destination network reassembles large packet
  - Destination point cannot handle oversize packet and crashes
  - Evading network intrusion detection with [flagrouter](https://www.kali.org/tools/fragrouter/)
- Modern systems are protected from this 


Session Hijacking
---
- Enables attacker to interrupt a TCP session
- Taking over another user's session


Addressing Physical Security
---
- Protecting a network also requires physical security
  - Lock up your servers
    - Physical access means they can hack in
    - Consider [Ophcrack](https://ophcrack.sourceforge.io/) – booting to a CD-based OS will bypass almost any security
  - Lockpicking
    - Average person can pick deadbolt locks in less than five minutes
      - After 30 min. of practice
    - Experienced hackers can pick deadbolt locks in under 30 seconds
    - Bump keys are even easier 
  - Card Reader Locks
    - Keep a log of who enters and leaves the room
    - Security cards can be used instead of keys for better security
- Inside attacks are more likely than attacks from outside the company
- Insider Threats


Keyloggers
---
- Used to capture keystrokes on a computer
- Software
  - Behaves like Trojan programs
- Hardware
  - Easy to install
  - Goes between the keyboard and the CPU
  - KeyKatcher and KeyGhost
- Protection
  - Software-based
    - Antivirus
- Hardware-based
  - Random visual tests
  - Look for added hardware
  - Superglue keyboard connectors
