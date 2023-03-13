# lab00: Setup lab environment
# Option 2: Cloud installation


## 1.Description
**In this lab, we will build our own penetration test environment using Kali Linux and Windows server**

Find a cloud with free trial such as Google cloud, Microsoft Azure, etc.

* Create a virtual machine for Kali Linux
* Create a virtual machine for Windows server


**Prerequisite:**

You must be able to access the cloud from your computer with a browser.

## 2.Steps

1. (25%)Install Kali Linux
Follow the steps below to setup Kali Linux in its VM:

* [Create a Linux VM instance in Compute Engine](https://cloud.google.com/compute/docs/create-linux-vm-instance)

   ```bash
   default username: kali
   default password: kali
   ```


2. (25%)Install Windows server

   * [Create a Windows Server VM instance in Compute Engine](https://cloud.google.com/compute/docs/create-windows-server-vm-instance)

   * Extending the Trial Period (If you have an old one)
     In Powershell, execute this command to see how many days you have left in your trial:

     slmgr -dlv

     Execute this command to extend the trial for another 180 days:

     slmgr -rearm

     You can extend the trial six times, for up to three years.

3. (30%) Show the NAT network is working
	 * On the Windows Server VM, find its ip configuration of the Ethernet adapter connected to the NAT: 	
    ```cmd
    ipconfig /all
    :: take a note of your Windows VM IP address
    ```
	 * On the Kali Linux VM, find its ip configuration of the Ethernet adapter connected to the NAT: 	
    ```bash
    ifconfig -a
    :: take a note of your Kali Linux VM IP address
    ```
	 * from the Windows server VM ping the Kali VM
    ```cmd
    ping KaliIP // the Kali ip address noted before
    ```
	 * from the Kali VM ping the Windows server VM
    ```bash
    ping WindowsIP // the Windows ip address noted before
    ```

**Note**

Please fully update your Kali at home, it takes a long time.

```bash
sudo apt update
sudo apt upgrade
```


*Optional*

After installation, *make sure you can access Internet*, update and upgrade Kali, then install the following tools. Open a terminal window, run the following commands:

```bash
# 1. populate the repository
# use a text editor open /etc/apt/sources.list with sudo then add the following two lines if there are not there
deb http://http.kali.org/kali kali-rolling main contrib non-free
deb-src http://http.kali.org/kali kali-rolling main contrib non-free
# 2. update, upgrade Kali then install several popular tools
sudo apt update
sudo apt full-upgrade -y
sudo apt install apt-transport-https dirmngr
sudo apt install p7zip-full build-essential gcc perl cmake automake curl git geany okular vim
```

## References
* *Google cloud*
  * [Kali Linux with GUI & 2500+ tools & apps on Google Cloud (GCP)](https://console.cloud.google.com/marketplace/product/techlatest-public/kali-linux)
    * [Launch Ubuntu Desktop on Google Cloud](https://ubuntu.com/blog/launch-ubuntu-desktop-on-google-cloud)
  * [Gcloud instance can't ping another one](https://stackoverflow.com/questions/36918142/gcloud-instance-cant-ping-another-one)
* *Projects from samsclass*
  * [Project 1C: Google Cloud Machines](https://samsclass.info/123/proj14/p1cgc.htm)
  * [Project 2C: Katoolin](https://samsclass.info/123/proj14/p2ckat.htm)

* *command line basics*
  * [Linux journey](https://linuxjourney.com/)
  * [Windows commands cheatsheet](./commandCheatsheets/CommandPromptCheatsheet.pdf)
  * [Linux commands cheatsheet](./commandCheatsheets/LinuxCommandMemento.pdf)
* _old os_
  * [WinWorld](https://winworldpc.com/library/operating-systems)
  * [Old versions of Linux](https://soft.lafibre.info/)
  * [archiveos](https://archiveos.org/)
* [Install Kali on VMware](https://samsclass.info/152/proj/M108.htm)
* [Kali Linux and Windows server 2012 VMs](https://drive.google.com/drive/folders/1fT7DlwAQjaDjCRsDDSDtaYZU2sCSLa_v)
  * Windows user/pass: Lab250/toor, Administrator/Admin123
  * Kali user/pass: root/toor
* [Immersive learning games](https://drive.google.com/drive/folders/1lrMrlt7txA1VviePt4koUjyxB6nedtLg)