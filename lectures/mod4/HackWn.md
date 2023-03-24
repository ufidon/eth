# Hacking Wireless Networks

Objectives
---
- Describe and explain
  - wireless technology
  - wireless networking standards
  - the process of authentication
  - wardriving
  - wireless hacking
- Explore and exploit tools used by hackers and security professionals


Wireless Technology
---
- A wireless network functions with the right hardware and software
- Wireless technology is part of our lives
  - Baby monitors
  - Keyless entry systems
  - Cellphones and smartphones
  - GPS
  - Remote controls
  - Garage door openers
  - Two-way radios
  - Bluetooth speakers


Wireless Network Components
---
- Access Point (AP)
  - connects to  the wired network with an Ethernet cable
  - Not all wireless networks connect to a wired network
    - Starlink
  - Most companies have Wireless LANs (WLANs) that connect to their wired network topology
- Wireless network interface card (WNIC)


Access Point (AP)
---
- has channels configured 
- enables users to connect to a WLAN using wireless technology
- available only within a defined area
- A wireless router includes an access point, a router, and a switch


Reading ✏️
---
- Explore Wi-Fi network scanner applications for their capabilities
  - [Kismet: Wi-Fi, Bluetooth, RF, and more](https://www.kismetwireless.net/)
  - [inSSIDer](https://www.metageek.com/inssider/)
    - [netstumbler](http://www.netstumbler.com/)


Service Set Identifiers (SSIDs)
---
- Name used to identify the wireless local area network (WLAN)
- The SSID is configured on the AP
  - Unique 1- to 32-character alphanumeric name
  - Name is case sensitive
- Wireless computers need to configure the SSID before connecting to a wireless network
- transmitted with each packet
  - Identifies which network the packet belongs
- The AP usually broadcasts the SSID
- Many vendors have SSIDs set to a default value that companies never change
- An AP can be configured to not broadcast its SSID until after authentication
  - Wireless hackers can attempt to guess the SSID
- Verify that your clients or customers are not using a default SSID


Practice ✏️
---
- Find default SSIDs for popular routers
  - D-Link
  - Netgear
  - Belkin
  - Cisco
  - Compaq


Configuring an Access Point
---
- Most devices allow access through any Web browser
- Enter IP address on your Web browser
  - login with your user logon name and password
  - default or initial logon name and password are printed on the back of AP device


Configuring an Access Point
---
- Change the default SSID
  - Turn off SSID broadcast
- Wired Equivalent Privacy (WEP) encryption
- WPA (WiFi Protected Access ) is better


Wireless NICs
---
- used to connect to WiFi by each node or computer
- Convert the radio waves to/from digital signals
- Choose a NIC for your purpose
  - Some tools require certain specific brands of NICs
    - Cracking WEP requires NICs with monitor mode or 
    - ability to inject packets


Wireless Network Standards
---
- a set of rules formulated by an organization
- Institute of Electrical and Electronics Engineers (IEEE)
  - Defines several standards for wireless networks


IEEE Standards
---
- pass through these groups:
  - Working group (WG)
  - Sponsor Executive Committee (SEC)
  - Standards Review Committee (RevCom)
  - IEEE Standards Board
- IEEE Project 802
  - LAN and WAN standards


[The 802.11 Standard]((https://en.wikipedia.org/wiki/IEEE_802.11))
---
- The first wireless technology standard
- Defined wireless connectivity at 1 Mbps and 2 Mbps within a LAN
- Applied to layers 1 and 2 of the OSI model
- Wireless networks cannot detect collisions
  - Carrier sense multiple access/collision avoidance (CSMA/CA) is used instead of CSMA/CD


Wireless LANs Addressing
---
- not associated with a physical location
- An addressable unit is called a station (STA)


The Basic Architecture of 802.11
---
- uses a basic service set (BSS) as its building block
- nodes within a BSS can communicate with each other
- requires a distribution system (DS) to connect two BSSs


[Frequency Range](https://en.wikipedia.org/wiki/IEEE_802.11n-2009)
---
- In the United States, Wi-Fi uses frequencies near 2.4 GHz
  - (Except 802.11a at 5 GHz)
- There are 11 channels, 
  - but they overlap 
  - only three are commonly used


Infrared (IR)
---
- Infrared light can’t be seen by the human eye
- IR technology is restricted to a single room or line of sight
- IR light cannot penetrate walls, ceilings, or floors


Reading ✏️
---
- Explore [IEEE Additional 802.11 Projects](https://en.wikipedia.org/wiki/IEEE_802.11)
- Explore [IEEE 802.15 standards](https://en.wikipedia.org/wiki/IEEE_802.15)


[Bluetooth](https://en.wikipedia.org/wiki/Bluetooth)
---
- Defines a method for interconnecting portable devices without wires
- Maximum distance allowed is 10 meters
- It uses the 2.45 GHz frequency band
- Throughput of up to 2.1 Mbps for Bluetooth 2.0
  - Up to 24 Mbps for Bluetooth 3.0 


Reading ✏️
---
- Explore [Cellular network](https://en.wikipedia.org/wiki/Cellular_network)
- Explore [Starlink](https://en.wikipedia.org/wiki/Starlink)


Reading 📝
---
- [Wireless capture on Windows](https://blog.packet-foo.com/2019/04/wireless-capture-on-windows/comment-page-1/)
  - [Wireless Cards and NetHunter](https://www.kali.org/docs/nethunter/wireless-cards/)
  - [WLAN (IEEE 802.11) capture setup in WireShark](https://wiki.wireshark.org/CaptureSetup/WLAN)


Wireless network authentication
---
- Establishes that a user is authentic—authorized to use the network
- If authentication fails, anyone in radio range can use your network
- The 802.1X Standard
  - Defines the process of authenticating and authorizing users on a WLAN
    - Point-to-Point Protocol (PPP)
    - Extensible Authentication Protocol (EAP)
    - Wired Equivalent Privacy (WEP)
    - Wi-Fi Protected Access (WPA)


Point-to-Point Protocol (PPP)
---
- Many ISPs use PPP to connect dial-up or DSL users
- PPP handles authentication with a user name and password
  - sent with PAP or CHAP
  - PAP (Password Authentication Protocol) sends passwords unencrypted
    - Vulnerable to trivial sniffing attacks


CHAP (Challenge-Handshake Authentication Protocol) Vulnerability
---
- Server sends a Challenge with a random value
- Client sends a Response, hashing the random value with the secret password


Practice 📝
---
- [Assless-Chaps : Crack MSCHAPv2 Challenge/Responses Quickly Using A Database Of NT Hashes](https://kalilinuxtutorials.com/assless-chaps/)


Extensible Authentication Protocol (EAP)
---
- an enhancement to PPP
- Allows a company to select its authentication method
  - Certificates
  - Kerberos
    - used on LANs for authentication
    - Uses Tickets and Keys
    - Used by Windows 2000, XP, and 2003 Server by default
    - Not common on WLANS




X.509 Certificate
---
- Record that authenticates network entities
- Identifies
  - The owner
  - The certificate authority (CA)
  - The owner’s public key
    - used to encrypt data


Practice 📝
---
- Explore certificates 
  - downloaded when browsing a HTTPS website
    - click the padlock icon at the left of the URL address box
  - installed in Chrome browser or Firefox browser


Lightweight Extensible Authentication Protocol (LEAP)
---
- A vulnerable Cisco product
- Joshua Wright wrote the [ASLEAP hacking tool to crack LEAP](https://github.com/joswr1ght/asleap)


More Secure EAP Methods
---
- Extensible Authentication Protocol-Transport Layer Security (EAP-TLS)
  - Secure but rarely used
    - because both client and server need certificates signed by a CA
- Protected EAP (PEAP) and Microsoft PEAP
  - Very secure, only requires server to have a certificate signed by a CA


802.1X components
---
- Supplicant
  - The user accessing a WLAN
- Authenticator
  - The AP
- Authentication server
  - Checks an account database to see if user’s credentials are acceptable
  - May use RADIUS (Remote Access Dial-In User Service)


Wired Equivalent Privacy (WEP)
---
- Part of the 802.11b standard
- Encrypts data on a wireless network
- WEP has many vulnerabilities


Practice 📝
---
- [WEP Cracking with Kali Linux](https://www.yeahhub.com/wep-cracking-kali-linux-2018-1-tutorial/)


Wi-Fi Protected Access (WPA)
---
- Specified in the 802.11i standard
- Replaces WEP
- improves encryption by using Temporal Key Integrity Protocol (TKIP)
- adds an authentication mechanism implementing 802.1X and EAP


TKIP Enhancements
---
- Message Integrity Check (MIC)
  - Prevent attacker from injecting forged packets 
- Extended Initialization Vector (IV) with sequencing rules
  - Prevent replays (attacker re-sending copied packets)
- Per-packet key mixing
  - MAC addresses are used to create a key
  - Each link uses a different key
- Rekeying mechanism
  - Provides fresh keys
  - Prevents attackers from reusing old keys


WPA and WPA-2
---
- WPA only implements part of 802.11i, using TKIP
  - Can run on older hardware
- WPA2 implements the full IEEE 802.11i security standard, using CCMP
  - Counter Mode with Cipher Block Chaining Message Authentication Code Protocol (CCMP)
  - More secure


Pre-Shared Key v. 802.1x
---
- Both WPA and WPA-2 can run in either mode
- Pre-Shared Key uses a passphrase the user types into each device
  - Less secure because 
    - the user might choose a guessable passphrase 
    - all devices on the WLAN use the same passphrase
- 802.1x uses a server to manage keys
  - Each user has a different key
  - More secure


Hacking WPA
---
- In 2008 and 2009, some new WPA attacks were developed, for its weakest form (TKIP)
  - These attacks allow injection of spoofed packets for limited periods of time
    - Up to 18 minutes
  - They don't find the WPA key, but they are a warning that it's time to go to WPA-2


Practice 📝
---
- [Crack WPA/WPA2 WiFi Passwords using Aircrack-ng & Kali Linux](https://nooblinux.com/crack-wpa-wpa2-wifi-passwords-using-aircrack-ng-kali-linux/)


Wardriving
---
- Hackers use wardriving
  - Finding insecure access points
  - Using a laptop or palmtop computer
- Wardriving is not illegal
  - But using the resources of these networks is illegal
- Warflying
  - Variant where an airplane is used instead of a car


How to wardrive
---
- An attacker or security tester simply drives around with the following equipment
  - Laptop computer
  - Wireless NIC
  - An antenna
  - [Software that scans the area for SSIDs](https://www.kali.org/tools/kismet/)
- Not all wireless NICs are compatible with scanning programs
- Antenna prices vary depending on the quality and the range they can cover
- Scanning software can identify
  - The company’s SSID
  - The type of security enabled
  - The signal strength
  - Indicating how close the AP is to the attacker


NetStumbler
---
- Shareware tool written for Windows that enables you to detect WLANs 
  - Supports 802.11a, 802.11b, and 802.11g standards
- primarily designed to
  - Verify your WLAN configuration
  - Detect other wireless networks
  - Detect unauthorized APs
- capable of interface with a GPS
  - to map out locations of all the WLANs the software detects
- logs the following information
  - SSID
  - MAC address and Manufacturer of the AP
  - Channel
  - Signal Strength
  - Encryption (but not level of encryption)


Kismet
---
- Another product for conducting wardriving attacks
- Runs on Linux, BSD, MAC OS X, and Linux PDAs
- advertised also as a sniffer and IDS (Intrusion Detection System)
  - can sniff 802.11b, 802.11a, and 802.11g traffic
- features
  - Ethereal- and Tcpdump-compatible data logging
  - AirSnort compatible
  - Network IP range detection
  - Hidden network SSID detection
  - Graphical mapping of networks
  - Client-server architecture
  - Manufacturer and model identification of APs and clients
  - Detection of known default access point configurations
  - XML output
  - Supports more than 25 card types


Practice ✏️
---
- Explore Wi-Fi network scanner applications for wardriving
  - [Kismet: Wi-Fi, Bluetooth, RF, and more](https://www.kismetwireless.net/)
  - [inSSIDer](https://www.metageek.com/inssider/)
    - [netstumbler](http://www.netstumbler.com/)


Wireless Hacking
---
- not much different from hacking a wired LAN
- Techniques for hacking wireless networks
  - Port scanning
  - Enumeration
- Equipment
  - Laptop computer
  - A wireless NIC
  - An antenna
  - Sniffer software


Reading ✏️
---
- Explore the features of
  - [AirCrack NG](https://www.kali.org/tools/aircrack-ng/)


Practice ✏️
---
- [Bypass MAC address filtering](https://kalitut.com/bypass-mac-filtering-wifi/)


Countermeasures for Wireless Attacks
---
- Anti-wardriving software makes it more difficult for attackers to discover your wireless LAN
  - Honeypots
    - Servers with fake data to snare intruders
  - Fakeap and Black Alchemy Fake AP
    - Software that makes fake Access Points
- Use special paint to stop radio from escaping your building
- secure configuration
  - Allow only predetermined MAC addresses and IP addresses to have access to the wireless LAN
  - Use an authentication server instead of relying on a wireless device to authenticate users
  - Use an EAP authentication protocol
  - If you use WEP, use 104-bit encryption rather than 40-bit encryption
    - But just use WPA instead
  - Assign static IP addresses to wireless clients instead of using DHCP
  - Don’t broadcast the SSID
  - Place the AP in the demilitarized zone (DMZ) 
- pentest with [pineapple](https://shop.hak5.org/)


# References
- [attack and defense labs](https://attackdefense.pentesteracademy.com/)
- [Step By Step Kali Linux and Wireless Hacking Basics WEP Hacking Part 3](https://www.wirelesshack.org/step-by-step-kali-linux-and-wireless-hacking-basics-wep-hacking-part-3.html)
