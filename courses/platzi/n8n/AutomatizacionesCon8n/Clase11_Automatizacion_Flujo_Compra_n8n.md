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