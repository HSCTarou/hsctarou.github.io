---
layout: single
title:  "HTB Blackhole Challenge Writeup"
date:   2020-07-26 12:20:55 -0400
classes: wide
categories: HTB
---

En esta ocasión estaremos realizando el Challenge **Blackhole** de la plataforma [HackTheBox](https://hackthebox.eu) que pertenece a la categoria MISC. A continuación el detalle desde la plataforma:

![Challenge info](/images/HTB/Blackhole/00-challenge-info.png "Challenge info"){: .align-center}


Para empezar obtenemos un archivo llamado Blackhole.zip, el cual al descomprimirlo nos generará el archivo ```hawkings```.

![Blackhole.zip files](/images/HTB/Blackhole/01-files.png "Blackhole.zip files"){: .align-center}

Lo primero será visualizar la imagen para verificar si existe algún tipo de información útil en su interior.

![Stephen Hawking](/images/HTB/Blackhole/02-hawking.png "Stephen Hawking"){: .align-center}

Como se puede apreciar, es una imagen con la fotografía **Stephen Hawking** y la frase ***"Life would be tragic if it weren't funny."***. En primera instancia pensé que se podía tratar de una pista para conseguir la flag, por lo que busqué en internet para después de un tiempo darme cuenta de que la resolución no iba por ese camino.

Ya que verificamos que la imagen no contiene mayor información relevante, toca revisar el fichero. Lo primero es ejecutar el comando "file" para ver con que tipo de archivo estamos tratando.


![File info](/images/HTB/Blackhole/03-rename-file.png "File info"){: .align-center}

Vemos que se trata de un archivo **JPG** pero éste no viene con la extensión, por lo que renombramos el archivo para poder aplicar la utilidad ```Stegcracker``` sobre él. Esto para ver si contiene algún archivo oculto en su interior. Haciendo uso del diccionario ***rockyou.txt*** le aplicamos fuerza bruta.

{% highlight bash %}
stegcracker hawking.jpg /usr/share/wordlists/rockyou.txt
{% endhighlight %}

![Stegcracker](/images/HTB/Blackhole/04-stegcracker.png "Stegcracker"){: .align-center}

Al cabo de unos minutos obtenemos un match con la contraseña ***hawkingez*** y como resultado nos genera el archivo ```hawking.jpg.out```. Le aplicamos un ```cat``` y vemos una cadena de caracteres que parecen estar codificados en **base64**. 

Luego de realizar dos decodificaciones en base64, obtendremos el mensaje que se visualiza a continuación, el cual tiene un formato similar al de la **flag** que buscamos:

![Decode](/images/HTB/Blackhole/05-decode1.png "Decode"){: .align-center}

A simple vista el mensaje parece estar codificado en cifrado césar o **ROT13**, por lo que con la ayuda de [CyberChef](https://gchq.github.io/CyberChef/) luego de unos intentos, obtendremos nuestro mensaje decodificado junto con la **flag**.

![Decode 2](/images/HTB/Blackhole/06-decode2.png "Decode 2"){: .align-center}

Flag: ```HTB{N3veR_l3T_tH3_b4sTaRd5_G3t_Y0u_d0wN}```.