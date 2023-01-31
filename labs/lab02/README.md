# Footprinting and Port Scanning

## Task 1: Footprinting
* Select any domain name as your choice – your target  for the following tasks
1. Footprinting with command [whois](https://www.computerhope.com/unix/uwhois.htm) in Kali VM.
    ```bash
    # syntax: whois domain_name
    whois handsonsecurity.net
    ```
2. Footprinting with 
   * [ICANN online whois tool](https://lookup.icann.org/en/lookup), or
   * [whois lookup on Domaintools](https://whois.domaintools.com/)
3. Getting information of Mail Exchange Server of your selected domain name with [nslookup](https://www.computerhope.com/unix/unslooku.htm)
    ```bash
    nslookup -type=mx handsonsecurity.net
    ```


## Task 2: Port Scanning
In this task, both Windows VM and Kali VM are needed, keep them running. Inside Kali, open an terminal run 'sudo inetsim' and keep it running.

1. Ping sweeping with [Angry IP scanner](https://angryip.org)
   1. Download and install Angry IP scanner on Windows VM
   2. You may need to download and install a Java JDK FX as well
      1. [Azul Java 11, Windows, x86 64-bit JDK FX](https://www.azul.com/downloads/?version=java-11-lts&os=windows&architecture=x86-64-bit&package=jdk-fx) is recommended. Download and install the .msi file.
   3. ping sweep the NAT network and report your findings.

2. Port scanning with nmap command in Kali VM and [Zenmap](https://nmap.org/zenmap/) in Windows VM. Carry out the following four types of scan on the NAT network:
   1. SYN scan (Half Scan) 
   2. NULL scan 
   3. XMAS scan 
   4. Connect scan (Full Connect Scan)

3. [Packet crafting with hping3](https://github.com/Samsar4/Ethical-Hacking-Labs/blob/master/2-Scanning-Networks/1-hping3.md) in Kali VM.
   1. Prepare wireshark on Windows VM
      1. Download and install [wireshark](https://www.wireshark.org/) on Windows VM
      2. Close browser
      3. Run wireshark and keep capturing
   2. Run FileZilla server administration on Windows VM
   3. Craft TCP SYN packets with hping3 on Kali VM
    ```bash
    hping3 -S Windows_VM_ip -p 21 -c 2
    ```
   4. Go back to Windows VM
      1. Stop wireshark capture and report your findings
      2. Check FileZilla server logs and report your findings


# References
* [Ethical Hacking Labs](https://github.com/Samsar4/Ethical-Hacking-Labs)