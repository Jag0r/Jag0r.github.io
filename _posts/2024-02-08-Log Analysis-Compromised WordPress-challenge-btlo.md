---
title: Log Analysis – Compromised WordPress-btlo
date: 2024-02-08 14:10:00 +0800
categories: [Btlo, Challenge]
tags: [Incident Response]
render_with_liquid: false
img_path: Ghimg/btlo/Log%20Analysis%20Compromised%20WordPress/
---

## Escenario

Uno de nuestros sitios de WordPress se ha visto comprometido, pero actualmente no estamos seguros de cómo. La hipótesis principal es que un complemento instalado era vulnerable a una vulnerabilidad de ejecución remota de código que le daba a un atacante acceso al sistema operativo subyacente del servidor.

### Used tools

- **Grep**: _Se utiliza para buscar patrones en archivos de texto. Puedes buscar palabras o expresiones regulares en un archivo o incluso en la salida de otro comando._
- **Sort**: _Ordena las líneas de un archivo de texto. Puedes especificar diferentes opciones para ordenar alfabéticamente, numéricamente o basado en campos específicos_ 
- **Uniq**: _Se utiliza para mostrar líneas únicas en un archivo. Puede ser útil para eliminar duplicados o encontrar líneas repetidas._ 



## Desafio

**_Identifique el URI del panel de inicio de sesión de administración al que el atacante obtuvo acceso_**

Al usar **WordPress** sabemos que la pagina de inicio de sesion de administracion `/wp-login.php`, asi que buscamos dentro del registro

`cat access.log | grep wp-login.php | cut -d '"' -f2 | sort | uniq` 

![20240213143316.png](20240213143316_e8x0i7)


**_¿Puedes encontrar dos herramientas que usó el atacante?_**

 `cat access.log | cut -d '"' -f6 | sort | uniq`      

![20240213144303.png](20240213144303_blaw8r)



![20240213144422.png](20240213144422_vy1psz)


**_El atacante intentó explotar una vulnerabilidad en 'Contact Form 7'. ¿A qué CVE era vulnerable el plugin?_**

`cat access.log | grep contact-form-7` para buscar la version y luego hacemos una busqueda para ver cual es el cve

![Pasted image 20240129221855.png](wp-ans3.1)

![Pasted image 20240129222142.png](wp-ans3.2)


**_¿Qué plugin fue explotado para obtener acceso?_**

_ContactForm7 versión 5.3.1 y anteriores no desinfecta adecuadamente los nombres de archivos cargados para evitar la carga arbitraria de archivos que puede llevar a la toma total del servidor en el peor de los casos._

_Esto sucede en la función `wpcf7_antiscript_file_name`, que no logra desinfectar el nombre de archivo proporcionado si termina con cualquier carácter especial Unicode que vaya desde U+0000 (null) hasta U+001F (us)._

_La función compara tanto el nombre del archivo como la extensión del archivo con una expresión regular de exclusión. Agregar cualquier carácter especial Unicode a la extensión del archivo da como resultado una omisión completa de esta verificación (ya que la expresión regular no coincide), lo que lleva a la carga de archivos sin restricciones._

![Pasted image 20240129224342.png](wp-ans4)

**_¿Cuál es el nombre del archivo PHP web shell?_**

r34k.php

**_¿Cuál fue el código de respuesta HTTP proporcionado cuando se accedió al shell web por última vez?_**

404