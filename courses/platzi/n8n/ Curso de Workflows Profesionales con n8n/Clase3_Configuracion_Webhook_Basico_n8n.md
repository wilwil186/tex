# Configuración de Webhook Básico en n8n

**Clase 3 de 16 • Curso de Workflows Profesionales con n8n**

## Resumen
Un workflow simple pero bien estructurado en n8n puede ser tu base para automatizaciones sólidas: recibe una petición, valida los datos y responde de forma controlada. Aquí se explica cómo crear un webhook, configurar su método HTTP, probar con JSON, extraer campos con set o edit fields, validar con if y responder con respond to webhook. Además, verás trucos como pin data y el uso de expresiones JavaScript para añadir lógica, manteniendo la coherencia con los prerrequisitos técnicos de APIs, HTTP y JSON discutidos en la Clase 2.

## Lecturas Recomendadas
- [Curso de Automatizaciones Low-Code con n8n](enlace al curso)
- [Trabajando con JSON](enlace)
- [ReqBin: Online REST & SOAP API Testing Tool](https://reqbin.com/)

## ¿Qué es un Webhook y Cómo Configurarlo en n8n?
Un webhook es una URL que expone tu workflow al exterior, permitiendo que aplicaciones externas activen el flujo mediante peticiones HTTP. En n8n, comienza creando un nuevo workflow, renombrándolo con un nombre claro (como "Asistente Interno") y añadiendo el nodo trigger de tipo "Webhook". Esto establece el punto de entrada para recibir datos externos, alineándose con los conceptos de APIs y métodos HTTP de la Clase 2.

## ¿Cómo Elegir Método HTTP y Path en el Webhook?
- **Método HTTP**: Selecciona según la operación. Para enviar datos (como en un asistente), usa POST. Otros métodos como GET son para recuperar información.
- **Path**: Define un path legible en lugar del aleatorio generado, ej. "/asistente-interno". La URL completa incluye el dominio de n8n, el segmento de webhook y tu path personalizado.

## ¿Cuándo Usar Test URL o Production URL?
- **Test URL**: Ideal para desarrollo. Se activa pulsando "Listen for test events" o ejecutando el workflow manualmente.
- **Production URL**: Para entornos reales. Activa el workflow con el botón hasta que esté verde. Mantén producción apagado durante desarrollo para evitar ejecuciones no deseadas y costos innecesarios.

## ¿Cuáles son los Modos de Respuesta y Streaming?
- **Acción por defecto**: Respuesta inmediata al recibir la petición.
- **Cuando el último nodo haya acabado**: Espera al final del flujo completo.
- **Usar otro nodo para contestar**: Selecciona "Respond to Webhook" para responder desde un nodo específico, controlando el momento exacto.
- **Streaming**: Envía datos a medida que se generan, útil para integraciones con agentes de IA que requieren respuestas progresivas.

## ¿Cómo Probar y Responder Solicitudes HTTP con Control?
Probar de forma segura evita errores comunes. Usa herramientas como Postman o ReqBin para enviar un JSON con campos como "usuario" y "mensaje". Envía la petición a la Test URL y observa la respuesta en n8n, asegurando que los datos se procesen correctamente según los métodos HTTP y JSON de la Clase 2.

## ¿Cómo Escuchar Eventos de Test y Evitar Errores 4xx?
- Copia la Test URL en tu herramienta de pruebas.
- Activa "Listen for test events" o ejecuta el workflow antes de enviar.
- Si ves "The request of hook is not registered", significa que n8n no estaba escuchando; siempre activa el modo test primero.

## ¿Qué Revisar en Esquema y Body del Request?
- Abre el nodo Webhook y usa la vista "Esquema" para ver cabeceras y datos recibidos.
- Identifica el body con campos como "usuario" y "mensaje".
- Si no hay respuesta inicial, agrega un nodo "Respond to Webhook" y vuelve a ejecutar para confirmar el flujo.

## ¿Cómo Responder con JSON y Usar Expresiones?
Configura "Respond to Webhook" para enviar JSON estructurado:
- **Caso exitoso**: Estado "recibido" y usuario insertado con expresiones JavaScript (ej. `{{ $json.body.usuario }}`).
- **Caso de error**: Estado "error" y detalle "el mensaje está vacío".
Duplica nodos con clic derecho o atajos Ctrl+C/V para reutilizar configuraciones.

## ¿Cómo Validar y Transformar Datos Antes de Responder?
Convertir y validar datos controla el flujo. Usa "Set" o "Edit Fields" para extraer campos necesarios y "If" para ramificar basado en condiciones, aplicando validaciones para mantener la mantenibilidad discutida en la Clase 1.

## ¿Cómo Extraer y Renombrar Campos con Set o Edit Fields?
- Arrastra campos desde el body (ej. usuario, mensaje).
- Define tipos: string, number, boolean, object o array.
- Renombra eliminando prefijos como "body." para claridad (ej. "usuario" en lugar de "body.usuario").
- Ejecuta y valida que el output contenga solo los datos necesarios.

## ¿Cómo Congelar Datos con Pin Data para Iterar Más Rápido?
Usa "Pin Data" para fijar datos en un nodo, evitando reenviar peticiones durante pruebas. Activa/desactiva con clic derecho en el nodo > "Pin". Atajo: tecla P. Esto acelera el desarrollo sin afectar el flujo real.

## ¿Cómo Validar con If que el Mensaje No Esté Vacío?
- Añade el nodo "If" y arrastra el campo "mensaje".
- Selecciona condición "no está vacío".
- Rama verdadera: continúa y responde con éxito.
- Rama falsa: responde con error y detalle claro, previniendo fallos como se enfatizó en la Clase 1.

¿Listo para un reto rápido? Vuelve a "Edit Fields" y crea un campo "prioridad". Usa expresiones JavaScript: si el mensaje contiene "urgente", asigna "alta"; de lo contrario, "baja". Prueba, toma una captura y compártela en los comentarios.

¿Tienes dudas sobre webhook, respond to webhook, pin data o if? Deja tu pregunta y comenta cómo estructuraste tu JSON y expresiones.