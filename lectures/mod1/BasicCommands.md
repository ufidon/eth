# Basic Windows & Linux Commands

**Objectives**
* Exploit basic Windows & Linux commands


## Basic [Windows commands](./commandCheatsheets/CommandPromptCheatsheet.pdf)

**Path representation on Windows**
---
- Absolute path
  - C: is the C drive
  - C:\user\Documents is the Document folder
  - C:\user\Documents\commands.txt is a file in the Documents folder
- Relative path
  - Documents
  - Documents\commands.txt
  - . current folder
  - .. parent folder


**Basic commands**
---
* help - get help on commands
  * help: list all commands
  * help cls: get help on cls commands
* echo - display message or turn on/off message echoing
  * echo This is a message
  * echo on/off
* cls - clear the screen
* exit - exit current command prompt or batch scripts


**Directory management commands**
---
* dir - display the contents of a folder
  * dir: show current folder
  * dir folder
* cd - change directory
  * cd: show the current folder
  * cd folder
  * cd .. 
* md/mkdir - create a folder
* rm/rmdir - remove a folder
  * rm folder: remove an empty folder
  * rm /s folder: remove an non-empty folder


**File management commands**
---
* copy - copy a file from one location to another
  * copy srcFilepath dstFilepath
* move - move a file from one location to another
  * move srcFilepath dstFolder
* ren/rename - rename a file
  * ren oldname newname
* del - delete one or more files
  * del filename
* type - display the content of a file
  * type filename
* fc - compare two files and display their difference
  * fc file1 file2


**User management**
* [net user](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771865(v=ws.11))
  * net user: displays a list of all user accounts for the local computer
  * net user username: displays information about the user account username
  * net user username /add: add a new user with username


**Network management**
* [netstat](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/ff961504(v=ws.11)) displays active TCP connections, routing table and other internet information.
  * netstat: displays active TCP connections
  * netstat -e -s: displays both the Ethernet statistics and the statistics for all protocols
  * netstat -s -p tcp udp: displays the statistics for only the TCP and UDP protocols
  * netstat -o 5: displays active TCP connections and the process IDs every 5 seconds
  * netstat -n -o: displays active TCP connections and the process IDs using numerical form
* arp - Displays or changes items in the address resolution protocol cache, which maps IP addresses to physical addresses
* ipconfig - Displays Windows IP Configuration
* ping - Send ICMP/IP "echo" packets over the network to the designated address (or the first IP address that the designated hostname maps to via name lookup) and print all responses received


## Basic [Linux commands](./commandCheatsheets/LinuxCommandMemento.pdf)

**Path representation on Linux**
---
- Absolute path
  - / is the root folder
  - /home/user/Documents is the Document folder
  - /home/user/Documents/commands.txt is a file in the Documents folder
- Relative path
  - Documents
  - Documents/commands.txt
  - . current folder
  - .. parent folder