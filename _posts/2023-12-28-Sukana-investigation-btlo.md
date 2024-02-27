---
title: Sukana-btlo
date: 2023-12-28 14:10:00 +0800
categories: [Btlo, Investigations]
tags: [Incident Response]
render_with_liquid: false
img_path: /Ghimg/btlo/Investigations/Sukana/img/
---
![Pasted image 20231223120551.png](Pasted_image_20231223120551_rcnlso)

## Used tools
- Thunderbird
- Cisco Talos 
- Volatility 
- Autopy 
- Wireshark 
- Timeline Explorer 
- CyberChef 
- MFTECmd

## Escenario

Desi Sukana es una aspirante a analista de DFIR. Se trata de profesionales que recopilan e investigan grandes cantidades de datos para llenar los vacíos de información sobre los ataques cibernéticos. Despertó este interés después de presenciar el fallecimiento de su padre en un trágico accidente. Su padre, Drake Sukana, fue víctima de una violación de datos que comprometió su información personal, incluido el salario, la ubicación, el estado civil, etc. El atacante utilizó esa información para enviar a los ladrones a su domicilio en Estados Unidos. Defendió fielmente a su familia, pero no pudo sobrevivir a las heridas. Después del funeral, la Sra. Sukana (la madre de Desi) lo llevó y se mudó a Sydney, Australia, su país de origen. Impulsado por el fallecimiento de su padre y su extraño entorno, Desi se esforzó rigurosamente por sus clases universitarias y sus estudios independientes no solo para adquirir las habilidades necesarias para resolver el asesinato de su padre, sino también para encontrar un empleo remunerado.  
  
El Sr. Sukana era el sostén de la familia, mientras que la Sra. Sukana era el ama de casa. El pago del seguro de vida de su muerte proporcionó a Desi y a su madre vivir 4 años sin tener trabajo, ese mismo pago termina en dos meses. La Sra. Sukana no tiene habilidades laborales en el mercado para pagar el alto alquiler en Bellevue Hill. Está apostando por Desi para conseguir un trabajo en el campo de la ciberseguridad, concretamente en el DFIR.  
  
Desi actualmente tiene una Licenciatura en Ciencias en Informática Forense, GHFI y GCFA. Dirige un Discord y un podcast de DFIR y es anfitrión de CTF. A pesar de este portafolio asesino, está luchando por entrar en el campo de la ciberseguridad como recién graduado. Todavía lidia con la depresión por el fallecimiento de su padre hace 4 años. Tiene dos perros de servicio llamados Moxie (un amante humano) y Waffle (un ladrador salvaje) para apoyarse. En su reciente paseo con el perro, se encontró con la oportunidad de su vida.  
  
Conoció a Kurt Hansen en un parque local para perros. Kurt es el director ejecutivo de Tesserent, la empresa de ciberseguridad que cotiza en bolsa más grande de Australia. Moxie y Waffle estaban haciendo un estilo libre canino que reunió a una multitud de público, especialmente a Kurt. Desi, conociendo su situación dentro del país, aprovechó la oportunidad para venderse y explicar su interés en el DFIR. Kurt quedó impresionado con su experiencia y pasó su información a su departamento de ciberseguridad.  
  
Una semana después, Desi tuvo una entrevista con el equipo de DFIR en Tesserent. Salió muy bien. Llegó a las etapas finales después de algunas evaluaciones de comportamiento y una llamada de presentación con el equipo. Su ronda final consistió en una evaluación en línea (OA). Se le ha proporcionado la salida KAPE y un volcado de memoria de una máquina Windows infectada. Se proporcionó un contexto adicional en el OA, como la conversación por correo electrónico con la víctima y un informe de malware. Si Desi aprueba este OA, se le presentará un puesto de analista de DFIR con un salario inicial de $ 120,000. Esto le permitirá pagar el alquiler en Bellevue Hill, recibir más tratamiento para su depresión y cuidar de su madre. ¿Pasará el OA de 19 preguntas, depende de ti? Tienes 24 horas, Desi. ¡Buena suerte!

## Presentación de la investigación

P1) ¿Cuál es el valor hash SHA256 para el archivo de malware? (Formato: SHA256) _(1 puntos)_

![[Pasted image 20231227193319.png]](Pasted_image_20231227193319_htphgr)

![[Pasted image 20231227194013.png]](Pasted_image_20231227194013_a9plyq)


P2) ¿Cuál es el tamaño del archivo del malware en bytes? (Formato: XXXXXX) _(1 puntos)_

![[Pasted image 20231227194324.png]](Pasted_image_20231227194324_zxvofb)

445485

P3) Utilizando Cisco Talos, ¿cuál es el "Nombre de detección de terminales seguros de Cisco" para el malware dado? (Formato: Nombre) _(1 puntos)_

![[Pasted image 20231227194529.png]](Pasted_image_20231227194529_hwzxmo)

W32.Auto:a879d2.in03.Talos

P4) Utilizando Cisco Talos, ¿cuál es la reputación del archivo del malware dado? (Formato: Cadena) _(1 puntos)_

Malicious

P5) Con Windows Defender habilitado, inicie el malware. ¿Cuál es el nombre de la amenaza según Microsoft Defender Antivirus? (Formato: Nombre) _(1 puntos)_

![[Pasted image 20231227195009.png]](Pasted_image_20231227195009_bq1seu)

VirTool:Win32/PoshC2.G

P6) ¿En qué lenguaje de scripting está escrito principalmente este C2 Framework? (Formato: Idioma) _(1 puntos)_

![[Pasted image 20231227195239.png]](Pasted_image_20231227195239_v50rbt)

python

P7) ¿Cuál era la dirección de correo electrónico de envío en cuestión? (Formato: `mailbox@domain.tld) _(1 puntos)_

![[Pasted image 20231227195544.png]](Pasted_image_20231227195544_tnbxt7)

`secretsociety2023@protonmail.com

P8) ¿Cuál es el nombre del asunto del correo electrónico? (Formato: Asunto) _(1 puntos)_

TurnOffAV&Run

P9) Utilice CyberChef. Después de cargar el contenido Base64 del correo electrónico en CyberChef, ¿cuál es la salida sin colmillos del href? (Formato: hxxps[://]domain[.] tld/) _(1 puntos)_

![[Pasted image 20231227201820.png]](Pasted_image_20231227195544_tnbxt7)

https[://]proton[.]me/


P10) Un volcado de memoria es una instantánea de la memoria de un equipo que contiene datos sobre cualquier proceso en ejecución en el momento en que se realizó la captura. ¿Cuál es el tamaño, en GB, del volcado de memoria de la máquina Windows infectada? Redondear a la centésima más cercana (Formato: X.XX) _(1 puntos)_

![[Pasted image 20231227202154.png]](Pasted_image_20231227202154_xas7dc)

5.37

P11) Utilizar la volatily. Mirando la conexión de red del volcado de memoria, ¿cuál es el ISP para la dirección extranjera frecuente que termina en .181? (Formato: ISP) _(1 puntos)_

![[Pasted image 20231227203707.png]](Pasted_image_20231227203707_chu5nh)

con la ip hacemos una busqueda whois
 
![[Pasted image 20231227203919.png]](Pasted_image_20231227203919_sxm1n0)

P12) Sobre el tema de la volatily, ¿qué tipo de evidencia digital analiza desde las computadoras? Hay que tener en cuenta, esta memoria volátil es muy común dentro de los ordenadores (Formato: XXX) _(1 puntos)_

Volatily analiza volcado de memoria RAM

RAM

P13) Utilice Wireshark. ¿Cuál es el puerto de destino para el IOC de red en el informe de análisis de archivos de Intezer? (Formato: Puerto) _(1 puntos)_

revisar el informe Intezer Report - Malware

![[Pasted image 20231227203350.png]](Pasted_image_20231227203350_fywzji)

hacemos una busqude en wireshark

![[Pasted image 20231227204552.png]](Pasted_image_20231227204552_tvmpsf)

443

P14) De acuerdo con el informe de análisis de archivos de Intezer, ¿cuál es el ID de MITRE y la gravedad de los primeros TTP? (Formato: TXXXX, Gravedad) _(1 puntos)_

![[Pasted image 20231227211513.png]](Pasted_image_20231227211513_qod7iy)

Enviar

P15) Utilice Timeline Explorer. Echemos un vistazo al archivo CSV de muestra relacionado que obtuvimos de Intezer. Se trata de un ejemplo de archivo adicional que se sabe que está relacionado con el ejemplo principal. ¿Cuándo se vio por primera vez este malware genérico? (Formato: XXX, XX Mes AAAA HH:MM:SS XXX)) _(1 puntos)_

![[Pasted image 20231227212518.png]](Pasted_image_20231227212518_zoss4l)

FRI, 08 May 2020 02:39:58 GMT

P16) Usando Virus Total, el malware está claramente relacionado con la familia de troyanos. Un adversario puede confiar en que un usuario abra este archivo malicioso para obtener la ejecución. ¿Cuál es el ID de MITRE que corresponde a esta táctica? (Formato: TXXXX.xxx) _(2 puntos)_

![[Pasted image 20231227212938.png]](Pasted_image_20231227212938_fnbv35)

T1204.002

P17) Utilice Timeline Explorer (TE). Después de usar MFTECmd, el analizador MFT de línea de comandos, para cargar el $MFT CSV en TE. Localice la marca de tiempo de creación del nombre de archivo (FN) (0x10) para el archivo de malware (formato: AAAA-MM-DD HH:MM:SS) _(2 puntos)_

tranformar el mft a  csv

![[Pasted image 20231227214532.png]](Pasted_image_20231227214532_rmbvrc)

luego usamos TIMELINE EXPLORER

![[Pasted image 20231227215019.png]](Pasted_image_20231227215019_stxcsw)

2023-01-31 09:33:41


Pregunta 18) $Boot. Como se puede adivinar fácilmente, este archivo está relacionado con el proceso de arranque y contiene el sector de arranque NTFS. Utilizando el mismo proceso anterior, encuentre el tamaño del clúster (Formato: XXXX) _(2 puntos)_

![[Pasted image 20231227215256.png]](Pasted_image_20231227215256_mkguik)

4096

P19) Con la última respuesta en mente, podemos decir que el impulso de la víctima es bastante grande. Si se tratara de un sistema heredado, ¿qué tamaño de sector, en bytes, se necesitaría para arrancar el sistema? (Formato: XXX) _(2 puntos)_

512

Q20) Utilice la autopsy. Vamos a examinar otro volcado de memoria proporcionado por Sam Bowne, un instructor del City College de San Francisco. Esto nos dará más práctica con la herramienta. ¿Cuál es la contraseña de Waldo? (Formato: Contraseña) _(2 puntos)_

![[Pasted image 20231227223719.png]](Pasted_image_20231227223719_b4o4lx)

![[Pasted image 20231227224141.png]](Pasted_image_20231227224141_qfaglu)
