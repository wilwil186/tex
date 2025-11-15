# Configuración paso a paso de tu primer flujo en n8n

**Curso de Automatizaciones con n8n**  
**Clase 4 de 14**

## Contexto de clases anteriores
Esta clase continúa la secuencia del curso, implementando en n8n el diagrama de flujo diseñado en la [Clase 3](Clase3_Simbolos_Diagramas_Flujo.md). Aplica los conceptos de automatización sin programar introducidos en la [Clase 1](Clase1_Automatizacion_Workflows_IA.md) y los flujos de soporte automatizados de la [Clase 2](Clase2_Flujos_Soporte_Automatizados.md). Aquí aprenderás a crear un workflow práctico que gestiona leads: recibe datos de un formulario, evalúa el mensaje con un nodo condicional (if) y envía notificaciones por Slack o Gmail, integrando IA para decisiones inteligentes.

## Resumen
Aprende a configurar un flujo en n8n paso a paso para gestionar leads. Incluye un trigger, evaluación de mensaje con nodo if, y acciones de notificación. Practica nombrado de workflows, creación de datos de prueba, pruebas de ramas true/false, y preparación de acciones antes de conectar credenciales.

## Lecturas recomendadas
- AI Workflow Automation Platform & Tools - n8n

## Preparación del espacio en n8n
Comienza creando una cuenta en n8n.io y completando el onboarding básico para sentar bases sólidas.

### Pasos iniciales:
1. Crea la cuenta y haz clic en **Get Started**.
2. Completa el formulario: dónde conociste n8n (ej.: Google) y para quién es la cuenta (para mí).
3. Pulsa **Submit**, omite invitaciones con **Skip** y continúa con **Start Automating**.
4. Inicia un workflow con **Start from Scratch** y cambia el nombre en la esquina superior izquierda (ej.: "mi flujo").
5. Recuerda: el **trigger** es el evento que inicia el flujo (aquí, un lead).

## Configuración del trigger para pruebas
Para testear el workflow, usa un trigger manual antes de cambiarlo por un formulario real.

- Añade el primer paso con **Add First Step** y selecciona un trigger manual.
- Más adelante, cámbialo por un formulario para datos reales del usuario.

## Nodos y condiciones del flujo de leads
El flujo se basa en tres componentes clave: nodo **set** para simular datos, nodo **if** para decidir según el texto, y ejecución para validar ramas.

### Configuración del nodo set con datos estáticos
1. Agrega un segundo nodo y busca **set** para crear campos.
2. Define nombre, email y mensaje desde "drag input fields".
3. Escribe un mensaje de prueba, ej.: "quiero una demo".
4. Ejecuta con **Execute workflow** y verifica que el nodo set muestra el mensaje configurado.

### Evaluación de texto con el nodo if y ramas true/false
1. Añade un nodo **if**. Arrastra el campo mensaje al primer cuadro.
2. Elige tipo **string** y condición **contiene**.
3. En el último campo, escribe "demo" para detectar intención de demo.
4. Ejecuta el flujo: observa ramas **true branch** y **false** según contenga "demo".
5. Prueba borrando "demo" en el set y ejecuta para ver rama false activa.

### Tipos de datos admitidos en condiciones string
- **String**: para texto.
- **Number**: para números.
- **Date and time**: para fechas y tiempos.
- Otros tipos complejos existen, pero no son necesarios ahora.

## Conexión de acciones en Slack y Gmail sin credenciales
Aunque los nodos aparezcan en rojo por falta de credenciales, configura campos clave y deja acciones definidas: Slack para "sí", Gmail para "no".

### Configuración en Slack (condición true)
1. En rama true, agrega nodo **Slack** con acción **send message**.
2. Define destinatario en **channel** o **user**; elige **channel**.
3. Selecciona canal **by name** y usa "#sellers".
4. Escribe mensaje, ej.: "nuevo lead".

### Envío por Gmail (condición false)
1. En rama false, agrega **email** y usa **Gmail** con **send message**.
2. Arrastra campo email del set al campo "to".
3. Asunto: "gracias". Mensaje: "gracias por su interés".

## Operación en producción con credenciales
Conecta credenciales de Slack y Gmail para envío real. Sin ellas, el flujo toma forma y permite probar lógica.

## Idea para practicar
Añade datos de contacto (nombre y email) en el mensaje de Slack para acción rápida del equipo. Sube captura en comentarios indicando estructura. ¿Otra variante de filtro en if? Compártela y qué canal usarías para distintos tipos de lead.
Cristian Morón Oñate
Cristian Morón Oñate

student
•
hace 3 meses
Este es mi mensaje




13

Responder

Reportar
Luz Angélica Barrera Peña
Luz Angélica Barrera Peña

student
•
hace 12 días
te dieron respuesta ?. Estoy igual.


1
Karla Gabriela Alvarado Barrancos
Karla Gabriela Alvarado Barrancos

student
•
hace 3 meses
Recomienda usar un VPS en hostinger en vez de pagar mes con mes en n8n.io?


10

Responder

Reportar
Eduardo Recinos
Eduardo Recinos

student
•
hace 3 meses
Puedes instalarlo en local y no pagas nada.


6
Idir Ouhab Meskine
Idir Ouhab Meskine

teacher
•
hace 3 meses
tienes varias opciones, puedes usar la opción de pagar n8n.io y así tienes mas facilidad de obtener las actualizaciones y además el soporte.

O puedes usar cualquier topo de VPS o tu propia máquina local para instalarlo.

En uno te ahorras la gestión de la instalación y actualización, pero tiene un coste. En la otra, tiene un coste menor pero tienes que encargarte del mantenimiento.


6

Ver 5 respuestas más
Alexandra Rivero
Alexandra Rivero

student
•
hace un mes
Hola! Me está pasando que a medida que veo la clase, me saltan las pruebas de conocimientos, pero en ocasiones estas pruebas son de temas adelantados a los cuales no he ni llegado en la misma clase, sería bueno revisar en el momento en que salen :)


8

Responder

Reportar
Jorge Luis Velázquez Téllez
Jorge Luis Velázquez Téllez

student
•
hace 21 días
Totalmente de acuerdo y esto pasa con varios cursos, no solo con este.


3
Johan Garcia
Johan Garcia

student
•
hace 2 meses
Usen mejor Docker Compose:

creen un archivo con nombre docker-compose.yml en un directorio X y ponganle el siguiente contenido:


version: '3.7'

services:
  n8n:
    image: docker.n8n.io/n8nio/n8n
    container_name: n8n
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
      - GENERIC_TIMEZONE=America/New_York
      - TZ=America/New_York
    volumes:
      - n8n_data:/home/node/.n8n

volumes:
  n8n_data:
Desde una terminal situados dentro del directorio creado que contiene el archivo docker-compose.yml:


docker-compose up -d
¡Listo! 🚀 n8n estará corriendo. Puedes acceder igual desde http://localhost:5678.

Para detenerlo, desde la misma carpeta, ejecuta:


docker-compose down
Esto detendrá y eliminará el contenedor, pero tu volumen n8n_data con tus workflows permanecerá intacto para la próxima vez que lo inicies con docker-compose up -d.


6

Responder

Reportar
Angel David cortes Rodríguez
Angel David cortes Rodríguez

student
•
hace 3 meses
Sí, n8n permite integrar con diversas plataformas, incluyendo Office 365. Puedes utilizar nodos específicos para conectarte a servicios de Office 365, como Outlook o OneDrive. Esto te permite automatizar tareas entre n8n y Office 365, optimizando flujos de trabajo y reduciendo tareas repetitivas. El enfoque low-code de n8n facilita la creación de estas integraciones sin necesidad de escribir mucho código.


5

Responder

Reportar
Diego Adolfo Forero Garzon
Diego Adolfo Forero Garzon

student
•
hace 2 meses
el if esta mal definido, porque si el cliente escribe "no quiero una demo" igual se va por el camino de demo


5

Responder

Reportar
Josué Rubén Robles Gonzalez
Josué Rubén Robles Gonzalez

student
•
hace 2 meses
Tienes razón lo mejor quizás sería llamar a un llm muy pequeño para q lo evalúe, vd?


2
Christian Arturo Rios  Mock
Christian Arturo Rios Mock

student
•
hace 3 meses
Hola team, el segundo test me salio en el minuto 3:07, y me pregunta una parte del flujo que en teoria no hemos visto aun, quizas convenga ponerle mas adelante en el video.

quizas es error mio, solo lo dejo por aca. : )


4

Responder

Reportar
Kevin Ortiz
Kevin Ortiz

student
•
hace 3 meses
Me pasa lo mismo, deberian ponerlo mas adelante.


2
Miguel Libreros
Miguel Libreros

student
•
hace 2 meses
Hola compañero.

El primero crea el Diagrama de flujo para que puedas entender toda la automatización que vas a hacer. Hasta antes de que aparezca la trivia, él ya a apuesto el trigger, después setea los datos y después le pone la condición del if, hasta ahí, ya vas a poder poner los primeros tres bloques del test, y ya después si prestaste atención al fujo dice que le va a conectar Slack y también Email, entonces realmente el test tiene un buen timing.


2
Alejandra Cerecedo
Alejandra Cerecedo

student
•
hace 3 meses


Mi mensaje!

3

Responder

Reportar
Franklyn Guillen
Franklyn Guillen

student
•
hace 3 meses



3

Responder

Reportar
Diego Herrera
Diego Herrera

student
•
hace 22 días
Vas demasiado rápido toca verlo en 0.5x


2

Responder

Reportar
Johann Sebastian Salazar Cabrera
Johann Sebastian Salazar Cabrera

student
•
hace 20 días



2

Responder

Reportar
William Ruiz
William Ruiz

student
•
hace un mes
excelente clase


2

Responder

Reportar
Jimmy Vidal
Jimmy Vidal

student
•
hace 2 meses


es así no?

2

Responder

Reportar
Felipe Santiago Roldán Rodríguez
Felipe Santiago Roldán Rodríguez

student
•
hace 2 meses



2

Responder

Reportar
JOSE ANTONIO MESA GONZALEZ
JOSE ANTONIO MESA GONZALEZ

student
•
hace 2 meses



2

Responder

Reportar
christhopher racchumi gonzales
christhopher racchumi gonzales

student
•
hace 2 meses



2

Responder

Reportar
Cristobal Jose Quilimaco Lopez
Cristobal Jose Quilimaco Lopez

student
•
hace 2 meses
Mi mensaje en slack



Mi mensaje en Gmail




2

Responder

Reportar
jappsku Aponte
jappsku Aponte

student
•
hace 2 meses
Que molesto que acá nada presenta un quiz para contestar, hay forma de desactivar esto ?


2

Responder

Reportar
Josué Rubén Robles Gonzalez
Josué Rubén Robles Gonzalez

student
•
hace 2 meses
Me parece muy bueno el quiz, personalmente me encanta, pero si debería de haber una opción para activarlo.


1
