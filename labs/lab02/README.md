# Footprinting and Port Scanning

A. Footprinting
---
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


B. Port Scanning
---