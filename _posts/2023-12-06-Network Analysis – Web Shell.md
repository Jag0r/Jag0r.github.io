---
title: Network Analysis – Web Shell-Btlo
date: 2023-12-06 14:10:00 +0800
categories: [Blogging, Tutorial]
tags: [writing] 
render_with_liquid: false
img_path: /Ghimg/btlo/challenge/Network%20Analysis%20%E2%80%93%20Web%20Shell/img/
---

## Scenario

El SOC recibió una alerta en su SIEM de "Local to Local Port Scanning" donde una IP privada interna comenzó a escanear otro sistema interno. ¿Puedes investigar y determinar si esta actividad es maliciosa o no? Se le ha proporcionado un PCAP, investigue utilizando las herramientas que desee.

### Used tools

- **Wireshark:** Es una **herramienta de análisis de red** que te permite **capturar y examinar paquetes de datos** intercambiados a través de **protocolos web**. Su función principal es **investigar y resolver problemas** en las comunicaciones de red. 

### Resolution summary
- Usamos diferentes filtro para analizar el trafico con wireshark 


## Desafio

**_¿Cuál es la IP responsable de realizar la actividad de escaneo de puertos?_**

Usamos el filtro `tcp.flags.syn==1 and tcp.flags.ack=0` para ver si es un escaneo SYN y obenemos la ip **10.251.96.4**

![Pasted image 20231205184410.png](Pasted_image_20231205184410_rk73qc)

**_¿Cuál es el rango de puertos analizado por el host sospechoso?_**

Para ver el trafico de estos dos puntos finales vamos a Conversation settings y vemos el rango **1-1024**

![Pasted image 20231205184709.png](Pasted_image_20231205184709_fujulq)


**_¿Cuál es el tipo de escaneo de puertos que se realiza?_**

Como el primer filtro que usamos determinamos que es un escaneo **TCP SYN**

**_Se utilizaron dos herramientas más para realizar reconocimientos contra puertos abiertos, ¿cuáles fueron?_**

![Pasted image 20231205193822.png](Pasted_image_20231205193822_rmnj31)

Podemos utilizar el filtro `http.request.method` para analizar el tráfico HTTP y filtrar paquetes con los método de solicitud `GET` y `POST`.
observamos que se utilizaron dos herremientas `gobuster 3.0.1` que se usa para reconocimiento web de fuerza bruta y `sqlmap 1.4.7` que se usa principalmente para la detección y explotación de vulnerabilidades de inyección SQL en aplicaciones web

`http.request.method == "GET"`

![Pasted image 20231205194458.png](Pasted_image_20231205194458_cfh0tm)

`http.request.method == "POST"`

**_¿Cuál es el nombre del archivo php a través del cual el atacante cargó un shell web?_**

Al usar el filtro en la pregunta anterior notamos **upload.php` y vemos una archivo llamado `editprofile.php`

![Pasted image 20231205195019.png](Pasted_image_20231205195019_qgwuvg)


**_¿Cuál es el nombre del shell web que subió el atacante?_**

Hacemos una busqueda de **upload.php** y encontramos el nombre del archivo **dbfuntions.php**

![Pasted image 20231205203745.png](Pasted_image_20231205203745_biz5df)


**_¿Cuál es el parámetro utilizado en el shell web para ejecutar comandos?_**

Buscamos este archivo **dbfuntions.php** y vemos que se usa el comando **cmd=id**

![Pasted image 20231205205025.png](Pasted_image_20231205205025_exipdl)

**_¿Cuál es el primer comando ejecutado por el atacante?_**

Se uso primero **id**

**_¿Cuál es el tipo de conexión de shell que obtiene el atacante mediante la ejecución de comandos?_**

Vanos a **Analizar → Seguir → Secuencia TCP** y observamos un **reverse shell**

![Pasted image 20231205205349.png](Pasted_image_20231205205349_nbazgy)


**_¿Cuál es el puerto que utiliza para la conexión shell?_**

Vemos que usa el puerto **4422**

