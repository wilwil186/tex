# Revisión y optimización de workflows en n8n

Para más contexto, revisa [Clase 12: Personalización de correos de soporte con IA y plantillas HTML](Clase12_Personalizacion_Correos_Soporte_IA_Plantillas_HTML_n8n.md).

## Resumen
Optimiza tu automatización en n8n con un proceso claro y sin fallos. Aquí aprenderás a renombrar nodos, probar expresiones, verificar condiciones con IA, etiquetar por departamento y activar en producción. Todo enfocado en que tu flujo sea entendible y estable.

¿Como dejar listo tu workflow en n8n?
Para garantizar calidad, aplica una secuencia simple: nombra bien, prueba paso a paso, valida condiciones, organiza con etiquetas y publica. Así evitas errores y aseguras que cualquiera del equipo sepa qué hace cada nodo.

¿Como renombrar nodos de forma clara?
Usa la tecla space para renombrar más rápido que con el menú contextual.
Nombra con intención: trigger formulario, normalizar datos, excluir Platzi, clasificar mensaje.
Describe función y resultado: qué entra, qué sale y por qué importa.
Mantén consistencia de nombres para facilitar el debug.

¿Como testear expresiones y flujos?
Asegúrate de tener datos congelados en pin: se ven en morado.
Ejecuta con execute workflow para recorrer el camino actual.
Abre el nodo inicial (trigger): normalmente no requiere verificación.
Avanza nodo a nodo con la navegación lateral: adelante y atrás sin cerrar ventanas.
Confirma que las expresiones estén en verde en cada paso.
Repite en todos los caminos del flujo para evitar errores ocultos.

¿Como verificar condiciones y salidas?
Revisa el condicional de exclusión: excluir correos con arroba Plaxi respecto a un correo como promptandplay@gmail.com.
Valida el enrutamiento por intención con IA: demo, info, soporte, compra.
En el switch, alinea nombres de salidas con las condiciones: demo con demo, etc.
Elige el campo correcto: usa la output del nodo de inteligencia artificial si cambiaste la fuente.
Haz clic en la condición para ver su información prevista antes de aceptar.

¿Como organizar y encontrar tus automatizaciones?
Un buen nombre y un sistema de etiquetas te ahorran tiempo cuando crece el número de flujos. Además, comunican propósito y dueño sin explicaciones extra.

¿Como nombrar y etiquetar el flujo?
Cambia el nombre genérico por uno descriptivo: clasificador inteligente de leads.
Añade tags para filtrar por departamento o uso.
Crea la etiqueta "ventas" si no existe y aplícala.
En la vista principal de n8n, filtra por tags y encuentra el flujo al instante.

¿Como publicar en producción y validar ejecuciones?
Trabajar en test y pasar a producción requiere un cambio simple pero crítico. Activa tu workflow, prueba con datos reales y valida resultados desde la vista de ejecuciones.

¿Como activar y probar en producción?
Cambia de la URL de test a la URL de producción.
Activa el flujo con el switch superior hasta ver la confirmación.
Abre la URL, completa el lead: nombre, correo y mensaje como "Quiero una demo".
Tras enviar, el canvas no mostrará en verde lo ocurrido en producción: es normal.

¿Como revisar ejecuciones y datos?
Entra a la vista de ejecuciones para ver historial y estado.
Identifica pruebas de test con el icono de probeta.
En producción no aparece ese icono: así distingues entornos.
Abre una ejecución y revisa los datos usados, por ejemplo el texto "Quiero una demo".

¿Te animas a mejorarlo? Agrega una nota útil, ajusta un nombre o refina una condición. Comparte una captura y cuéntanos qué cambio hiciste y por qué.
Idir Ouhab Meskine
Idir Ouhab Meskine

teacher
•
hace 3 meses
me encanta cómo lo has documentado, da gusto verlo!


14
gemma clavero del moral
gemma clavero del moral

student
•
hace 3 meses
Corrijo Copy/Paste Error en Titulo Ultima rama! ((gracias Profe! por su comentario y a todos los compañeros por sus 💚




16

Ver 3 respuestas más
Cesar Flores
Cesar Flores

student
•
hace 3 meses
Idir, felicidades. De los mejores cursos que he realizado en Platzi. Bien estructurado, se te entiende todo, buen ritmo, no das nada por sentado sino que abordas todos los conceptos necesarios para comprender la idea. Muchas gracias.


20

Responder

Reportar
Pablo Etcheverry
Pablo Etcheverry

student
•
hace 2 meses
Muy buen curso introductorio. Excelente la explicación del docente. Estoy muy contento de ver cursos de n8n en Platzi, felicitaciones!


7

Responder

Reportar
Fabio Nogales
Fabio Nogales

student
•
hace 3 meses
Me gusta mucho la manera sencilla de explicar pero necesito saber bien detalles especificos com correr en local o la optimizacion de recursos y costos que se pueden tener para correr n8n para clientes de todo tipo! Muchas gracias !


6

Responder

Reportar
santiago Prada
santiago Prada

student
•
hace 2 meses
Con un vps de hostinguer te puede ir muy bien, la manera mas facil de instalar es con docker aunque en hostinguer cuando elijes cambiar el sistema operativo te da la opcion de instalar ademas una app, y dentro de las apps esta n8n, lo que simplifica mucho mas el proceso ya que configura automaticamente un subdominio para n8n en el servidor de forma automática.

lo que hace hostinguer es que te deja el docker-compose.yml en la raiz el usuario root y este se inicia de manera automatica


4
Antonio Aaron Caamal Murillo
Antonio Aaron Caamal Murillo

student
•
hace 3 meses
Excelente curso Idir, me abrió la mente a automatizar varías tareas, seguiré averiguando que tanto se puede explotar esta herramienta.


5

Responder

Reportar
Lizbeth Grisales
Lizbeth Grisales

student
•
hace 3 meses
excelente inicio para este maravilloso mundo de las automatizaciones...espero ver la creación de agentes de IA nivel crack 🔥🔥🤖


5

Responder

Reportar
Juan Camilo Ortiz Villegas
Juan Camilo Ortiz Villegas

student
•
hace 3 meses
Un curso muy interesante, esperando los otros niveles!!!


5

Responder

Reportar
Marcia Cecilia Gamarra Alcalá
Marcia Cecilia Gamarra Alcalá

student
•
hace 3 meses
Idir, qué gusto haber tomado tu curso! Ha sido una experiencia de aprendizaje de primer nivel: todo está organizado con mucha claridad, explicas de forma sencilla y mantienes un ritmo que invita a seguir. Me encantó cómo cubres cada punto clave para que nadie se pierda. Gracias por tanta dedicación!


4

Responder

Reportar
Héctor Gerardo Reyes Bautista
Héctor Gerardo Reyes Bautista

student
•
hace 3 meses
Excelente primer curso de N8N. Me encantaría una serie de mini cursos con casos de uso específicos para aprovechar la herramienta. Gracias. 🙌


4

Responder

Reportar
Atenas Maini
Atenas Maini

student
•
hace 3 meses
Excelente curso Idir! Muchas gracias! Explicas muy claro cada paso.


4

Responder

Reportar
Jose Alvarez
Jose Alvarez

student
•
hace 2 meses
Muy buen curso, explica el concepto, el paso a paso y ademas con un ejemplo claro.


4

Responder

Reportar
Rodolfo Guaiquirian
Rodolfo Guaiquirian

student
•
hace 3 meses
Existe alguna diferencia entre utilizar un nuevo cerebro para el Agente IA o reutilizarlo en cada nodo. Es decir agregar un modelo a Open IA cada vez que agregamos un nodo de IA o conectarlo a uno ya existente en el nodo anterior?


4

Responder

Reportar
Idir Ouhab Meskine
Idir Ouhab Meskine

teacher
•
hace 3 meses
se puede usar el mismo para todos, en el curso se usa uno por cada agente para hacerlo mas sencillo.


2
Maikel Andres Vinces Mendoza
Maikel Andres Vinces Mendoza

student
•
hace un mes
Estamos listisimoos!




4

Responder

Reportar
Luis Gonzalez
Luis Gonzalez

student
•
hace 3 meses
encantado con el curso, dinamico, puntual y aborda muchos temas para comprender la idea, gracias por el curso


3

Responder

Reportar
Jefry Gonzalez
Jefry Gonzalez

student
•
hace 3 meses
muy buen curso, todo bien explicado.


3

Responder

Reportar
Carlos Mario Paternina Pérez
Carlos Mario Paternina Pérez

student
•
hace 3 meses
Tengo una duda relacionada a la utilización de hojas de calculo... Como diferencia el flujo que una hoja de calculo es de un ambiente de prueba o un ambiente productivo?


3

Responder

Reportar
Idir Ouhab Meskine
Idir Ouhab Meskine

teacher
•
hace 3 meses
Eso se deberá de gestionar mediante expresiones. Lo verás en el curso intermedio, pero si no sabes como funciona, la única solución es que cuando pongas el workflow en modo productivo, cambies a la hoja de cálculo que sea de producción


2
Raul Oidor
Raul Oidor

student
•
hace 3 meses
Muy buen curso, explica el concepto, el paso a paso y ademas con un ejemplo claro y util del día a día. Me gusto mas que el primer curso de n8n el cual fue muy enredado.


3

Responder

Reportar
Laura Alvarez
Laura Alvarez

student
•
hace 3 meses
Excelente curso ,muy bien explicado


3

Responder

Reportar
Jonathan Cardona
Jonathan Cardona

student
•
hace 2 meses
Muy buen curso, super práctico y una muy buena manera de tener el primer acercamiento con esta grandiosa herramienta




3

Responder

Reportar
Iván Ignacio Alvarado Diaz
Iván Ignacio Alvarado Diaz

student
•
hace un mes
Excelente curso, muy bien explicado, llevaba algunas semanas tratando de llegar a la practica con n8n con videos de youtube, y en éste curso super rapido hice una automatización, gracias, lo único que recomendaría sería quitar esos incrusivos test, uno te está prestando atención y de pronto se corta y aparece un test, es verdaderamente molesto. Pero nada, tu curso excelente.


3

Responder

Reportar
