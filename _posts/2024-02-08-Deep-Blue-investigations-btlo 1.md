---
title: Deep Blue-btlo
date: 2023-12-26 14:10:00 +0800
categories: [Btlo, Investigations]
tags: [Incident Response]
render_with_liquid: false
img_path: /Ghimg/btlo/Investigations/Deep%20Blue/img/
---

![Pasted image 20231223120931.png](Pasted_image_20231223120931_wtpj6j.png)

## Escenario

Una estación de trabajo Windows fue comprometida recientemente, y la evidencia sugiere que fue un ataque contra RDP orientado a Internet, entonces Meterpreter fue desplegado para llevar a cabo 'Acciones sobre Objetivos'. ¿Puede verificar estos hallazgos?

Se le han proporcionado las exportaciones de registro Security.evtx y System.evtx del sistema comprometido - debe analizar estos, NO los registros de Windows generados por la máquina de laboratorio (cuando utilice DeepBlueCLI asegúrese de que está proporcionando la ruta a estos archivos, almacenados dentro de \Desktop\Investigation\.

Material de lectura:https://github.com/sans-blue-team/DeepBlueCLI 

### Used tools
DeepBlueCLI 
PowerShell 
Event Viewer 

T1133 
T1078.003 
T1136.001 
T1543.003

## Presentación de la investigación

**_Con DeepBlueCLI, investigue el registro de seguridad recuperado (Security.evtx). ¿Qué cuenta de usuario ejecutó GoogleUpdate.exe?_** 

![Pasted image 20231226190231.png](Pasted_image_20231226190231_u0hwpe)



**_Con DeepBlueCLI, investigue el registro Security.evtx recuperado. ¿En qué momento es probable que haya evidencia de actividad de Meterpreter?_** _(4 puntos)_

![Pasted image 20231226190438.png](Pasted_image_20231226190438_osdza4)

**_Con DeepBlueCLI, investigue el registro System.evtx recuperado. ¿Cuál es el nombre del servicio sospechoso creado?_** 

![Pasted image 20231226190911.png](Pasted_image_20231226190911_akiqpb)


**_Investigue el registro de Security.evtx en el Visor de eventos. Se está auditando la creación de procesos (identificador de evento 4688). Identifique el ejecutable malicioso descargado que se utilizó para obtener un shell inverso de Meterpreter, entre las 10:30 y las 10:50 a. m. del 10 de abril de 2021._** _(4 puntos)_

![[Pasted image 20231226192358.png]](Pasted_image_20231226192358_vfckgm)


**_También se cree que se creó una cuenta adicional para garantizar la persistencia entre las 11:25 a. m. y las 11:40 a. m. del 10 de abril de 2021. ¿Cuál fue la línea de comandos utilizada para crear esta cuenta? (¡Asegúrate de haber encontrado la cuenta correcta!)_** _(4 puntos)_

![[Pasted image 20231226193113.png]](Pasted_image_20231226193113_wbk5eq)

**_¿A qué dos grupos locales se agregó esta nueva cuenta?_** _(4 puntos)_

![[Pasted image 20231226193729.png]](Pasted_image_20231226193729_awxtfz)