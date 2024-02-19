---
title: Phishing Analysis 2-btlo
date: 2024-02-08 14:10:00 +0800
categories: [Btlo, Challenge]
tags: [writing]
render_with_liquid: false
img_path: /Ghimg/btlo/challenge/Phishing%20Analysis%202/img/
---

## Escenario

Pon a prueba tus habilidades de análisis de phishing clasificando y recopilando información sobre una campaña de phishing reciente.

### Used tools
- **Mozilla Thunderbird**:Thunderbird es un cliente de correo electrónico, noticias, chat y calendario código abierto. Está diseñado para hacer el correo más fácil y opera en múltiples plataformas. 

- **URL2PNG**:URL2PNG es una aplicación web que permite capturar instantáneamente imágenes de cualquier página web 

- **CyberChef**: es una herramienta web que permite analizar y decodificar datos.

### Resolution summary
- Analizamos el correo con **Thunderbird**
- Usamos **URL2PNG** para inspeccionar la web
- Usamos **CyberChef** para decodificar e inspeccionar la web

## Desafio

**_¿Cuál es la dirección de correo electrónico de envío?_**

Analizamos el correo electronico con **Thunderbird**

![Screenshot_2024-01-17_23_19_36.png](Screenshot_2024-01-17_23_19_36_qo5ahd)

**_¿Cuál es la dirección de correo electrónico del destinatario?_** 

Usamos un editor de texto y observamos el campo **_To, From Subject y date_**

![Pasted image 20240118133916.png](Pasted_image_20240118133916_cabewh)

**_¿Cuál es el asunto del correo electrónico?_**

_Your Account has been locked_

**_¿A qué empresa intenta imitar el atacante?_**

_Amazon_

**_¿Cuál es la fecha y hora en que se envió el correo electrónico? (Copiado de un editor de texto)_**

_Wed, 14 Jul 2021 01:40:32 +0900_

**_¿Cuál es la URL del botón principal de llamada a la acción?_**

Podemos inspecciónar para ver el enlace

![Pasted image 20240118142556.png](Pasted_image_20240118142556_chvftr)

**_Mira la URL usando URL2PNG. ¿Cuál es la primera oración (encabezado) que se muestra en este sitio? (independientemente de si cree que el sitio es malicioso o no)_**

Al copiar la direccion en _URL2PNG_ vemos el encabezado

![Screenshot_2024-01-17_22_00_55.png](Screenshot_2024-01-17_22_00_55_ied3hc)

**_Al observar el contenido del cuerpo principal en un editor de texto, ¿qué esquema de codificación se está utilizando?_** 

Vemos que esta codificado en _base64_

![Pasted image 20240118135118.png](Pasted_image_20240118135118_iprngt)

**_¿Cuál es la URL utilizada para recuperar el logotipo de la empresa en el correo electrónico?_** 

copiamos el contenido _base64_ en **_CyberChef_** y buscamos el campo **_https_**

![Screenshot_2024-01-17_23_02_26.png](Screenshot_2024-01-17_23_02_26_c0rwwl)

**_Por alguna razón desconocida, una de las URL contiene una URL de perfil de Facebook. ¿Cuál es el nombre de usuario (no necesariamente el nombre para mostrar) de esta cuenta, según la URL? _**

buscamos en campo **_facebook_** en la salida en **Cyberchef**

![Screenshot_2024-01-17_23_15_45.png](Screenshot_2024-01-17_23_15_45_xxqttb)