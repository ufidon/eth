# Attacking web servers

## Description
- Learn how to use WebGoat and WebWolf
- Learn HTTP, web developer tools and CIA triad
- Practice basic SQL injection attack and XSS attack

## Equipment
- Kali Linux VM 🐧 OR Windows server VM 🪟 OR Windows 10/11

**How to setup and run WebGoat/WebWolf?**

**Method 1: using docker**

In Kali Linux VM 🐧 or Linux host, 
- [install docker](https://www.kali.org/docs/containers/installing-docker-on-kali/)
- run using docker

```bash
# 1. install docker
sudo apt update -y && sudo apt upgrade -y
sudo apt install -y docker.io
sudo systemctl enable docker --now
sudo usermod -aG docker $USER
# !!!  logout and in again, or restart Kali VM
# 2. run webgoat using docker, webwolf will be started automatically
docker run -it -p 127.0.0.1:8080:8080 -p 127.0.0.1:9090:9090 webgoat/webgoat
# or
docker run --name webgoat -it -p 127.0.0.1:8080:8080 -p 127.0.0.1:9090:9090 webgoat/webgoat
```
- In a browser, access 
  - WebGoat: http://localhost:8080/WebGoat
  - WebWolf: http://localhost:9090/WebWolf


**Method 2: using jar**

- Uninstall any previously installed JDK and JRE
- Download and install [JDK FX 17+](https://www.azul.com/downloads/#zulu)
  - choose the right version for your operating system, for example
    - Java Version: Java 17 (LTS)
    - Operating System: Windows
    - Architecture: x86 64-bit
    - Java Package: **JDK FX**
    - File format: **.msi**
  - During the installation,
    - make sure choose "Set JAVA_HOME variable -> Entire feature will be installed on local hard drive" during the installation
    - i.e. install everything on local hard drive
- Download [the latest WebGoat standalone jar file](https://github.com/WebGoat/WebGoat/releases)
- Run WebGoat in command prompt or terminal

```cmd
:: cd to the folder contains your jar file
cd folder_contains_the_jar_file
:: change the jar file name in the command line to yours
java -Dfile.encoding=UTF-8 -Dwebgoat.port=8080 -Dwebwolf.port=9090 -jar webgoat-2023.4.jar
```

- In a browser, access 
  - WebGoat: http://localhost:8080/WebGoat
  - WebWolf: http://localhost:9090/WebWolf

## Tasks
In WebGoat, complete the following lessons:

1. Introduction
   1. WebGoat
   2. WebWolf
2. General
   1. HTTP basics
   2. HTTP proxies
   3. Developer tools
   4. CIA triad
3. (A3) Injection
   1. SQL Injection (intro)
   2. Cross Site Scripting


# Reference
- [OWASP WebGoat](https://owasp.org/www-project-webgoat/)