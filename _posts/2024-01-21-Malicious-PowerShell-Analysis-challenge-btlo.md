---
title: Malicious PowerShell Analysis-btlo
date: 2024-01-21 14:10:00 +0800
categories: [Btlo, Challenge]
tags: [writing]
render_with_liquid: false
img_path: /Ghimg/btlo/challenge/Malicious%20PowerShell%20Analysis/img/
---

## Escenario

Recientemente, las redes de una gran empresa llamada GothamLegend se vieron comprometidas después de que un empleado abriera un correo electrónico de phishing que contenía malware. Los daños causados ​​fueron críticos y provocaron perturbaciones en todo el negocio. GothamLegend tuvo que comunicarse con un equipo externo de respuesta a incidentes para ayudar con la investigación. Eres miembro del equipo de IR; todo lo que tienes es un script Powershell codificado. ¿Puedes decodificarlo e identificar qué malware es responsable de este ataque?  
  
Material de lectura:  
[Enlace 1](https://malware.news/t/deobfuscating-powershell-putting-the-toothpaste-back-in-the-tube/23509)

### Used tools
- Editor de texto 
- **CyberChef**:

### Resolution summary
- Text
- Text

## Desafió


![Pasted image 20240121113311.png](Pasted_image_20240121113311_altaot)

En el script observamos `powershell -w hidden -ENCOD`. `hidden` se utiliza para ejecutar el script sin mostrar una ventana. El operador `-ENCOD` se utiliza para especificar el tipo de codificación de caracteres que se utilizará para el archivo de script, en este caso base64

utilizamos **CyberChef** para decodificar en base64 y vemos un código ofuscado 

![Screenshot_2024-01-20_20_21_52.png](Screenshot_2024-01-20_20_21_52_ie3wcr)

usamos **Removed null Byte** y **Generic Code Beauty** para ayudarnos un poco

![Screenshot_2024-01-20_20_51_15.png](Screenshot_2024-01-20_20_51_15_p4beph)

**_¿Qué protocolo de seguridad se utiliza para la comunicación con un dominio malicioso?_**

![Pasted image 20240121124309.png](Pasted_image_20240121124309_n94n7b)

podemos observar que hay una variable llamada `mbu` con el valor **sEcuRITYproTocol=Tls12**

**_¿Qué directorio crea el PowerShell ofuscado? (A partir de `\HOME\`)_**

![Pasted image 20240121124433.png](Pasted_image_20240121124433_m34myz)

nos ayudamos de **PowerShell**

![Pasted image 20240121130801.png](Pasted_image_20240121130801_ygbfmd)

**_¿Qué archivo se está descargando (nombre completo)?_**

la variable `$imd1yck` que hace referencia al directorio creado se concatena con un  archivo **dll** nombrado en la variable `$swrp6tc`

![Pasted image 20240121132929.png](Pasted_image_20240121132929_l18woc)

![Pasted image 20240121133039.png](Pasted_image_20240121133039_umzf5x)

**_¿Qué se utiliza para ejecutar el archivo descargado?_**

vemos que hay un bucle foreach que intera atravez de una serie de urls declaradas en `$b9fhbyv` y  usa las bibleoteca `rundll32` para ejecutar el archivo `a69s.dll` 

![Pasted image 20240121134628.png](Pasted_image_20240121134628_qxlejl)

**_¿Cuál es el nombre de dominio de la URI que termina en '/6F2gd/'_**

en la variable `$b9fhbyv` se encuentran ofuscados una serie de urls

![Pasted image 20240121135336.png](Pasted_image_20240121135336_kv4zbb)

wm.mcdevelop.net

**_Según el análisis del código ofuscado, ¿cuál es el nombre del malware?_**

con esta url hacemos una busqueda en [URLhaus Malware URL exchange](https://urlhaus.abuse.ch/) 

![Pasted image 20240121140749.png](Pasted_image_20240121140749_jpnhjf)

