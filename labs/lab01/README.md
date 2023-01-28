# Lab01: Configuring Windows server for ethical hacking

## 1. Description
Windows server 2019 provides two protections:

* Firewall
* Antivirus - Windows Defender

To practice ethical hacking on this system, these two protections need to be turned off and lowering other security settings. 

**Prerequisite**: the Windows server 2019 VM setup in Lab00.

## 2. Tasks
### Task 1: Lowering security settings
Follow Task2 of the [reference](https://samsclass.info/123/proj10/123p2win.htm), there could be some differences between Windows server 2016 and Windows server 2019. Run all commands as Administrator. For each security setting, take two screenshots:
* one shows the security if on
* the other one shows the security setting is off

1. Turn off automatic updates with command *sconfig*
2. Disable IE enhanced security configuration otherwise we can't download and install software.
   1. Download and install Google Chrome browser
3. Disable Windows Defender realtime protection
4. Turn off the firewall
5. Lower Data Execution Prevention (DEP) settings
   1. In the Windows search box, type "View advanced system settings"
   2. Close all open Windows and restart Windows server 2019 VM
6. Install and check VMware guest additions if you did not install it in Lab00
7. Find the system information with command systeminfo in a Command Prompt window
    ```cmd
    systeminfo
    ```
8. Check how many days you have left in your trial
    ```powershell
    # see how many days you have left in your trial
    slmgr -dlv
    ```
9. Extend the trial period in Powershell if you use an expired trial Windows server
    ```powershell
    # extend the trial for another 180 days
    slmgr -rearm
    ```    

### Task 2
In lab00, pinging to Windows server VM from Kali VM receives no response.
Do it again and show your result.

```bash
ping windows_server_vm_IP -c 2
```

### Task 3
1. In Windows server VM, download and install both [FileZilla client and server](https://filezilla-project.org/)
   1. [FileZilla Client](https://wiki.filezilla-project.org/Client_Installation)
      1. Decline any binding software
      2. Install for All users
   2. [FileZilla Server](https://wiki.filezilla-project.org/FileZilla_FTP_Server)
      1. Choose all default installation options
      2. You may refer to this [Youtube video](https://youtu.be/XXLnkeNjdCo)
2. Through its administration interface, configure FileZilla server, refer to the previous video
   1. Under Protocols settings
      1. Set the welcome message to be "FileZilla FTP server for ethical hacking"
      2. Tick passive mode with suggested port number
   2. Under Rights management -> Users
      1. Add a new user named "test" and set a password
      2. For the mount points, 
         1. put / in virtual path
         2. set the native path to be "c:\users\test", tick "Create native directory if it dose not exist"
      3. Put "for ethical hacking" in the Description box
3. From Kali VM, open a terminal window, login onto the FileZilla server with as user test
    ```bash
    # 1. create a test file under current folder
    echo "This is a test file from Kali" > test.txt
    # 2. login onto the FileZilla server with as user test
    ftp windows_server_vm_IP # the ip address you got with ipconfig /all in Windows VM)
    # 3. upload test.txt to FileZilla server
    ftp> put test.txt
    ```
4. On Windows VM, go to the folder c:\users\test
   1. Find and open test.txt uploaded from Kali
   2. Create a text file named winserver.txt and put the following sentence inside
    ```
    Hello from Windows Server!
    ```
   3. Go back to Kali VM, in the previous ftp session, download winserver.txt
    ```bash
    # 1. list remote folder
    ftp> ls
    # 2. download winserver.txt
    ftp> get winserver.txt
    # 3. quit ftp session
    ftp> bye
    # 4. print the contect of winserver.txt
    cat winserver.txt
    ```
### Task 4
1. Install and configure OpenSSH server and client on Windows VM. Open Powershell as administrator.
    ```powershell
    # 1. check you're a member of the built-in Administrators group.
    (New-Object Security.Principal.WindowsPrincipal([Security.Principal.WindowsIdentity]::GetCurrent())).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)

    # 2. Find the available OpenSSH server and client
    Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'

    # 3. install the server or client
    Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
    Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

    # 4. start and configure OpenSSH Server
    Start-Service sshd
    Set-Service -Name sshd -StartupType 'Automatic'

    # Configure firewall rule
    if (!(Get-NetFirewallRule -Name "OpenSSH-Server-In-TCP" -ErrorAction SilentlyContinue | Select-Object Name, Enabled)) {
        Write-Output "Firewall Rule 'OpenSSH-Server-In-TCP' does not exist, creating it..."
        New-NetFirewallRule -Name 'OpenSSH-Server-In-TCP' -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
    } else {
        Write-Output "Firewall rule 'OpenSSH-Server-In-TCP' has been created and exists."
    }
    ```
2. From Kali VM, open a terminal window, login onto Windows VM OpenSSH server by ssh command
    ```bash
    ssh Administrator@windows_server_vm_ip
    ```

# References
* [Sam's class: Project 2: Windows 2016 Server Virtual Machine](https://samsclass.info/123/proj10/123p2win.htm)
* [How To Enable Ping In Windows Server 2019 Firewall](https://www.rootusers.com/how-to-enable-ping-in-windows-server-2019-firewall/)
* [Install OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell)
  * [Installing and Configuring OpenSSH on Windows Server 2019](https://techcommunity.microsoft.com/t5/itops-talk-blog/installing-and-configuring-openssh-on-windows-server-2019/ba-p/309540)
  * [How to Enable and Configure SSH Server on Windows with OpenSSH?](https://woshub.com/connect-to-windows-via-ssh/)
* [How to recover FileZilla FTP Server’s Admin Password](https://www.how2shout.com/how-to/filezilla-server-admin-password-recovery.html)
  * FileZilla FTP Server's settings are saved in the hidden folder by default
    ```cmd
    C:\Users\username\AppData\Roaming\FileZilla
    :: When FileZilla is installed by the Administrator, username is Administrator
    ```