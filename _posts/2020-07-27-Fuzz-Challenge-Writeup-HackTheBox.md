---
layout: single
title:  "Fuzz Challenge Writeup [ES] - HackTheBox"
date:   2020-07-27 20:00:00 -0400
classes: wide
categories: HTB
tags:
 - CTF
 - Web
---

![Challenge Info](/images/HTB/Fuzz/01-web.png "Challenge Info"){: .align-center}

Como primer paso, accederemos a la dirección web proporcionada para realizar un reconocimiento y verificar si es posible extraer información relevante del sitio.

Nos encontramos con la siguiente página web.

![Sitio web](/images/HTB/Fuzz/02-web.png "Sitio web"){: .align-center}

Haciendo uso de la utilidad [dirsearch](https://github.com/maurosoria/dirsearch), ejecutaremos un fuzzing de los directorios en la dirección ```http://docker.hackthebox.eu:30923/```


```bash
python3 dirsearch.py -u http://docker.hackthebox.eu:30923 -e "html,php,txt"
```

![Directory Fuzzing](/images/HTB/Fuzz/03-fuzzing1.png "Directory Fuzzing"){: .align-center}