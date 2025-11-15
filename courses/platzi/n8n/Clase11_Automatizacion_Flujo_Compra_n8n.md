# Automatización de flujo de compra con notificación y seguimiento

Para más contexto, revisa [Clase 10: Análisis de Sentimiento en n8n](Clase10_Analisis_Sentimiento_n8n.md).

## Resumen
La automatización de la compra es clave para escalar. Aquí verás cómo añadir la categoría compra, enrutar con un switch, notificar por Slack, enviar un email de bienvenida con Gmail y programar un follow up con un nodo wait, todo probado paso a paso para asegurar resultados.

¿Cómo añadir la categoría compra con AI agent y switch?
Para que el flujo tome decisiones correctas, primero se configura la nueva categoría en el AI agent y luego se enruta con el switch. Así, la intención de “compra” activa acciones específicas.

¿Dónde configurar el system message y el prompt?
Abrir el AI agent y editar el prompt o system message. [00:00].
Añadir la palabra clave “compra” junto a info, demo y soporte. [00:00].
¿Cómo enrutar con add routing en el switch?
Ir al nodo switch, hacer scroll y pulsar add routing. [00:00].
Arrastrar el output del agente al campo del switch. [00:00].
Escribir “compra” y renombrar el campo para mayor claridad. [00:00].
Guardar y confirmar que aparece la nueva rama. [00:00].
¿Cómo testear con Execute workflow y unpin?
Si el flujo está en azul, los datos están congelados: botón derecho y unpin. [00:00].
Rellenar nombre y email válido (@gmail.com) y escribir intención de compra: “Me gusta mucho su producto. ¿Cuándo empiezo a usarlo?”. [00:00].
Ejecutar con Execute workflow y verificar que la ruta “compra” se marca en verde (doble clic al nodo para verlo). [00:00].
¿Cómo notificar al equipo y dar la bienvenida con Slack y Gmail?
Tras detectar “compra”, se disparan dos acciones en paralelo: notificar al equipo interno y enviar un mensaje de bienvenida al cliente. Reutilizar nodos acelera la edición y mantiene consistencia.

¿Cómo duplicar nodos para reutilizar configuración?
Duplicar el nodo de Slack con botón derecho y conectar desde la rama “compra”. [00:00].
Duplicar el nodo de mensaje de Gmail y conectarlo a “compra”. [00:00].
Ordenar el diagrama para claridad y guardar cambios. [00:00].
¿Qué mensaje enviar en Slack al canal de sellers?
Personalizar el texto: “Equipo, buenas noticias, no nos vamos a hundir, nos han comprado”. [00:00].
Mantener el mismo equipo/canal usado previamente. [00:00].
Verificar en el canal de sellers que el mensaje se envió correctamente. [00:00].
¿Qué asunto y cuerpo usar en el email de bienvenida?
Asunto: “Bienvenido a nuestra empresa”. [00:00].
Cuerpo simple y directo: “Hola, [nombre]. Bienvenido a nuestra plataforma.” [00:00].
Confirmar en la bandeja de entrada que llega el correo con el asunto correcto. [00:00].
¿Cómo programar el seguimiento con nodo wait y mensaje directo al vendedor?
El seguimiento garantiza satisfacción del cliente. Se configura un nodo de control de flujo wait para esperar y luego se envía un recordatorio por Slack a una persona específica.

¿Cómo configurar el nodo de control de flujo wait?
Buscar “wait” o “esperar” y seleccionar el nodo de espera. [00:00].
Opciones disponibles: tras intervalo, en fecha concreta, tras llamada de API o envío de formulario. [00:00].
Para la práctica: usar un intervalo corto de 5 segundos (en real, podría ser una semana o un mes). [00:00].
¿Canal o usuario en Slack para seguimiento?
Duplicar el nodo de Slack y conectarlo a wait. [00:00].
Cambiar el destino de “canal” a “usuario” y seleccionar en la lista a la persona responsable. [00:00].
Mensaje de recordatorio: “Hola, recuerda hacer el seguimiento de [nombre]. Email: [email].”. [00:00].
¿Cómo validar el flujo paso a paso?
Fijar datos con pin para no reenviar el formulario y ejecutar. [00:00].
Observar: mensaje de Slack al canal enviado. [00:00].
Observar: email de bienvenida enviado. [00:00].
Observar: nodo wait espera 5 segundos y luego envía el Slack directo al usuario. [00:00].
Ideas y habilidades que te llevas: - Clasificación por intención con AI agent y categoría “compra”. [00:00]. - Enrutamiento condicional con switch y add routing. [00:00]. - Reutilización de nodos con duplicar para acelerar la configuración. [00:00]. - Mensajería multicanal: Slack para equipo y Gmail para clientes. [00:00]. - Control de tiempos con nodo wait para programar seguimiento. [00:00]. - Pruebas y depuración con pin/unpin, Execute workflow, zoom y verificación visual del flujo. [00:00].

¿Te gustaría ver variantes del mensaje de bienvenida o del recordatorio de seguimiento? Comparte tu objetivo y lo ajustamos juntos.
Ivy Saskia Sejas Rocabado
Ivy Saskia Sejas Rocabado

student
•
hace 3 meses
SI


2

Ver 2 respuestas más
jimmy yahir gutierrez
jimmy yahir gutierrez

student
•
hace 3 meses
el de soporte y cliente va quedar loco con tanto correo jaja


12

Responder

Reportar
Royer Guerrero Pinilla
Royer Guerrero Pinilla

student
•
hace 2 meses
Conecta jira y le colocas el seguimiento como subtask


2
Edwar Y. Castillo B.
Edwar Y. Castillo B.

student
•
hace 2 meses



7

Responder

Reportar
Daniel Antonio Millan Villalba
Daniel Antonio Millan Villalba

student
•
hace 2 meses
Me gusta tu personalización me ayudas con la mía.


2
Ronald Cuello
Ronald Cuello

student
•
hace 2 meses
He modificado el system prompt un poco para la detección de la intención del usuario:


Clasifica el siguiente mensaje en una de las siguientes categorías, basándote en la intención principal del usuario:

* **info**: El usuario busca información general sobre el producto o servicio.
* **demo**: El usuario quiere ver una demostración.
* **compra**: El usuario desea comprar algo o preguntar sobre el proceso de compra.
* **soporte**: El usuario tiene un problema, una queja o necesita ayuda con un producto existente.

La respuesta debe ser solo la palabra en minúscula que corresponda a la categoría (ej. 'info').

7

Responder

Reportar
Pedro Jesus Hincapie Garcia
Pedro Jesus Hincapie Garcia

student
•
hace 2 meses
jajaja Buenas noticias, no nos vamos a hundir... jajaja eso le diré a mi equipo de venta, para que se motiven todos los días a vender jajjajaj


7

Responder

Reportar
Fabián Ardila
Fabián Ardila

student
•
hace 3 meses
Noo! casi se acaba y no veo clase de poder ejecutarlo en local!! 💔


5

Responder

Reportar
Andres Felipe Restrepo Mejia
Andres Felipe Restrepo Mejia

student
•
hace 3 meses
está en el otro curso, en el que es con luis


5
Abinadi Contreras
Abinadi Contreras

student
•
hace 2 meses
Con npm es facil


2

Ver una respuesta más
Simón Marín
Simón Marín

student
•
hace 2 meses
Excelente contenido, tengo una consulta respecto al módulo de espera. Si bien el flujo se activa cuando recibe información, ¿qué pasaría si este módulo tiene una espera de 5 días y durante ese tiempo llega otro formulario de información y, por tanto, activa el flujo de automatización?

Mi consulta es, ¿el flujo debe primero terminar el proceso lineal, o sea, solamente funciona registro por registro, o puede funcionar de forma simultánea con distintos registros a la vez?


4

Responder

Reportar
Gonzalo Piñeiro Aleman Urquiza
Gonzalo Piñeiro Aleman Urquiza

student
•
hace 2 meses
•
editado
Podemos crear un nodo code, utilizando javascript, se puede crear un algoritmo para poder setear información base, como cannal o mensaje (para el caso de slack), asi podemos evitar tener muchos nodos de acciones repetidos. Tambien podemos evitar el nodo switch


3

Responder

Reportar
johnatan ramos
johnatan ramos

student
•
hace 2 meses
Veo


1
Hugo Rafael Cabrera
Hugo Rafael Cabrera

student
•
hace 6 días



2

Responder

Reportar
Brian Axel Rodríguez
Brian Axel Rodríguez

student
•
hace un mes



1

Responder

Reportar
Bautista Ribotta
Bautista Ribotta

student
•
hace un mes
El mensaje que uso de ejemplo "cuando lo pruebo?" hizo que el agente de IA (Gemini 2.5) delire y termine manejando el flujo a caminos aleatorios, ¿Como se podria arreglar algo asi?


1

Responder

Reportar
Natán Mejía
Natán Mejía

student
•
hace un mes
•
editado
En mi caso le detallé mas "System Message".

Eres un asistente experto en clasificación de mensajes.

Analiza el texto enviado por el usuario y determina a cuál de las siguientes categorías pertenece:

info → cuando el mensaje solicita información general, precios, detalles o características del producto o servicio.

demo → cuando el usuario pide una demostración, presentación o reunión para conocer la solución.

compra → cuando el mensaje expresa intención de adquirir, contratar o comprar el producto o servicio.

soporte → cuando el usuario reporta un problema, error, falla o necesita ayuda técnica.

Instrucciones importantes:

Elige solo una categoría.

Devuelve únicamente la palabra de la categoría, en minúsculas y sin comillas.

No incluyas texto adicional, explicaciones ni puntuación.

Ejemplos:

“Quiero saber cuánto cuesta su servicio” → info

“Podemos agendar una demo para mi equipo?” → demo

“Deseo comprar su producto hoy” → compra

“El sistema no funciona correctamente” → soporte


3
Mateo Montoya Henao
Mateo Montoya Henao

student
•
hace un mes
✨ Visual Summary of the Lecture: Automating Purchase Flow with Notification and Follow-Up ✨

1. The Central Idea (The Core 💡):
Automate the purchase workflow in n8n Cloud to notify customers and teams efficiently, ensuring a smooth follow-up process.

2. Key Points (In Bullet Points 📌):

Purchase Category Addition: Integrate 'purchase' in the AI agent and switch nodes to categorize requests properly.
Notification to Team: Duplicate Slack notification nodes to inform the internal team of successful purchases.
Welcome Email: Send personalized welcome emails to customers using Gmail nodes, adjusting message content dynamically.
Follow-Up Mechanism: Implement a wait node to schedule follow-ups after a specified duration for customer satisfaction checks.
3. The Crucial Example or Fact 🚀:
Successfully sent messages to both the team and the customer, showcasing the automated notification process, including a follow-up message to ensure customer satisfaction.

4. Connection or Next Step 🔗:
This workflow serves as a foundation for more complex automations, like leveraging AI for personalized follow-ups, as discussed in upcoming classes.


1

Responder

Reportar
Carlos Rodríguez
Carlos Rodríguez

student
•
hace 2 meses
N8N es como zapier pero con esteroides y el nivel de escalabilidad es increible


1

Responder

Reportar
santiago Prada
santiago Prada

student
•
hace 2 meses
alguno sabe si existe una alternativa a utilizar oAuth2.0 o la solucion para que estas credenciales no expiren constantemente?.

tengo alojado n8n en un vps de hostinguer y es un problema al cual me enfrento donde se debe de estar recargando la credencial periodicamente.


1

Responder

Reportar
carlos adrian choquehuanca mamani
carlos adrian choquehuanca mamani

student
•
hace 2 meses
Por lo que estuve revisando, el problema no viene de n8n sino de Google: en modo Testing los permisos de OAuth caducan a los 7 días. Eso hace que la credencial se desconecte sola.

Una solución rápida y manual es simplemente entrar a n8n cada semana y darle a Reconectar. Yo lo que hago es ponerme un recordatorio (uso Todoist) programado cada 7 días para no olvidarme.


1
Gilberto Gutiérrez Gordillo
Gilberto Gutiérrez Gordillo

student
•
hace 3 meses
perdón pero no me queda claro como es que sabe el flujo cuando se trata de: info, demo, compra , ó soporte, ¿ como lo identifica ? con una palabra clave o que por favor alguien me puede decir ...


1

Responder

Reportar
Idir Ouhab Meskine
Idir Ouhab Meskine

teacher
•
hace 3 meses
Eso se extrae el agente de IA, se explica en la clase "Integración de agentes de IA en N8N para clasificar leads automáticamente.


1
Brandon Vargas
Brandon Vargas

student
•
hace 2 meses
El agente de IA lee el mensaje y al ser "inteligente" clasifica automáticamente el mensaje dentro de alguna de las categorías definidas, entendiendo el contexto y sentido de lo que escribe el usuario. Así es cómo funciona, saludos!


1
