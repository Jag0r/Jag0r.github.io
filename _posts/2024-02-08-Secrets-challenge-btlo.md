---
title: Secrets-Btlo
date: 2024-02-08 14:10:00 +0800
categories: [Btlo, Challenge]
tags: [writing]
render_with_liquid: false
img_path: Ghimg/btlo/challenge/Secrets/img
---

## Escenario

Eres un ingeniero senior de ciberseguridad y durante tu turno, hemos interceptado/notado acciones de alto privilegio de origen desconocido que podrían ser identificadas como maliciosas. Te hemos conseguido el ticket que realizó estas acciones.
Usted es quien creó el secreto de estos tickets. Por favor, arregla esto y envía el ticket de bajo privilegio para que podamos asegurarnos de que mereces esta posición.

Aquí está el ticket:
  
**eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmbGFnIjoiQlRMe180X0V5ZXN9IiwiaWF0Ijo5MDAwMDAwMCwibmFtZSI6IkdyZWF0RXhwIiwiYWRtaW4iOnRydWV9.jbkZHll_W17BOALT95JQ17glHBj9nY-oWhT1uiahtv8**



### Used tools
- Text
- Text

### Resolution summary
- Text
- Text


**_#1) ¿Puedes identificar el nombre del token?_**

Primero decodificamos en base64

![[Pasted image 20231207170226.png]](Pasted_image_20231207170226_guknsm)

**Json web token** permite el intercambio seguro de datos entre dos partes utilizando formato JSON.


**_#2) ¿Cuál es la estructura de este token?_**

Un JWT firmado consta de tres partes, todas codificadas en Base64 y separadas por un punto:

- **Header**: Contiene información sobre el tipo de token y el algoritmo de firma o cifrado utilizado.
- **Payload**: Contiene la información real que se transmitirá a la aplicación.
- **Signature**: Se utiliza para verificar la autenticidad del token.

Abrimos [JWT](https://jwt.io/) para verla estructura

![[Pasted image 20231207170854.png]](Pasted_image_20231207170854_ppbanx)


**_#3) ¿Cuál es la pista que encontraste en este token?_**

Observamos a que la pista es `_4_Eyes`

**_#4) ¿Cuál es el secreto?_**

Usamos Hascat `hashcat json.txt -m 16500 -a 3 ?a?a?a?a` veamos un poco los parametros:

- `-m 16500`: se utiliza para descifrar tokens web JSON (JWT)
- `-a 3`: Para un Ataque de fuerza bruta. 
- `?a?a?a?a`: patrón utilizado en el ataque de fuerza bruta. 

Obtenemos `bT!0`

**_#5) ¿Se puede generar un nuevo ticket de firma verificada con pocos privilegios?_**

Lo generamos cambiando **PAYLOAD:DATA** `"admin": false` y **VERIFY SIGNATURE** `bT!0`

![[Pasted image 20231207211351.png]](Pasted_image_20231207211351_pjdolp)



