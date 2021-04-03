---
layout: single
title:  "Blocky Writeup [ES] - HackTheBox"
date:   2021-03-29 04:00:00 -0400
classes: wide
categories: HTB
tags:
 - OSCP
---

En esta ocasión estaré trabajando con la máquina **Blocky** de **HackTheBox** como práctica para el OSCP Path. Esta máquina es bastante sencilla como se verá a continuación.

## Box info

![Machine Info](/images/HTB/Blocky/00-info-machine.png "Machine Info"){: .align-center}


## Enumeration


* ```nmap -sC -sV -p21,22,80,25565 10.10.10.37```

```go
Nmap scan report for 10.10.10.37
Host is up (0.21s latency).

PORT      STATE SERVICE   VERSION
21/tcp    open  ftp       ProFTPD 1.3.5a
22/tcp    open  ssh       OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 d6:2b:99:b4:d5:e7:53:ce:2b:fc:b5:d7:9d:79:fb:a2 (RSA)
|   256 5d:7f:38:95:70:c9:be:ac:67:a0:1e:86:e7:97:84:03 (ECDSA)
|_  256 09:d5:c2:04:95:1a:90:ef:87:56:25:97:df:83:70:67 (ED25519)
80/tcp    open  http      Apache httpd 2.4.18 ((Ubuntu))
|_http-generator: WordPress 4.8
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: BlockyCraft &#8211; Under Construction!
25565/tcp open  minecraft Minecraft 1.11.2 (Protocol: 127, Message: A Minecraft Server, Users: 0/20)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

