# Security Foundations

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


ATM Machine Worms
---
- Cyberattacks against ATM machines
  - [Slammer](https://www.theregister.com/2003/01/27/atms_isps_hit_by_slammer/) and [Nachi](https://www.theregister.com/2003/11/25/nachi_worm_infected_diebold_atms/) worms
  - Nachi was written to clean up damage caused by the Blaster worm, but it got out of control
  - Diebold was criticized for using Windows for ATM machines, which they also use on voting machines
- [Trend Micro](https://www.atmmarketplace.com/news/trend-micro-intros-virus-protection-for-atms/) produces antivirus for ATM machines


Antivirus Software
---
- Detects and removes viruses
- Detection based on virus signatures
- Must update signature database periodically
- Use automatic update feature
- For example,
  - Windows security
  - Norton

