---
layout: single
title:  "Resolute Writeup [ES] (in progress)- HackTheBox"
date:   2021-04-24 17:00:00 -0400
published: false
classes: wide
categories: HTB
tags:
 - Privesc
 - OSCP
---



## Información de la máquina

![Machine Info](/images/HTB/Resolute/00-machine-info.png "Machine Info"){: .align-center}

asd

[Resolute](https://app.hackthebox.eu/machines/220) es una máquina Windows de la plataforma [HackTheBox](https://app.hackthebox.eu/) de dificultad media.

## Enumeración

Para la fase de enumeración, lo primero será realizar un escáner con nmap para identificar los puertos abiertos.

- ```nmap -p- -sS --min-rate 5000 -n -v 10.10.10.169 -oG allports.gnmap```

```bash
PORT      STATE SERVICE
53/tcp    open  domain
88/tcp    open  kerberos-sec
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
389/tcp   open  ldap
445/tcp   open  microsoft-ds
464/tcp   open  kpasswd5
593/tcp   open  http-rpc-epmap
636/tcp   open  ldapssl
3268/tcp  open  globalcatLDAP
3269/tcp  open  globalcatLDAPssl
5985/tcp  open  wsman
9389/tcp  open  adws
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49671/tcp open  unknown
49678/tcp open  unknown
49679/tcp open  unknown
49686/tcp open  unknown
49713/tcp open  unknown
49743/tcp open  unknown
```

Posteriormente, lo ideal es hacer una detección de versiones y servicios que corren en los puertos encontrados.

- ```nmap -sC -sV -p53,88,135,139,389,445,464,593,636,3268,3269,5985,9389,47001,49664,49665,49666,49667,49671,49678,49679,49686,49713,49743 10.10.10.169 -oN ports.nmap```


```bash
Nmap scan report for 10.10.10.169
Host is up (0.42s latency).

PORT      STATE  SERVICE      VERSION
53/tcp    open   domain       Simple DNS Plus
88/tcp    open   kerberos-sec Microsoft Windows Kerberos (server time: 2021-04-24 21:07:13Z)
135/tcp   open   msrpc        Microsoft Windows RPC
139/tcp   open   netbios-ssn  Microsoft Windows netbios-ssn
389/tcp   open   ldap         Microsoft Windows Active Directory LDAP (Domain: megabank.local, Site: Default-First-Site-Name)
445/tcp   open   microsoft-ds Windows Server 2016 Standard 14393 microsoft-ds (workgroup: MEGABANK)
464/tcp   open   kpasswd5?
593/tcp   open   ncacn_http   Microsoft Windows RPC over HTTP 1.0
636/tcp   open   tcpwrapped
3268/tcp  open   ldap         Microsoft Windows Active Directory LDAP (Domain: megabank.local, Site: Default-First-Site-Name)
3269/tcp  open   tcpwrapped
5985/tcp  open   http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
9389/tcp  open   mc-nmf       .NET Message Framing
47001/tcp open   http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
49664/tcp open   msrpc        Microsoft Windows RPC
49665/tcp open   msrpc        Microsoft Windows RPC
49666/tcp open   msrpc        Microsoft Windows RPC
49667/tcp open   msrpc        Microsoft Windows RPC
49671/tcp open   msrpc        Microsoft Windows RPC
49678/tcp open   ncacn_http   Microsoft Windows RPC over HTTP 1.0
49679/tcp open   msrpc        Microsoft Windows RPC
49686/tcp open   msrpc        Microsoft Windows RPC
49713/tcp open   msrpc        Microsoft Windows RPC
49743/tcp closed unknown
Service Info: Host: RESOLUTE; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 2h27m00s, deviation: 4h02m31s, median: 6m59s
| smb-os-discovery: 
|   OS: Windows Server 2016 Standard 14393 (Windows Server 2016 Standard 6.3)
|   Computer name: Resolute
|   NetBIOS computer name: RESOLUTE\x00
|   Domain name: megabank.local
|   Forest name: megabank.local
|   FQDN: Resolute.megabank.local
|_  System time: 2021-04-24T14:08:08-07:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: required
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2021-04-24T21:08:09
|_  start_date: 2021-04-24T20:49:12
```


## Acceso inicial




## Escalada de privilegios

