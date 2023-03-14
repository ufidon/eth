# Taking Control of a Server with Armitage

## Description
- Take control of a server on which EasyFtp Server 1.7.0.11 is installed and on service with [Armitage](https://www.kali.org/tools/armitage/)
  - There is a vulnerability of stack-based buffer overflow in [EasyFTP Server 1.7.0.11 and earlier](https://www.rapid7.com/db/modules/exploit/windows/ftp/easyftp_cwd_fixret/)
  - There is an [exploit](https://www.exploit-db.com/exploits/14402) integrated with [metasploit-framework](https://github.com/rapid7/metasploit-framework/blob/master/modules/exploits/windows/ftp/easyftp_cwd_fixret.rb)
  - Armitage is a GUI interface to ease the use of [Metasploit-Framework](https://www.metasploit.com/)
- There are [many software](https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=buffer+overflow) contain the vulnerability of buffer overflow, but not all of them can be used to take control of a server

## Equipments
- Both the Kali Linux VM 🐧 and the Windows server VM 🪟

## Tasks
On Windows server VM, 🪟

0. Stop the FileZilla server
1. Install, configure and run EasyFTP
   1. Download [EasyFTP Server 1.7.0.11](./easyftp-server-1.7.0.11-en.7z)
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

2. Test the Windows FTP service is ready
  ```bash
  ftp Windows_VM_IP
  ```
3. Install armitage and initialize Metasploit-Framework database
  ```bash
  # 3.1 run armitage, a prompt says that armitage is not installed, go ahead install it
  armitage
  sudo apt install armitage
  # 3.2 initialize metasploit-framework database\
  sudo msfdb init
  # 3.3 run armitage again
  armitage
  ```
4. Scan the Windows VM from Armitage
   1. In armitage, from its menu: Hosts -> Nmap Scan -> Intense Scan. In the popup textbox, enter your Windows VM IP
   2. Wait until the scan complete. Now the target machine (your windows vm) appear in the armitage windows
5. Exploit the target with the easyftp_cwd_fixret attack
   1. In armitage, find the easyftp_cwd_fixret attack, drag it then drop it on the target machine icon
   2. In the popup box, at its bottom, select "9=>Windows Universal - v1.7.0.11" from the drop-down list
   3. Launch the attack. When the attack succeeds, the target machine shows electric arc graphics on it indicating this box is owned!
6. Looting: post-exploitation
   1. Right-click the owned box, from the popup menu, try each item
   2. Close armitage

On Windows server VM, 🪟

7. Hardening the target machine by turning on Data Execution Protection (DEP) 
8. Restart Windows server VM then restart EasyFTP

On Kali Linux VM, 🐧

9. Launch the easyftp_cwd_fixret exploit again

On Windows server VM, 🪟

10. If you see a box pops up saying "ftpbasicsvr.exe has stopped working", then DEP has saved your server by stopping the attack!




# Reference
- [samsclass Project 3: Taking Control of a Server with Armitage](https://samsclass.info/123/proj10/123p3arm.htm)