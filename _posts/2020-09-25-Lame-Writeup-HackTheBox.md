---
layout: single
title:  "Lame Writeup [ES] (in progress) - HackTheBox"
date:   2020-09-24 03:50:00 -0400
classes: wide
categories: HTB
tags:
 - OSCP
---

En esta ocasión estaré trabajando con la máquina **Lame** de **HackTheBox** como práctica para el OSCP Path. Esta máquina es una de las más sencillas de toda la plataforma. A continuación la veremos en detalle.


## Box info

![Machine Info](/images/HTB/Lame/00-info.png "Machine Info"){: .align-center}



## Enumeration

Como siempre lo primero será lanzar un nmap contra la máquina. Inicialmente utilizaremos este comando para obtener en escaner de todos los puertos que se encuentren abiertos:

```bash
nmap -p- --open -T4 -n 10.10.10.3 -oG allPorts.gnmap

Starting Nmap 7.80 ( https://nmap.org ) at 2020-09-25 04:14 -03
Nmap scan report for 10.10.10.3
Host is up (0.20s latency).
Not shown: 65530 filtered ports
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
3632/tcp open  distccd
```

Posteriormente realizaremos un scan específicos a los puertos abiertos, esta vez identificando servicios y versiones que están corriendo en la máquina.


```bash
nmap -sC -sV -n -p21,22,139,445,3632 10.10.10.3 -oX targeted.xml -oN targeted.nmap

Starting Nmap 7.80 ( https://nmap.org ) at 2020-09-25 04:18 -03
Nmap scan report for 10.10.10.3
Host is up (0.23s latency).

PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to 10.10.14.2
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey:
|   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
|_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
3632/tcp open  distccd     distccd v1 ((GNU) 4.2.4 (Ubuntu 4.2.4-1ubuntu4))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

A simple vista ya detectamos el puerto 21 abierto (FTP) y nmap nos identifica que dicho servicio tiene habilitado el login anónimo. Para verificarlo simplemente realizamos:

```go
ftp 10.10.10.3
Connected to 10.10.10.3.
220 (vsFTPd 2.3.4)
Name (10.10.10.3:hsct): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.

ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
226 Directory send OK.
```

Ingresamos al FTP pero vemos que no posee archivos ni directorios visibles que nos puedan ser de utilidad.

Continuando, también podemos observar que el puerto smb 445 se encuentra abierto, lo que podemos hacer es lanzar ```CrackMapExec``` sobre el servicio para ver que información nos muestra.

![SMB](/images/HTB/Lame/04-smb.png "SMB"){: .align-center}

Se verifica que el puerto está abierto con SMB v1. Ahora, revisando con smbmap se obtiene lo siguiente.

![SMB](/images/HTB/Lame/05-smb.png "SMB"){: .align-center}

Se detecta que el directorio compartido ```tmp``` posee permisos de escritura/lectura y se puede acceder sin problemas con un usuario anónimo.

![SMB](/images/HTB/Lame/06-smb.png "SMB"){: .align-center}

Al identificar que esta máquina está bastante desactualizada, lo habitual sería verificar las versiones de los servicios que está corriendo y si existe alguna vulnerabilidad que se pueda explotar. Para ello se hace uso de la utilidad searchsploit para buscar posibles vectores de ataque.

