# Network Protection Systems

Objectives
---
- Explain how routers are used to protect networks
- Describe and use firewall technology
- Describe and use intrusion detection systems
- Describe and use honeypots


Routers
---
- Routers are like intersections
  - they are hardware devices used on a network to send packets to different network segments
    - Operate at the network layer of the OSI model
- switches are like streets


Routing Protocols
---
- Routers tell one another what paths are available with Routing Protocols
  - Link-state routing protocol
    - Each router has complete information about every network link
    - Example: Open Shortest Path First (OSPF)
  - Distance-vector routing protocol
    - Routers only know which direction to send packets, and how far
    - Example: Routing Information Protocol (RIP)
  - Path-vector routing protocol
    - Used on the Internet Backbone
    - Example: Border Gateway Protocol (BGP)


IP hijacking via BGP
---
- Simply advertise routes to IP addresses assigned to other companies, but unused
- Like pirate radio


Cisco Routers
---
- widely used in the networking community
  - More than one million Cisco 2500 series routers are currently being used by companies around the world
- Vulnerabilities exist in Cisco as they do in any operating system


[Ciscogate: Michael Lynn](https://en.wikipedia.org/wiki/Ciscogate)
---
- presented a major Cisco security vulnerability at the Black Hat security conference in 2005
- lost his job, was sued, conference materials were confiscated, etc.


Cisco Router Components
---
- Internetwork Operating System (IOS)
  - controlled from the command line
- Random access memory (RAM)
  - Holds the router’s running configuration, routing tables, and buffers
  - If you turn off the router, the contents stored in RAM are wiped out
- Nonvolatile RAM (NVRAM)
  - Holds the router’s configuration file, 
  - but the information is not lost if the router is turned off
- Flash memory
  - Holds the IOS the router is using
  - Is rewritable memory, so you can upgrade the IOS
- Read-only memory (ROM)
  - Contains a minimal version of the IOS used to boot the router if flash memory gets corrupted
- Interfaces
  - Hardware connectivity points
  - Example: an Ethernet port is an interface that connects to a LAN


Standard IP Access Lists
---
- Can restrict IP traffic entering or leaving a router’s interface based on source IP address
  - To restrict traffic from Network 3 from entering Network 1, access list looks like:
    ```bash
    # 1. Network 1: 10.0.0.0; Network 3: 173.110.0.0
    access-list 1 deny 173.110.0.0 0.0.255.255
    access-list permit any
    ```


Extended IP Access Lists
---
- Restricts IP traffic entering or leaving based on:
  - Source IP address
  - Destination IP address
  - Protocol type
  - Application port number


Firewalls
---
- hardware devices or software installed on a system and have two purposes
  - Controlling access to all traffic that enters an internal network
  - Controlling all traffic that leaves an internal network


Hardware Firewalls
---
- Advantage of hardware firewalls
  - Faster than software firewalls (more throughput)
- Disadvantages of hardware firewalls
  - limited by the firewall’s hardware
    - Number of interfaces, etc.
  - Usually filter incoming traffic only


Software Firewalls
---
- Advantages of software firewalls
  - Customizable: can interact with the user to provide more protection
  - You can easily add NICs to the server running the firewall software
- Disadvantages of software firewalls
  - have complex configurations
  - rely on the OS on which they are running


Firewall Technologies
---
- Network Address Translation (NAT)
- Access lists
- Packet filtering
- Stateful packet inspection (SPI)
- Application layer inspection


Network Address Translation (NAT)
---
- Internal private IP addresses are mapped to public external IP addresses
  - Hides the internal infrastructure
- Port Address Translation (PAT)
  - This allows thousands of internal IP addresses to be mapped to one external IP address
  - Each connection from the private network is mapped to a different public port


Access Lists
---
- A series of rules to control traffic
- Criteria
  - Source IP address
  - Destination IP address
  - Ports or services
  - Protocol (Usually UDP or TCP)


Packet Filtering
---
- Packet filters screen traffic based on information in the header, such as
  - Protocol type
  - IP address
  - TCP/UDP Port
  - More possibilities


Stateful Packet Inspection (SPI)
---
- Stateful packet filters examine the current state of the network
  - If you have sent a request to a server, packets from that server may be allowed in
  - Packets from the same server might be blocked if no request was sent first
- Stateful packet filters recognize types of anomalies that most routers ignore
- Stateless packet filters handle each packet on an individual basis
  - This makes them less effective against some attacks, such as the "reverse shell"


State Table
---
- Stateful firewalls maintain a state table showing the current connections


ACK Port scan
---
- Used to get information about a firewall
- Stateful firewalls track connection and block unsolicited ACK packets
- Stateless firewalls only block incoming SYN packets, so you get a RST response


Application Layer Inspection 
---
- Application-layer firewall can detect Telnet or SSH traffic masquerading as HTTP traffic on port 80


Implementing a Firewall
---
- Using only one firewall between a company’s internal network and the Internet is dangerous
  - It leaves the company open to attack if a hacker compromises the firewall
- Use a demilitarized zone instead


Demilitarized Zone (DMZ)
---
- DMZ is a small network containing resources available to Internet users
  - Helps maintain security on the company’s internal network
- Sits between the Internet and the internal network
- It is sometimes referred to as a “perimeter network”


The Cisco ASA (Adaptive Security Appliance) Firewall
---
- Replaced the Cisco PIX firewall
  - One of the most popular firewalls on the market
- Configuration
  - Working with a PIX firewall is similar to working with any other Cisco router
  - Login prompt
    ```bash
    If you are not authorized to be in this XYZ Hawaii network device,
    log out immediately!
    Username: admin
    Password: ********
    ```
    - This banner serves a legal purpose
    - A banner that says “welcome” may prevent prosecution of hackers who enter
- Features
  - Can group objects, such as terminals and serves, and filter traffic to and from them
  - High throughput, and many more features


Access List
---
```
ciscoasa( config)# show run access- list 
access- list PERMITTED_ TRAFFIC remark VPN- CONC1 TO TERMINAL CLOSET1B 
access- list PERMITTED_ TRAFFIC extended permit ip host 10.13.61.98 host 10.13.61.18 
access- list NONE extended deny ip any any log access- list CAP- ACL extended permit ip any any
```


Using Configuration and Risk Analysis Tools for Firewalls and Routers
---
- Center for Internet Security
  - Cisecurity.org
- Configuration benchmarks and risk assessment tools
- Free "Router Audit Tool" and many other tools


Red Seal
---
- Commercial tool to assess network security and compliance
- Diagram shows traffic flow between devices


Intrusion Detection Systems (IDSs)
---
- Monitor network devices so that security administrators can identify attacks in progress and stop them
- An IDS looks at the traffic and compares it with known exploits
  - Similar to virus software using a signature file to identify viruses
- Types
  - Network-based IDSs
  - Host-based IDSs


Network-Based and Host-Based IDSs
---
- Network-based IDSs
  - Monitor activity on network segments
  - sniff traffic and alert a security administrator when something suspicious occurs
- Host-based IDSs
  - installed on the server you’re attempting to protect, like antivirus software
  - Used to protect a critical network server or database server


Passive and Active IDSs
---
- categorized by how they react when they detect suspicious behavior
- Passive systems
  - Send out an alert and log the activity
  - Don't try to stop it
- Active systems
  - Log events and send out alerts
  - Can also interoperate with routers and firewalls to block the activity automatically


Explore 🔍
---
- [Snort: open-source network-based IDS](https://www.snort.org/)


Web Filtering
---
- Common attack: trick user into downloading and running malware
- Firewall won't stop that, because the request originates inside the network
- Web filtering blocks
  - Known malicious sites
  - Sites in risky categories like "hacking"
  - Known malware


Drive-By Downloads
---
- Malware that attacks browsers
- Even when they don't click on anything
- Often in iframes or malicious ads


Security Operations Center (SOC)
---
- Permanent team performing
  - Incident response
  - Damage remediation
- Find Indicators of Compromise
- Use Security Information and Event Management (SIEM) systems
  - Such as HP's ArcSight or AlienVault


Honeypots
---
- Computer placed on the perimeter of a network
- Contains information intended to lure and then trap hackers
- Computer is configured to have vulnerabilities
- Goal
  - Keep hackers connected long enough so they can be traced back


How Honeypots Work
---
- A honeypot appears to have important data or sensitive information stored on it
  - Could store fake financial data that tempts hackers to attempt browsing through the data
- Hackers will spend time attacking the honeypot
  - And stop looking for real vulnerabilities in the company’s network
- Honeypots also enable security professionals to collect data on attackers
- Virtual honeypots
  - Honeypots created using software solutions instead of hardware devices
  - Example: Honeyd


Project Honey Pot
---
- Web masters install software on their websites
- When spammers harvest email addresses from sites, HoneyNet's servers record the IP of the harvester
  - Can help prosecute the spammers and block the spam
- Uses a Capture Server and one or more Capture Clients
  - The clients run in virtual machines
  - Clients connect to suspect Web servers
  - If the client detects an infection, it alerts the Capture Server and restores itself to a clean state
  - The server gathers data about malicious websites


Explore 🔍
---
- Explore [honeypots](https://github.com/paralax/awesome-honeypots)


Web Application Firewalls
---
- Constantly-updated list of attack signatures
- Protects a vulnerable application
- Normal firewall must allow Web traffic
  - Doesn't stop attacks like SQL Injection
- Reverse Proxies
  - protect Web servers by intercepting requests and caching content
  - Make a Website faster and much more secure



# References
- [GNS3](https://www.gns3.com/)