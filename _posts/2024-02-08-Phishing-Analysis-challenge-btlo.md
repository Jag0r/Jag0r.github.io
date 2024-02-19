---
title: Phishing Analysis-btlo
date: 2024-02-08 14:10:00 +0800
categories: [Btlo, Challenge]
tags: [writing]
render_with_liquid: false
img_path: /Ghimg/btlo/challenge/Phishing%20Analysis/img/
---

## Escenario

Un usuario ha recibido un correo electrónico de suplantación de identidad (phishing) y lo ha reenviado al SOC. ¿Puede investigar el correo electrónico y el archivo adjunto para recopilar artefactos útiles?

### Used tools 
- **Mozilla Thunderbird**:Thunderbird es un cliente de correo electrónico, noticias, chat y calendario código abierto. Está diseñado para hacer el correo más fácil y opera en múltiples plataformas.  

- **URL2PNG**:URL2PNG es una aplicación web que permite capturar instantáneamente imágenes de cualquier página web

- **WHOis**:es un protocolo TCP basado en petición/respuesta que se utiliza para efectuar consultas en una base de datos. Esta base de datos permite determinar el propietario de un nombre de dominio o una dirección IP.

### Resolution summary
- Abrimos el correo con **Mozilla Thunderbird**
- Hacemos un **WHOis** para ver la informacion del dominio
- Usamos **URL2PNG** para ver el contenido de la pagina


## Desafio

**_¿Quién es el destinatario principal de este correo electrónico?_** 

Usamos **Mozilla Thunderbird** y vemos el _destinantario, asunto y fecha_

![Pasted image 20240113214915.png](Pasted_image_20240113214915_zipljl)

**_¿Cuál es el asunto de este correo electrónico?_** 

Undeliverable: Website contact from submission

**_¿Cuál es la fecha y hora en que se envió el correo electrónico? _**

18 March 2021 04:14

**_¿Cual es la IP de origen?_** 

Abrimos el correo con un editor de texto y obseramos la **IP**

![Pasted image 20240113215821.png](Pasted_image_20240113215821_huvzw7)

**_Realice DNS inverso en esta dirección IP, ¿cuál es el host resuelto? (whois.domaintools.com)_**

Al realizar el DNS inverso en _whois.domaintools.com_ obtenemos la informacion del host 

![Pasted image 20240113215909.png](Pasted_image_20240113215909_hqnuhn)

**_¿Cuál es el nombre del archivo adjunto?_** 

![Pasted image 20240113220004.png](Pasted_image_20240113220004_cbdct2)

**_¿Cuál es la URL que se encuentra dentro del archivo adjunto?_** 

![Pasted image 20240113220025.png](Pasted_image_20240113220025_cfwhst)

**_¿En qué servicio está alojada esta página web?_** 

Al observar la direccion vemos que es un servicio **blogspot**


**_Usando URL2PNG, ¿cuál es el texto del encabezado en esta página? (¡No importa si la página ha sido eliminada!)_**

Al verlo en **URL2PNG** vemos que es un blog que ha sido eliminado

![Pasted image 20240113220108.png](Pasted_image_20240113220108_h0btzg)