---
title: SOC Alfa 1-btlo
date: 2023-12-20 14:10:00 +0800
categories: [Btlo, Investigations]
tags: [Security Operations]
render_with_liquid: false
img_path: /Ghimg/btlo/Investigations/SOC%20Alfa%201/img/
---

![[Pasted image 20231220134119.png]](Pasted_image_20231220134119_snjgm0)


## Escenario
  
Usted es un analista de SOC y el manejo de las alertas dentro de su SIEM, ELK, es parte de las tareas diarias. ¡Responda a las siguientes preguntas analizando las alertas proporcionadas en README.txt!  
  
![[Pasted image 20231220182735.png]](Pasted_image_20231220182735_a2mn6f)


### Used tools

- ELK 
- Log Analysis 
- Network Analysis 
- T1569.002


## Presentación de la investigación

**_Alerta 1 (1/2): ¿Cuál es el cmdlet que se usa para la descarga?_** 

![[Pasted image 20231220184436.png]](Pasted_image_20231220184436_qogmr6)



**_Alerta 1 (2/2) - ¿Cuál es la URL completa desde la que se descarga el archivo?_** 

`https://raw.githubusercontent.com/nerrorsec/SBT-SOC/main/MSWorker.exe

**_Alerta 2 (1/1): ¿cuál es el nombre del EXE sospechoso que se agrega para la persistencia?_** 

![[Pasted image 20231220184838.png]](Pasted_image_20231220184838_v1o4nb.png)



**_Alerta 3 (1/2) - ¿Cuál es el nombre del archivo ejecutable sospechoso involucrado?_**

![[Pasted image 20231220185242.png]](Pasted_image_20231220185242_l0vdzw)

Service.exe

**_Alerta 3 (2/2) - ¿Cuál es el nombre de la ruta de acceso de la clave?_**

service

**_Alerta 4 (1/2) - ¿Cuál es el nombre de la tarea?_** 

![[Pasted image 20231220185749.png]](Pasted_image_20231220185749_aqo8hq)

My Task

**_Alerta 4 (2/2) - ¿Cuál es la ruta completa del programa?_**

`C:\Program Files\GameLoaderGen\gen.bat


