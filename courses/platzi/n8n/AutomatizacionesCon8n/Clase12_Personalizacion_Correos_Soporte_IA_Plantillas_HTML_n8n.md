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
¿Quieres que el flujo sea extensible y fácil de entender en tu equipo? 
