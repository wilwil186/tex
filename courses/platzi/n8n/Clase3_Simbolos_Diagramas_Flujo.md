# Símbolos de diagramas de flujo y su aplicación práctica

**Curso de Automatizaciones con n8n**  
**Clase 3 de 14**

## Lecturas recomendadas
- Lucidchart | Diagramming Powered By Intelligence

## Resumen
Domina cómo convertir un proceso real en un diagrama de flujo claro y accionable: desde recibir un lead hasta decidir si activar al equipo de ventas por Slack o enviar un email de agradecimiento. Aquí verás los símbolos esenciales, el orden lógico y las preguntas que validan un workflow efectivo.

## ¿Cómo diseñar un workflow que capta leads y decide acciones?
Para empezar, se define el objetivo: recibir un lead interesado en el producto [01:00]. El flujo inicia con un inicio/fin y continúa con la entrada de datos que el cliente envía por formulario.

- **Inicio**: óvalo llamado lead [01:00].
- **Entrada/salida**: paralelogramo para recoger nombre, email y mensaje [01:15].
- **Decisión**: rombo para evaluar si el mensaje contiene la palabra "demo" [01:30].
- **Acciones**: rectángulos con dos caminos posibles [01:45].
- La lógica es binaria y directa: si el mensaje contiene "demo", se notifica al equipo de ventas por Slack [01:45]. Si no, se envía un email de agradecimiento [01:50]. Habilidad clave: mapear entradas, formular una decisión clara y conectar acciones sin ambigüedades.

## ¿Qué pasos prácticos ayudan a construirlo en un software?
Usa un software de diagramas para arrastrar y conectar bloques [00:10]. Nombra cada símbolo con precisión y revisa la dirección de las flechas para evitar conexiones invertidas [01:05].

- Copiar y renombrar el óvalo: lead [01:00].
- Añadir paralelogramo: datos del formulario [01:15].
- Arrastrar rombo: ¿mensaje contiene "demo"? [01:30].
- Duplicar rectángulos: notificar por Slack o enviar email [01:45].

## ¿Qué habilidades se entrenan al modelar este flujo?
- **Conceptualización de procesos**: traducir un caso real a bloques conectados [00:05].
- **Uso correcto de símbolos**: inicio/fin, acción, decisión, entrada/salida [00:20].
- **Pensamiento condicional**: sí/no con efectos visibles en acciones [01:30].
- **Claridad operativa**: cada camino termina en una acción concreta [01:50].

## ¿Qué significan los símbolos del diagrama y cuándo usarlos?
Los símbolos básicos guían la lectura y evitan confusiones. En pantalla se presentan cuatro fundamentales que cubren el caso base.

- **Óvalo**: inicio o fin del flujo, como cuando alguien envía un formulario [00:20].
- **Rectángulo**: acción operativa, como enviar un email o editar un archivo [00:25].
- **Rombo**: decisión binaria, por ejemplo: ¿el email contiene la palabra "demo", sí o no? [00:28].
- **Paralelogramo**: entrada o salida de datos, como el nombre o el mensaje recibido [00:32].

Consejo práctico: en el panel lateral del software hay más bloques para otros casos. Tómate tiempo para explorarlos y elegir el que mejor represente tu necesidad [00:40].

## ¿Cómo se conectan correctamente los bloques?
Asegura que las flechas salgan de la salida de un bloque y entren a la entrada del siguiente [01:05]. Si un enlace queda al revés, corrígelo antes de continuar para no distorsionar el flujo.

## ¿Qué datos mínimos pedir al lead para decidir?
- **Nombre**: identifica al contacto [01:15].
- **Email**: canal de respuesta [01:15].
- **Mensaje**: campo a evaluar para localizar "demo" [01:15].

## ¿Cómo comprobar que tu diagrama está bien compuesto?
Un buen diagrama responde cuatro preguntas esenciales. Si las contestas con tu flujo, la lógica está completa y las acciones son ejecutables.

- **¿Qué inicia el flujo?**: un formulario enviado por el cliente [02:10].
- **¿Qué decisión se evalúa?**: si el mensaje contiene la palabra "demo" [02:12].
- **¿Qué resultado esperamos?**: una de dos salidas, notificar por Slack o enviar email [02:20].
- **¿Qué acciones se ejecutan?**: envío del mensaje a Slack o email según la condición [02:25].

Ahora piensa en una tarea repetitiva de tu día a día y conviértela en diagrama. Cuando lo tengas, toma una captura y compártela en los comentarios: así enriquecemos el aprendizaje en comunidad.