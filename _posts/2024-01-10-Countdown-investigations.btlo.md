---
title: Countdown-btlo
date: 2023-12-28 14:10:00 +0800
categories: [Btlo, Investigations]
tags: [Digital Forensics]
render_with_liquid: false
img_path: /Ghimg/btlo/Investigations/Countdown/img/
---

![Pasted image 20231223122313.png](Pasted_image_20231223122313_oclm2i.png)

## Used tools

- Autopsy 
- Window File Analyzer 
- WinPrefetchView 
- Jumplist Explorer 
- SQLite DB Browser

## Technique

- T1573


## Escenario

 
La policía de la ciudad de Nueva York recibió información de que una banda de atacantes ha ingresado a la ciudad y planea detonar un artefacto explosivo. Las fuerzas del orden han comenzado a investigar todas las pistas para determinar si esto es cierto o un engaño.  
  
Personas de interés fueron detenidas y otro sospechoso llamado "Zerry" fue detenido mientras los agentes allanaban su casa. Durante la búsqueda, encontraron una computadora portátil, recolectaron la evidencia digital y la enviaron a la división forense digital de la ciudad de Nueva York.  
  
La policía cree que Zerry está directamente asociado con la pandilla y está analizando su dispositivo para descubrir cualquier información sobre el posible ataque.  
  
Descargo de responsabilidad: La historia, todos los nombres, personajes e incidentes retratados en este desafío son ficticios y cualquier relevancia para los eventos del mundo real es completamente una coincidencia.

## Presentación de la investigación

Verifique la imagen de disco. Enviar SectorCount y MD5 _(7 puntos)_

![[Pasted image 20240109223621.png]](Pasted_image_20240109223621_s5kggt)


¿Cuál es la clave de descifrado de la aplicación de mensajería en línea utilizada por Zerry? _(7 puntos)_

![[Pasted image 20240109225027.png]](Pasted_image_20240109225027_jzwvxt)

hacemos una busqueda en google sobre laclave de esta app

[Signal Desktop Leaves Message Decryption Key in Plain Sight (bleepingcomputer.com)](https://www.bleepingcomputer.com/news/security/signal-desktop-leaves-message-decryption-key-in-plain-sight/)


%AppData%\Signal\config.json

![[Pasted image 20240109230632.png]](Pasted_image_20240109230632_n9ibzp)


![[Pasted image 20240109230825.png]](Pasted_image_20240109230825_ibz5aq)




¿Cuál es el número de teléfono registrado y el nombre de perfil de Zerry en la aplicación de mensajería utilizada? _(7 puntos)_

%AppData%\Roaming\Signal\sql\db.sqlite

![[Pasted image 20240109230319.png]](Pasted_image_20240109230319_vldfrn)

usamos SQLiteDatabaseBrowser para abrir db.sqlite ingresamos la clave leemos la coversations  

![[Pasted image 20240109232249.png]](Pasted_image_20240109232249_yrbfax)




¿Cuál es la identificación de correo electrónico que se encuentra en el chat? _(7 puntos)_

![[Pasted image 20240109232937.png]](Pasted_image_20240109232937_iuhli2)



¿Cuál es el nombre del archivo (incluida la extensión) que se recibe como archivo adjunto por correo electrónico? _(7 puntos)_

![[Pasted image 20240109234105.png]](Pasted_image_20240109234105_xxaa5f)




¿Cuál es la fecha y hora del ataque planeado? _(7 puntos)_

exportamos thumbcache_256.db /Users/Zerry/AppData/Local/Microsoft/Windows/Explorer 

![[Pasted image 20240109234630.png]](Pasted_image_20240109234630_ed9mhv)

abrimos con thumbcache_viewer y buscamos la imagen .png

![[Pasted image 20240109235133.png]](Pasted_image_20240109235133_sz2lnu)





¿Cuál es la ubicación GPS de la explosión? El formato es el mismo que se encuentra en la evidencia. [Sugerencia: codificar (XX grados, XX minutos, XX segundos)] _(8 puntos)_



![[Pasted image 20240110000527.png]](Pasted_image_20240110000527_kehwmg)


![[Pasted image 20240110001242.png]](Pasted_image_20240110001242_typhhm)