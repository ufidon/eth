# Networking Foundations

**Objectives**

- Describe the TCP/IP protocol stack
- Explain the basic concepts of IP addressing
- Exploit the binary, octal, and hexadecimal numbering system
- Construct client/server (C/S) systems

**Overview of TCP/IP**
---
- Network protocol
  - Common language used by computers for networking
  - Open Systems Interconnection model [(OSI model)](https://en.wikipedia.org/wiki/OSI_model)
    - Mainly used in theoretical description
  - Transmission Control Protocol/Internet Protocol [(TCP/IP)](https://en.wikipedia.org/wiki/Internet_protocol_suite)
    - Most widely used protocol in application
- TCP/IP stack contains four different layers
  - [Application layer](https://en.wikipedia.org/wiki/Application_layer): 
    - network services and clients
    - BGP, DNS, HTTP, HTTPS, FTP, SMTP, POP, SSH
  - [Transport layer](https://en.wikipedia.org/wiki/Transport_layer): 
    - transmit/receive data packets by sockets (IP:port number) 
    - TCP, UDP, SCTP
  - [Internet layer](https://en.wikipedia.org/wiki/Internet_layer): 
    - address hosts and route packets
    - IP, ICMP
  - [Link layer](https://en.wikipedia.org/wiki/Link_layer): 
    - represents physical network pathway and network interface cards
    - PPP, MAC


**The Application Layer**
---
- Front end to the lower-layer (transport layer) protocols
- What you can see and touch – closest to the user at the keyboard
- HTTP, FTP, SMTP, SNMP, SSH, IRC and TELNET all operate in the Application Layer

| Protocol | Application                        |
| -------- | ---------------------------------- |
| HTTPS    | Hypertext Transfer Protocol Secure |
| FTP      | File Transfer Protocol             |
| SMTP     | Simple Mail Transfer Protocol      |
| SNMP     | Simple Network Management Protocol |
| SSH      | Secure Shell                       |
| Telnet   | insecure shell                     |
| IRC      | Internet Relay Chat                |


**The Transport Layer**
---
- Encapsulates data into segments
- Segments can use TCP or UDP to reach a destination host
- TCP is a connection-oriented protocol
  - Setup by three-way handshake
    - Computer A sends a SYN packet
    - Computer B replies with a SYN-ACK packet
    - Computer A replies with an ACK packet


**TCP Header Format**
---
* [TCP segment header](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)
- Critical components:
  - TCP flags
  - Initial Sequence Number (ISN)
  - Source and destination port
- Abused by hackers finding vulnerabilities


**TCP Flags**
---
- Each flag occupies one bit
  - Can be set to 0 (off) or 1 (on)
- Six flags
  - SYN: synchronize flag
  - ACK: acknowledge flag
  - PSH: push flag
  - URG: urgent flag
  - RST: reset flag
  - FIN: finish flag


**Initial Sequence Number (ISN)**
---
- 32-bit number
- Tracks packets received
- Enables reassembly of large packets
- Sent on steps 1 and 2 of the TCP three-way handshake
  - By guessing ISN values, a hacker can hijack a TCP session, gaining access to a server without logging in


**TCP Ports**
---
- Port
  - Logical, not physical, component of a TCP connection
  - Identifies the service that is running
  - Example: HTTP uses port 80
- A 16-bit number – 65,536 ports
- Each TCP packet has a source and destination port


**Blocking Ports**
---
- Helps you stop or disable services that are not needed
  - Open ports are an invitation for an attack
- You can’t block all the ports
  - That would stop all networking
  - At a minimum, ports 25 and 80 are usually open on a server, so it can send out Email and Web pages
- Only the first 1023 ports are considered well-known


**List of [well-known ports](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)**
---
- Available at  the Internet Assigned Numbers Authority (IANA) Web site (www.iana.org)
- Ports 20 and 21
  - File Transfer Protocol (FTP)
  - Use for sharing files over the Internet
  - Requires a logon name and password
  - More secure than Trivial File Transfer Protocol (TFTP)
- Port 25
  - Simple Mail Transfer Protocol (SMTP)
  - E-mail servers listen on this port
- Port 53
  - Domain Name Service (DNS)
  - Helps users connect to Web sites using URLs instead of IP addresses
- Port 69
  - Trivial File Transfer Protocol
  - Used for transferring router configurations
  - Had the ["Sorcer's Apprentice Syndrome"](https://en.wikipedia.org/wiki/Sorcerer%27s_Apprentice_Syndrome) Denial-of-Service vulnerability
- Port 80
  - Hypertext Transfer Protocol (HTTP)
  - Used when connecting to a Web server
- Port 110
  - Post Office Protocol 3 (POP3)
  - Used for retrieving e-mail
- Port 119
  - Network News Transfer Protocol
  - For use with newsgroups
- Port 135
  - Remote Procedure Call (RPC)
  - Critical for the operation of Microsoft Exchange Server and Active Directory
- Port 139
  - NetBIOS
  - Used by Microsoft’s NetBIOS Session Service
  - File and printer sharing
- Port 143
  - Internet Message Access Protocol 4 (IMAP4)
  - Used for retrieving e-mail
  - More features than POP3

**Exercises**

On Kali Linux, 
* Play [INetSim](https://www.inetsim.org/documentation.html)
  ```bash
  # 1. start inetsim in one command tab
  sudo inetsim

  # 2. in another command tab
  # 2.1 show simulation services provided by inetsim
  netstat -a | grep -i lis | grep -i tcp # show port name

  # 2.2 show port number
  netstat -a -n | grep -i lis | grep -i tcp

  # 2.3 try webservice
  # type http://localhost in firefox address bar
  # type https://localhost in firefox address bar

  # 2.4 try ftp service
  ftp localhost
  ```
* Use Wireshark to sniff
  * TCP handshake: SYN, SYN/ACK, ACK
  * TCP ports, status and flags
  ```bash
  # 1. run Wireshark and start capturing packets on eth0
  # refresh the webpage in firefox
  # stop Wireshark capturing and analyze the captured TCP packets
  ```

**User Datagram Protocol (UDP)**
---
- Fast but unreliable protocol
- Operates on transport layer
- Does not verify that the receiver is listening
- Higher layers of the TCP/IP stack handle reliability problems
- Connectionless protocol


**The Internet Layer**
---
- Responsible for routing packets to their destination address
- Uses a logical address, called an IP address
- IP addressing
- Packet delivery is connectionless


**Internet Control Message Protocol (ICMP)**
---
- Operates in the Internet layer of the TCP/IP stack
- Used to send messages related to network operations
- Helps in troubleshooting a network
- Popular commands include
  - ping
  - traceroute
- List of [ICMP control messages](https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol)

**Exercises**
* Use Wireshark to capture and analyze a ping request packet and its echo packet
  ```bash
  # 1. run Wireshark and start capturing packets on eth0
  # 2. from a command window, ping 8.8.4.4 twice
  ping 8.8.4.4 -c 2
  # 3. stop Wireshark capturing and analyze the captured ping packets
  # 4. find the route from your computer to 8.8.4.4
  traceroute 8.8.4.4
  ```

**IPv4 Addressing**
---
- Consists of four bytes, in *dot-decimal* notation 
  - 8.8.4.4, 192.168.100.123
- Two components: netId/hostId
  - netId: network address
  - hostId: host address
  - Neither portion may be all 1s or all 0s
- [Historical classful network architecture](https://en.wikipedia.org/wiki/IP_address)
  - Class A
  - Class B
  - Class C
- Subnetting
  - Each network can be assigned a subnet mask
  - Helps identify the network address bits from the host address bits
- Class A uses a subnet mask of 255.0.0.0
  - Also called /8
- Class B uses a subnet mask of 255.255.0.0
  - Also called /16
- Class C uses a subnet mask of 255.255.255.0
  - Also called /24  

**Planning IP Address Assignments**
---
- Each network segment must have a unique network address
- Address cannot contain all 0s or all 1s
- To access computers on other networks
  - Each computer needs IP address of gateway
- TCP/IP uses subnet mask to determine if the destination computer is on the same network or a different network
  - If destination is on a different network, it relays packet to gateway
  - Gateway forwards packet to its next destination (routing)
  - Packet eventually reaches destination

**IPv6**
---
- Modern operating systems like Windows 10 use [IPv6](https://en.wikipedia.org/wiki/IPv6) in addition to IPv4
- [IPv6 addresses](https://en.wikipedia.org/wiki/IPv6_address) are much longer: 128 bits instead of the 32 bits used by IPv4
  - Represented as eight groups of four hexadecimal digits
    - 2001:0db8:85a3:0000:0000:8a2e:0370:7334


**Numbering system**
---
- Four popular numbering systems used in computer
  - binary uses only 0 and 1
    - 4 bits per nibble, or 1 hex digit
    - 8 bits per byte
  - octal uses 0-7
    - 3 bits per digit
  - hexadecimal uses 0-9 and a-f
    - 4 bits per digit
    - 2 digits per byte
  - [base64](https://en.wikipedia.org/wiki/Base64) uses printable characters to represent binary data 
    - represents a sequence of bytes in groups of 3-bytes that can be represented by four 6-bit Base64 digits

**Exercises**

Using Python3 to do number conversion in different numbering systems.

```python
# 1. run python3 in a command window
# 2. decimal number <-> binary/octal/hex number
decnum = 123
bin(decnum) # dec->binary
int('0b111_1011',2) # binary->dec
oct(decnum) # dec->octal
int('0o173',8) # octal->dec
hex(decnum) # dec->hex
int('0x7b',16) # hex->dec
```

**Base 64 Encoding**
---
- Used to evade anti-spam tools, and to obscure passwords
- Encodes six bits at a time (0 – 63) with a single ASCII character
  - A - Z:		0 – 25
  - a – z:		26 – 51
  - 1 – 9:		52 – 61
  - \+ and /:	62 and 63
  - Padding: =

**Exercises**
* Encode and decode with [Base64 online tool](https://www.base64decode.org/)
  * Encode "Ethical hacking is fun!" then decode
  * Encode an image with Base64 then decode
* Encode and decode in Base64 with Python
  ```python
  import base64
  plaintex = b"Ethical hacking is fun!"
  # encode
  enb64code = base64.b64encode(plaintex)

  print("plaintext:", plaintext)
  print("Base64 encoded:", enb64code)

  # decode
  deb64text = base64.b64decode(enb64code)
  print("Base64 decoded:", deb64text)
  ```



## References
* [Wireshark doc](https://wiki.wireshark.org/Home)
* [Wikiversity Wireshark](https://en.wikiversity.org/wiki/Wireshark)