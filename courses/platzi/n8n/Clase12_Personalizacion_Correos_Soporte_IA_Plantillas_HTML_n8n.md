# Personalización de correos de soporte con IA y plantillas HTML

Para más contexto, revisa [Clase 11: Automatización de flujo de compra con notificación y seguimiento](Clase11_Automatizacion_Flujo_Compra_n8n.md).

## Resumen
Optimiza el soporte al cliente con un flujo claro y profesional: desde detectar el sentimiento hasta enviar correos personalizados con IA, usar plantillas en HTML y CSS compatibles con Gmail y registrar incidencias en Google Sheets. Aquí verás cómo se conectan los nodos, cómo mapear campos y cómo acelerar pruebas con pin/unpin para un proceso ágil y confiable.

¿Cómo estructurar el flujo de soporte con IA y sentimiento positivo?
El punto de partida es separar casos: si el cliente está enfadado, va a un equipo humano; si el sentimiento es positivo, se automatiza. Para probarlo con rapidez, primero se hace unpin de los datos, se ejecuta el formulario, se introduce un nombre y un correo real y se envía un mensaje con tono amable. Tras validar que el flujo detecta correctamente el sentimiento, se vuelve a hacer pin para congelar datos y acelerar las pruebas.

Formulario y pruebas rápidas: usar correo real, ejecutar y validar sentimiento positivo.
Pin/unpin: congelar o liberar datos para acelerar iteraciones.
Ruta del flujo: positivo → correo personalizado; enfadado → equipo humano.
¿Dónde ubicar el agente de IA y cómo configurar el prompt?
El agente de IA se añade en la línea verde del flujo con Add → AI. En la configuración, se usa “source for prompt” para tomar datos previos desde “edit fields” y se arrastra el “mensaje” al campo “prompt”. Además, se define un “system message” que pide una respuesta corta que resuelva el problema; si es genérico, debe solicitar más detalles.

Datos de entrada: “mensaje” desde edit fields hacia “prompt”.
Instrucción clara: generar respuesta breve y útil; pedir detalles si faltan.
¿Cómo conectar el cerebro con OpenAI y validar la salida?
Si el nodo marca en rojo, hace falta el “cerebro”: se conecta a un nodo de OpenAI. Tras ordenar el canvas, se testea y se abre el agente para ver la respuesta. Un ejemplo generado: “Hola, nos alegra saber que te gusta mucho nuestro producto…”. Luego, en el nodo de Gmail, se arrastra el output del agente al cuerpo del correo, se limpia el contenido anterior y se guarda.

Conexión: agente de IA → nodo OpenAI.
Mapeo en correo: output del agente al cuerpo en Gmail.
Prueba en bandeja de entrada: recibir y revisar el mensaje.
¿Cómo personalizar emails con plantillas HTML compatibles con Gmail?
Para dar un salto de calidad, se usa ChatGPT para generar un “template” en HTML y CSS compatible con Gmail, dejando un espacio para insertar el cuerpo que generó la IA. En el nodo de correo, se pega la plantilla, se localiza “cuerpo principal” y se reemplaza por el output del agente. Se previsualiza a la derecha, se guarda y se testea con datos fijados en pin.

Plantilla profesional: estructura en HTML/CSS compatible con Gmail.
Inserción dinámica: reemplazar “cuerpo aquí” con el output del agente.
Resultado: mensaje más claro, con espacio para el nombre de la empresa.
¿Cómo adaptar el mensaje al problema específico del cliente?
Cuando el cliente detalla su problema (“no me funciona el botón amarillo”), la IA responde de forma específica, por ejemplo sugiriendo reiniciar la máquina. Así se evita un correo genérico y se entrega una ayuda contextual.

De genérico a específico: si hay detalle, la respuesta se ajusta al caso.
Coherencia del tono: mantener cortesía y claridad.
¿Cómo registrar incidencias en Google Sheets y mantener seguimiento?
Para el seguimiento, se añade un nodo de Google Sheet con la acción “append row in sheet”. Se configuran credenciales con “create new credential” y “sign in with Google”, se elige el spreadsheet “clientes” y la “sheet one”. El sistema detecta cabeceras automáticamente. Se arrastran los valores desde nodos previos: “nombre” y “email” desde edit fields, y la “fecha de incidencia” desde el formulario (campo “submitted at”). Tras ejecutar, se verifica que se añadió el “book” y la fecha.

Luego se crea una columna extra “error del cliente”. El nodo muestra un icono de aviso: se reabre y aparece el nuevo campo. Se arrastra el “mensaje” al mapeo, se guarda y se ejecuta de nuevo. El registro queda completo y útil para mejorar el producto.

Cabeceras y mapeo: nombre, email, fecha de incidencia desde “submitted at”.
Columna adicional: “error del cliente” para recoger el mensaje exacto.
Ejecución del workflow: validar que los datos llegan a la hoja.
¿Quieres que el flujo sea extensible y fácil de entender en tu equipo? Comparte qué ampliarías o qué nodo agregarías en los comentarios.
Santiago Rodz
Santiago Rodz

student
•
hace 3 meses
Yo le cambié el formato a la fecha porque se veía feo. Lo dividí en tres campos:

FECHA | HORA | DÍA DE LA SEMANA



El resultado final en mi base de datos de Google Sheets es el siguiente:



A continuación, el código por si lo quieren hacer: Fecha:

{{ DateTime.fromISO($json.submittedAt).toFormat('dd-LL-yy') }}

Hora:

{{ DateTime.fromISO($json.submittedAt).toFormat('HH:mm \'Horas\'') }}

Día de la semana:

{{ DateTime.fromISO($json.submittedAt).setLocale('es').toFormat('cccc') }}


23

Responder

Reportar
Amin Chavarria
Amin Chavarria

student
•
hace 2 meses
Sí, en n8n puedes conectarte a bases de datos en lugar de usar hojas de cálculo. Puedes utilizar nodos específicos para bases de datos como MySQL, PostgreSQL, MongoDB, entre otros. Esto te permite realizar operaciones de lectura y escritura directamente en la base de datos, lo cual es más eficiente para manejar grandes volúmenes de datos en comparación con las hojas de cálculo. Asegúrate de tener las credenciales necesarias y de configurar el nodo adecuadamente para realizar la conexión.


9

Responder

cs
Javier Camilo Torres Vera
Javier Camilo Torres Vera

student
•
hace 16 días
Puedo conectar la base de datos en supabase y visualizar en dashboard en nexjs?


1
Platzi Team
Platzi Team

student
•
hace 16 días
Hola ✌🏻 en mi empresa yo implemento modelos ETL, conectandome a una base de datos origen y a la base de datos destino, hago toda la transformación de datos en n8n y hago el cargue final en postgres para luego conectar Power bi a mi BD, levantamos el Datagateway de power BI para programar su consumo de datos y actualización automatica del tablero BI. Con eso hacemos todo un flujo de trabajo, extraemos, transformamos, cargamos y por ultimo llevamos a visualización sin intervención humana.


5

Ver una respuesta más
Diego Cesar Lerma Torres
Diego Cesar Lerma Torres

student
•
hace 3 meses
En la fecha de incidencia, no me gusta que el formato que se recibe de n8n no sea legible para humanos y tampoco se procese fácilmente por Google Sheets.

Encontré dos soluciones:

Opción 1: La que me pareció más limpia:
Agregar un nodo entre "On form submission" y "Edit Fields" llamado Date & Time.

Este nodo formateará la fecha para que sea más legible tanto por nosotros como por Sheets.


En Operation pondremos Format a Date.

En Date ponemos el valor que recibimos del nodo anterior de submittedAt

En formato, pondremos Custom Format, con la estructura que queramos. En mi caso, puse dd/MM/yyyy HH:mm:ss para evitar que se pierda la hora.

En Ouput Field Name puse formattedDate y este fue el valor que le pasé a Edit fields para fechaFormateada


Opción 2: Con código
La segunda opción me parece un poco más sucia, debido a que usa código y es menos explícita y legible para el resto del equipo, pero también es útil y nos evita agregar el nodo extra.

En Edit Fields, podemos poner en el value de fechaFormateada:


{{ new Date($json["submittedAt"]).toLocaleString('es-MX', { timeZone: 'America/Mexico_City' }) }}

Esto formateará todo automáticamente y hará que la información que llegue a Google Sheets sea legible y fácil de manejar.

Luego, en Google Sheets, con toda esta información, podemos darle un formato variable con las funciones de formato de la hoja de cálculo.

Para ello damos clic para seleccionar toda la columna de fecha de incidencia, damos clic en donde dice 123, a la izquierda de donde le cambiamos la fuente al texto y ahí seleccionamos el formato que queramos. Puede ser Fecha, Hora, Fecha y Hora, o incluso un formato custom.

Así, no perdemos nada de información, pero solo mostramos a quienes consuman esta hoja de cálculo la información que necesitan de un vistazo.



7

Responder

Reportar
Daniel Hidalgo
Daniel Hidalgo

student
•
hace 11 días
en Date & Time / Custom Format le puse "ff" que da como resultado esto, ejem: Nov 4, 2025 8:26 PM

Aquí están las posibles combinaciones que pueden usar de la documentación de n8n: https://moment.github.io/luxon/#/formatting?id=table-of-tokens


2
Giancarlo Zevallos Lecca
Giancarlo Zevallos Lecca

student
•
hace 2 meses
Me parece muy buena la clase, en mi caso prefiero usar un nodo mas simple que el de agente, mas que todo para hacerlo más bonito por ejemplo el nodo específico de OpenAI


4

Responder

Reportar
Wilson Barrera
Wilson Barrera

student
•
hace un mes
tip: para las prueba podria hacer pin al switch para evitar que me consuman creditos de usar la ia en la primera parte...


4

Responder

Reportar
Juan Camilo Ortiz Villegas
Juan Camilo Ortiz Villegas

student
•
hace 3 meses
Hice unos cambios al flujo, para que genere un markdown y posible respuesta con un segundo agente.



El system message es:


Eres un generador de mensajes con formato **Slack mrkdwn**. 
Tu salida debe ser **solo texto**, sin HTML, sin JSON y sin bloques de código. 
Usa los siguientes datos (inyectados por n8n) y entrega un mensaje conciso (máx. 6–7 líneas).

**Datos:**
- Nombre: {{ $('Code').item.json.nombre }}
- Categoría: {{ $('AI Agent').item.json.output }}  → `demo` | `info` | `soporte`
- Mensaje: {{ $('Code').item.json.mensaje }}
- Sentimiento: {{ $json.sentimentAnalysis.category }} → `positivo` | `neutral` | `negativo`

**Reglas:**
- El mensaje debe estar formateado con **mrkdwn** básico (negritas mediante asteriscos).
- Usa **negritas** para los rótulos de cada campo.
- Genera una **Solución propuesta** breve (1–2 frases), accionable y acorde al sentimiento.
- Ajusta el tono de la **Solución propuesta** según el **sentimiento**:
  - `positivo`: motivador y proactivo.
  - `neutral`: informativo y cordial.
  - `negativo`: empático y resolutivo.
- **No** incluyas tiempos de respuesta ni compromisos específicos.
- **No** agregues explicación fuera del mensaje final.
- **No** uses emojis.

**Estructura a producir (exacta, reemplazando con los datos):**
*Nuevo mensaje recibido*

*Nombre:* {{ $('Code').item.json.nombre }}
*Canal:* {{ $('AI Agent').item.json.output }}
*Mensaje:* {{ $('Code').item.json.mensaje }}
*Sentimiento:* {{ $json.sentimentAnalysis.category }}
*Solución propuesta:* [redacta aquí una acción breve y concreta, ajustada a canal y sentimiento, sin prometer tiempos]

4

Responder

Reportar
Bautista Ribotta
Bautista Ribotta

student
•
hace un mes
¿Como hiciste para crear los recuadros de colores verde, azul y violeta?


1
Platzi Team
Platzi Team

student
•
hace 16 días
Hola, das click derecho y agregas una nueva nota


2
Ana Sofía Aguirre
Ana Sofía Aguirre

student
•
hace 3 meses
Muy buenoo


3

Responder

Reportar
Claudia Z. González Sáenz
Claudia Z. González Sáenz

student
•
hace 3 meses
Yo registraria todos los emails para luego analizar y ver si hay algo que puedo mejorar en mi proceso "producto" o me puedo anticipar a las necesidades de los clientes.


3

Responder

Reportar
Valeria Solari Herrera
Valeria Solari Herrera

student
•
hace 2 meses
Para manejar los casos donde el sistema clasifica erróneamente sentimientos como negativos y envía respuestas genéricas, revisa la lógica de tu flujo en n8n. Asegúrate de que el módulo de análisis de sentimiento esté correctamente entrenado y que los prompts sean claros y específicos para detectar emociones. Considera implementar un mecanismo de revisión manual o un sistema que ajuste la clasificación automáticamente en función de la retroalimentación del cliente. Esto mejorará la precisión de las respuestas y personalización del soporte.


3

Responder

Reportar
Nain Cortes
Nain Cortes

student
•
hace 2 meses
le falta el numero de d caso


3

Responder

Reportar
Julian Leonardo Cardozo
Julian Leonardo Cardozo

student
•
hace 17 días
Es imprecinante todo lo que se puede hacer con esta herramienta de N8N de la mano de un modelo de Inteligencia Artificial




3

Responder

Reportar
Daniel Hidalgo
Daniel Hidalgo

student
•
hace 11 días
Así resolví lo de la hora para que me de un formato más agradable:








2

Responder

Reportar
Manfred Bustos
Manfred Bustos

student
•
hace 16 horas
Prompts Genera una respuesta en modo texto que solucione el problema del cliente.

Si es generico, preguntale como le podemos ayudar y que de mas detalles.

Genera un template en html y css que sea compatible con Gmail para dar la bienvenida a mi cliente que acaba de comprar nuestro producto. Que se vea profesional y con una cabecera que genere engagement. El cuerpo del mensaje ya esta predefinido así que deja un placeholder que diga CUERPO_AQUI


1

Responder

Reportar
ARLEY ALEJANDRO TOLOZA MARTINEZ
ARLEY ALEJANDRO TOLOZA MARTINEZ

student
•
hace 13 días





1

Responder

Reportar
Walkyria Espitia
Walkyria Espitia

student
•
hace un mes
Alguien sabe como cambiar aqui el formato de la fecha. Gracias


1

Responder

Reportar
Juan Carlos García Priego
Juan Carlos García Priego

student
•
hace un mes
Solo ponlo asi



{{ DateTime.fromISO($('On form submission').item.json.submittedAt).toFormat('yyyy-MM-dd HH:mm:ss') }}

2
Juan Carlos García Priego
Juan Carlos García Priego

student
•
hace un mes


Generado con Gemini 2.5

1

Responder

Reportar
Brian Axel Rodríguez
Brian Axel Rodríguez

student
•
hace un mes
En mi caso, lo hice con Microsoft Outlook, y para lograr el cuerpo del email tuve que habilitar la opcón de Message Type = HTML

Les paso el tip en caso de que también hayan recibido el código plano en su primer intento.






1

Responder

Reportar
Natán Mejía
Natán Mejía

student
•
hace un mes
Prompt: Quiero que generes un template en html y css que sea compatible con gmail para dar la bienvenida a mi cliente que acaba comprar nuestro product. Que se vea profesional y con una cabecera que genere engagement. El cuerpo del mensaje ya está predefinido así que deja un placeholder que diga CUERPO_AQUI


1

Responder

Reportar
alejandro gomez
alejandro gomez

student
•
hace 2 meses


Ayuda, deje mi flujo quito por 2 días debido a un viaje, hoy que regrese a continuar el curso al momento de ejecutar el flujo me aparece este error. Ya intente cambiar la API pensando que era eso pero no funcionó.

¿Alguien sabe que puede ser?

Gracias


1

Responder

Reportar
Bautista Ribotta
Bautista Ribotta

student
•
hace un mes
Tuve el mismo problema, nose porque pero pareciera que N8N tiene algun problema con lA y el mensaje que usan, como que en algun momento el mensaje que el usuario carga en el formulario, la IA lo toma como vacio cuando literamente te deja leer el mensaje de lo que pusiste


1
