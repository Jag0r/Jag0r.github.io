---
title: Paranoid-Btlo
date: 2024-02-08 14:10:00 +0800
categories: [Btlo, Challenge]
tags: [Incident Response]
render_with_liquid: false
img_path: Ghimg/btlo/challenge/Paranoid/img
---


## Escenario

Yo no soy paranoico, tú sí.

### Used tools

- **AUReport**: es una **herramienta de línea de comandos** utilizada para **crear informes resumidos** a partir de los archivos de registro almacenados en `/var/log/audit/`. también acepta datos de registro sin procesar desde la entrada estándar. 




## Desafío

Usamos el siguiente comando para ver un resumen del archivo `aureport --summary -if /ruta/al/archivo.log`


![Pasted image 20240128211217.png](Pasted_image_20240128211217_f2unov)

Vemos algo interesante hay 87 inicios de sesion fallidos.


**_#1) ¿Qué cuenta fue comprometida?_**

Usamos el comando `-au` Authentication report `aureport -au -if audit.log` observamos que lo multiples intentos se hicieron contra el host **btlo**

![Pasted image 20240128211449.png](Pasted_image_20240128211449_rpwcxn)


**_#2) ¿Qué tipo de ataque se utilizó para obtener acceso inicial?_**

Estos multiples intentos de autenticacion coicide con un patron de ataque de fuerza bruta 

![Pasted image 20240128212149.png](Pasted_image_20240128212149_f83qos)


**_#3) ¿Cuál es la dirección IP del atacante?_**

192.168.4.155

**_#4) ¿Qué herramienta se utilizó para realizar la enumeración del sistema?_**

Usamos `aureport --tty -if audit.log` para ver las pulsaciones de teclas que se realizaron en el terminal. vemos que utilizo **linpeas** para la enumeracion.

**linpeas** es una herramienta de enumeración y recopilación de información en entornos Linux 

![Pasted image 20240128212657.png](Pasted_image_20240128212657_fz38zv)


**_#5) ¿Cuál es el nombre del binario y el pid utilizados para obtener raíz?_**

observamos que usa `lsb_release -a` para ver la version del sistema luego descarga un archivo `evil.tar.gz` y  usa `make` para compilar

usamos `aureport -p -if audit.log | grep "evil"` para enumerar esos procesos

![Pasted image 20240128214004.png](Pasted_image_20240128214004_bjnjw7)


**_#6) ¿Qué CVE se aprovechó para obtener acceso root? (¡Investiga!)_**

![Pasted image 20240128215131.png](Pasted_image_20240128215131_vpig7y)


**_#7) ¿Qué tipo de vulnerabilidad es esta?_**

`heap-based buffer overflow` es un tipo de desbordamiento de búfer que ocurre en la zona de memoria heap. Se produce cuando se accede fuera de los límites de un búfer que fue asignado en la memoria heap.


**_#8) ¿Qué archivo se exfiltró una vez que se obtuvo la raíz?_**

vemos que extrajo el achivo `etc/shadow`





