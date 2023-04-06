# Cracking Windows Password Hashes


## Description
Practice cracking Windows password hashes using Cain & Abel and HashCat.

## Equipment
- Both the Kali Linux VM 🐧 and the Windows server VM 🪟

## Prerequisite!!!
- [Lab01](../lab01/README.md) must be done first if you use a new Windows VM


## Tasks
On Windows server VM 🪟, 

Task 1: Extract Windows password hashes with Cain & Abel
---
- 1.1 create a Windows test user in a command prompt running as Administrator
  ```cmd
  :: create a user named "test" with a password "P@ssw0rd"
  net user test P@ssw0rd /add
  ```

- 1.2 Download and install [7-zip](https://www.7-zip.org/) with default options

- 1.3 Download and install [Cain & Abel](../repo/ca_setup.7z)
  - Unzip ca_setup.7z then run the installer
  - Don't install WinPcap during the installation of Cain & Abel

- 1.4 Download and install [WinPcap](https://www.winpcap.org/install/) with default options
  - On its official webpage, click "Installer for Windows" to download and install it
  - If you have installed a new version, this installation will abort, it's fine

- 1.5 Extract Windows password hashes with Cain & Abel
  - Run Cain & Abel as Administrator, from its GUI
    - Choose  the Cracker tab, right-click in its blank client area
    - From the popup menu, choose "Add to list"
    - From the dialog "Add NT Hashes from", choose "Import Hashes from local system"
      - A table of user name, hashes ,etc. will show in the Cracker tab client area

There are two types of Windows password hashes: 
- LM Hashes: 
  - Weak, no longer used by Microsoft
  - In Cain & Abel, they are shown as dummy values that no longer include any information about real passwords
- NT hashes
  - used by Windows NT since 1993 and never updated

- 1.6 Find the NT hashes for password "P@ssw0rd" online using
  - Generate the NT hash of password "P@ssw0rd" using [NTLM Hash Generator](https://codebeautify.org/ntlm-hash-generator) or [NTLM Password Hasher](https://www.browserling.com/tools/ntlm-hash)
    - Is it the same as the one shown in Cain & Abel?
  - Decrypt all the NT hashes shown in Cain & Abel online using
    - [Decrypt hashes](https://hashes.com/en/decrypt/hash)
      - What did you get?


Task 2: Crack Windows password hashes with Cain & Abel
---
- 2.1 In the Cracker tab, right-click user test, in the popup dialog choose 
  - "Dictionary Attack"
    - Download the dictionary [rockyou.txt](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt)
    - Right-click the top blank area, choose "Add to lick", then add rockyou.txt
    - Click start to crack the NT hash
  - "Rainbowcrack-Online" (optional)
    - Explore its usage by yourself


Task 3: Export the NT hash to a text file
---
- In the Cracker tab, right-click user test and choose Export
  - save the file as WinNtHashes.txt
  - Open WinNtHashes.txt in notepad, copy the NT hash of user test


In Kali Linux VM 🐧, *put the following mentioned files in the same working folder*:

Task 4: Crack Windows password hashes with HashCat
---
- 4.1 Install 7-zip on Kali
  ```bash
  sudo apt install p7zip-full
  ```
- 4.2 Paste or type the NT hash of user test in Kali in a terminal window
  ```bash
  # replace "the NT hash of user test" with the true NT hash of user test
  echo "the NT hash of user test" > winnt.hash
  ```

- 4.3 Download [rockyou.txt.gz](https://github.com/praetorian-inc/Hob0Rules/blob/master/wordlists/rockyou.txt.gz), save it in your current working directory, then unzip it
  ```bash
  # 4.3.1. unzip rockyou.txt.gz
  7z e ./rockyou.txt.gz
  # rockyou.txt serves as the password dictionary for dictionary attack
  # 4.3.2. check the top 10 popular password
  head ./rockyou.txt
  # 4.3.3. find the total number of passwords in rockyou.txt
  wc -l ./rockyou.txt
  ```

- 4.4 Get Hashcat 2.00. *You may use the [Hashcat](https://www.kali.org/tools/hashcat/) installed in Kali VM.*
  - 4.4.1. Download [hashcat 2.00](../repo/hashcat-2.00.7z) and save it in the current working directory
  ```bash
  # 4.4.2. extract hashcat
  7z e ./hashcat-2.00.7z
  # 4.4.3. find the working hashcat for using later, if both work, choose the 64bit, or you may try both
  ./hashcat-cli32.bin -V
  ./hashcat-cli64.bin -V
  ```

- 4.5 Crack the NT hash
  ```bash
  # 4.5.1. crack user test's NT hash
  ./hashcat-cli64.bin -m 1000 -a 0 -o winpass.txt --remove winnt.hash ./rockyou.txt

  # explanation:
  # ▶️ Windows NT hashes (-m 1000)
  # ▶️ Using a dictionary attack (-a 0)
  # ▶️ Putting output in the file winpass.txt
  # ▶️ Removing each hash as it is found
  # ▶️ Getting hashes from winnt.hash
  # ▶️ Using the dictionary rockyou.txt

  # 4.5.2. show the cracked password, is it right?
  cat ./winpass.txt
  ```

- 4.6 Crack more NT hashes
  - crack the following NT hashes 
    ```
    affe290d23ab2db6aaea954f1f89248a
    a060e07b196a4a8a49c67e85f7447f47
    20dedcddc0cf3176db3bf18feb979953
    680817337519d1733f52e37dcade465a
    ```
  - 4.6.1. with online tools (you may find more tools online) and 
  - 4.6.2. Hashcat

*Optional*
---
- Generate NTLM hash in python
  ```python
  import hashlib

  def ntlm(p):
    h = hashlib.new('md4', p.encode('utf-16le')).digest().hex()
    print(h)
    return h

  [ ntlm(p)  for p in ('cherry','Happy123', 'xerox','youcanntcrackme')]
  ```


# Reference
- [samsclass: Project 12: Cracking Windows Password Hashes with Hashcat](https://samsclass.info/123/proj14/123p12winhash.htm)
- [Hashcat P@ssw0rd Cracking: Basic Usage](https://in.security/2022/06/01/hashcat-pssw0rd-cracking-basic-usage/)
  - [Practical examples of Hashcat usage](https://miloserdov.org/?p=5426)
  - [Cracking Microsoft Office password](https://tinyapps.org/docs/hashcat.html)
  - [Crack RAR Passwords](https://www.doyler.net/security-not-included/crack-rar-files-hashcat)
  - [Cracking .zip and .rar Archives with Passwords](https://wind010.hashnode.dev/cracking-zip-and-rar-archives-with-passwords)
- [Password Hashes](https://cybercop-training.ch/?p=213)
- [Impacket - a collection of Python classes for working with network protocols](https://github.com/fortra/impacket)