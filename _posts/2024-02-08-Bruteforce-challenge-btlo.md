---
title: Bruteforce-Btlo
date: 2024-02-08 14:10:00 +0800
categories: [Btlo, Challenge]
tags: [writing]
render_with_liquid: false
img_path: /Ghimg/btlo/challenge/Bruteforce/img/
---

## Escenario

**¿Puede analizar los registros de un intento de ataque de fuerza bruta RDP?**  
  
Uno de nuestros administradores del sistema identificó un gran número de eventos de error de auditoría en el registro de eventos de seguridad de Windows.  
  
¡Hay varias formas diferentes de abordar el análisis de estos registros! Considere las herramientas sugeridas, ¡pero hay muchas otras por ahí!


### *Used tools*

- **PowerShell**: _Es una **interfaz de línea de comandos (CLI)** que permite ejecutar **scripts** y facilita la **configuración, administración y automatización de tareas**.

- **Text Editor** 

- **Windows Event Viewer**: _herramienta que registra y almacena diversos tipos de **registros de eventos**. Estos registros proporcionan información sobre el funcionamiento del sistema, errores, advertencias y otros sucesos relevantes
### Resolution summary

- Usamos powershell para encontrar los patrones en el archivo
- Usamos Windows Event Viewer para ver los detalles del registo
- Hacemos una busqueda **Whois** para ver la informacion de la dirección IP 


## Presentación 

Hay múltiples formas de abordar esto en este caso usaremos PowerShell y el visor de eventos de Windows.
Tenemos 3 archivos. abrimos `BTLO_Bruteforce_Challenge.evtx` en el visor de eventos de Windows

**_Pregunta 1) ¿Cuántos eventos de falla de auditoría hay?_** 

Para ver la cantidad de fallas usamos powershell con el **cmdlet** ```Get-Content``` para obtener el contenido del archivo, ```Select-String``` para encontrar patrones y ```Measure-Object``` para contar en numero de lineas


![ans1](Pasted_image_20240126155251_i7bmak.png)

**_Pregunta 2) ¿Cuál es el nombre de usuario de la cuenta local a la que se dirige?_** 

observamos el **Windows Event Viewer** cuenta con error de inicio de sesion

![ans2](Pasted_image_20240126162800_wcrcjt)


**_Pregunta 3) ¿Cuál es el motivo de la falla relacionada con los registros de fallas de auditoría?_** 

vemos información de error:

![ans3](Pasted_image_20240126163313_cxppdj)


**_Pregunta 4) ¿Cuál es el identificador de evento de Windows asociado con estos errores de inicio de sesión?_**

![ans4](Pasted_image_20240126163442_fy0jcw)


**_Pregunta 5) ¿Cuál es la IP de origen que lleva a cabo este ataque?_** 

![ans5](Pasted_image_20240126163547_xeymix)


**_Pregunta 6) ¿A qué país está asociada esta dirección IP?_** 

Hacemos una búsqueda whois para ver la info de la direccion IP

![ans6](Pasted_image_20240126164133_mfwmnu)


**_Pregunta 7) ¿Cuál es el rango de puertos de origen que utilizó el atacante para realizar estas solicitudes de inicio de sesión?_**

R: 49162-65534
