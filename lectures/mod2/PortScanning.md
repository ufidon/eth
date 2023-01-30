# Port Scanning

objectives
---
- Apply port scanning with various port-scanning tools
- Explain what ping sweeps are used for
- Automate security tasks with shell scripting


Introduction to Port Scanning
---
- Port Scanning
  - Examines a range of IP addresses
  - Finds out which services are running on a network
  - Identifies vulnerabilities
- Open services can be used on attacks
  - Identify a vulnerable port
  - Launch an exploit
- Scan all ports when testing
  - Not just well-known ports


Port scanners
---
- GUI port scanners
  - [Angry IP Scanner](https://angryip.org)
  - [Zenmap](https://nmap.org/zenmap)
- Command line port scanners
  - [nmap](https://nmap.org/)
  - [netdiscover](https://www.cyberpratibha.com/blog/netdiscover/)
    - gets the internal IP address and MAC address of live hosts in the network
        ```bash
        sudo netdiscover -i eth0 -r 10.0.2.0/24
        ```


Practice ✏️ 
---
- Download and install [Angry IP Scanner](https://angryip.org) on Windows VM
- Scan the NAT network on which the Windows VM attached


Port scanning report
---
- Open ports
  - allow access to applications and can be vulnerable to an attack
- Closed ports
  - don't allow entry or access to services
- Filtered ports
  - might indicate that a firewall is being used to allow specified traffic into or out of the network
- Best-guess assessment of which OS is running


Is Port Scanning Legal?
---
- The legal status of port scanning is unclear
  - If you have permission, it's legal
  - If you cause damage of $5,000 or more, it may be illegal


Types of [Port Scans](https://www.edureka.co/blog/nmap-tutorial/)
---
- SYN scan
- Connect scan
- NULL scan
- XMAS scan
- FIN scan
- ACK scan
- UDP scan
- ping scan


SYN Port Scan
---
- Applies TCP three-way handshake
  - Stage 1: attacker --SYN--> target
  - Stage 2: attacker <--SYN/ACK-- target
  - Stage 3: attacker --ACK-->target
- Completes the first two-way, not to complete the last way
- Three states of the target port
  - Closed: receives a RST/ACK packet at stage 2
  - Open: receives a SYN/ACK packet, replies with a RST/ACK packet to close the session
    - Stealthy because session handshakes are never completed
    - That keeps it out of some log files
  - Filtered: no responding SYN/ACK packet at stage 2


Connect scan
---
- Completes the three-way handshake
- Not stealthy--appears in log files


NULL scan
---
- All the packet flags are turned off
- Two results:
  - Closed ports reply with RST
  - Open or filtered ports give no response


XMAS scan and FIN scan
---
- FIN, PSH and URG flags are set
- Works like a NULL scan – a closed port responds with an RST packet
- Only FIN flag is set
- Closed port responds with an RST packet


Windows Machines
---
- NULL, XMAS and FIN scans don't work on Windows machines
- Win 2000 Pro and Win Server 2003 shows all ports closed
- Win XP Pro all ports open/filtered


ACK scan
---
- Used to get information about a firewall
- Stateful firewalls track connection and block unsolicited ACK packets
- Stateless firewalls just block incoming SYN packets, so you get a RST response


Ping scan
---
- Simplest method sends ICMP ECHO REQUEST to the destination
- TCP Ping sends SYN or ACK to any port 
  - default is port 80 for Nmap
- Any response shows the target is up


UDP scan
---
- Closed port responds with ICMP “Port Unreachable” message
- not receiving that message might imply the port is open


Using port scanners
---
- Nmap
- Nessus and OpenVAS (the GPL-licensed fork of Nessus)
  - A complete vulnerability scanner, more than a port scanner


[nmap](https://nmap.org/)
---
- One of the most popular command line port scanner
- GUI frontend
  - [zenmap](https://nmap.org/zenmap/)
- it is open-source
- Standard tool for security professionals


Practice ✏️ 
---
- Play with [zenmap](https://nmap.org/zenmap/)
  - Download and install zenmap on Windows VM
  - Run inetsim on Kali
  - Scan the NAT network with zenmap
- Play with [nmap](https://nmap.org/)
  - following this [tutorial](https://www.edureka.co/blog/nmap-tutorial)


Nessus
---
- Commercial, free version is called [OpenVAS(GreenBone)](https://github.com/greenbone)
  - Uses a client/server technology
  - Can conduct tests from different locations
  - Can use different OSs for client and network
- Finds services running on ports
  - Finds vulnerabilities associated with identified services


Conducting Ping Sweeps
---
- Ping sweeps
  - Identify which IP addresses belong to active hosts
  - Ping a range of IP addresses
- Problems
  - Computers that are shut down cannot respond
  - Networks may be configured to block ICMP Echo Requests
  - Firewalls may filter out ICMP traffic


[fping](https://fping.org/)
---
- Ping multiple IP addresses simultaneously
- Command-line tool
- Input: multiple IP addresses
  - To enter a range of addresses
    - -g option
  - Input file with addresses
    - -f option


[hping](www.hping.org)
---
- Used to bypass filtering devices
  - Allows users to fragment and manipulate IP packets
- A must-have for all security testers
- many command options
    ```bash
    hping3 --help
    ```

[Broadcast Addresses](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)
---
- pinging a broadcast address can create a lot of traffic
- Normally the broadcast address ends in 255
- But if your LAN is subnetted with a subnet mask like 255.255.255.192
- There are other broadcast addresses ending in 63, 127, and 191


Smurf Attack
---
- Pinging a broadcast address on an old network resulted in a lot of ping responses
  - So just put the victim's IP address in the "From" field
  - The victim is attacked by a flood of pings, none of them directly from you
    ```bash
    ping 10.0.2.255
    ```
- Modern routers don't forward broadcast packets
  - which prevents them from amplifying smurf attacks
- Windows XP and Ubuntu don't respond to broadcast PINGs


Crafting IP Packets
---
- Packet components
  - Source IP address
  - Destination IP address
  - Flags
- Crafting packets helps you obtain more information about a service
- Tools
  - fping
  - hping
  - [Scapy](https://scapy.net/)  
    - a powerful interactive packet manipulation program


Practice ✏️ 
---
- Play with [scapy](https://scapy.readthedocs.io/en/latest/index.html)


# References
*  [Common Vulnerabilities and Exposures](https://cve.mitre.org)
   *  [Cybersecurity & Infrastructure Security Agency](https://www.cisa.gov/)
* [The Official Nmap Project Guide to Network Discovery and Security Scanning](https://nmap.org/book/toc.html)
* [Greenbone Community Containers](https://greenbone.github.io/docs/latest/22.4/container/index.html)
  * ["Cannot connect to the Docker daemon ...." when running docker on Ubuntu/WSL](https://askubuntu.com/questions/1402272/cannot-connect-to-the-docker-daemon-when-running-docker-on-ubuntu-wsl)