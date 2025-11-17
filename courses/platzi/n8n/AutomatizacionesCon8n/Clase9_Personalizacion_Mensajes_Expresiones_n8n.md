# Personalización de mensajes con expresiones en n8n

**Curso de Automatizaciones con n8n**  
**Clase 9 de 14**

## Contexto de clases anteriores
Esta clase personaliza mensajes dinámicos en el workflow, usando expresiones para insertar datos de formularios en Slack y Gmail. Construye sobre el flujo de la [Clase 4](Clase4_Configuracion_Primer_Flujo_n8n.md), agentes IA de la [Clase 8](Clase8_Integracion_Agentes_IA_n8n.md), y enrutamiento de la [Clase 7](Clase7_Configuracion_Credenciales_OAuth2_n8n.md). Aquí aprenderás a crear mensajes contextuales sin repetir trabajo manual.

## Resumen
Convierte datos de formularios en mensajes dinámicos en Slack y Gmail usando expresiones. Aprende a usar pin data, duplicar nodos, arrastrar campos y conditional switch para diferenciar “información” y “soporte”.

## Personalización de Slack con expresiones
Trabajar con expresiones permite mensajes contextuales. Arrastra campos del nodo Edit Fields (nombre, email, mensaje) al texto de Slack para avisos completos y legibles.

### ¿Qué son las expresiones y cómo insertarlas?
- Expresiones: modifican textos dinámicamente con datos del flujo.
- Arrastrar desde Edit Fields: inserta nombre, email, mensaje en el cuerpo.
- Formato legible: añade saltos de línea, guiones, etiquetas como "email:", "nombre:", "mensaje:".
- Vista previa: usa botón para ampliar y ver campos dinámicos en verde.
- Mensaje final: "Equipo, buenas noticias, tenemos un nuevo lead..." con datos del cliente.

### Estructurar mensaje claro para el equipo
- Encabezado celebratorio para nuevo lead.
- Datos clave en líneas separadas.
- Consistencia: mismo orden para email, nombre, mensaje.
- Revisión rápida con vista expandida.

## Ramas de información y soporte en Gmail
Para correos, no es lo mismo informar que dar soporte. Duplica nodo Gmail, conecta cada caso y usa conditional switch para enviar por ruta correcta.

### Activar expresiones cuando aparecen en gris
- Contexto de ejecución: expresiones grises si rama no ejecuta.
- Forzar ruta: desactiva pin data y envía caso “información” o “soporte”.
- Confirmación: expresiones pasan a verde al ejecutar ruta.

### Personalizar correos de información y soporte
- **Información**: asunto claro, contenido útil con saludo personalizado.
- Saludo dinámico: "Hola, {nombre}" arrastrando nombre desde Edit Fields.
- Enlace de referencia: incluye "n8n.io" como recurso.
- **Soporte**: asunto "le atenderemos lo antes posible" para marcar prioridad.
- Empatía y contexto: cita mensaje del cliente entre comillas.

### Duplicar nodos y separar credenciales de contenido
- Eficiencia: copia conserva credenciales válidas.
- Claridad: cada nodo ajusta solo asunto y cuerpo.
- Mantenimiento: cambios rápidos sin romper conexiones.

## Eficiencia al desarrollar con pin data y pruebas
Usa pin data para “congelar” entradas y evitar rellenar formulario en iteraciones. Cambia caso con unpin y vuelve a ejecutar. Acelera pruebas, valida switch y comprueba salida en Slack/Gmail.

### Usar pin data para acelerar pruebas
- Fija datos en nodo formulario con clic derecho y Pin.
- Ejecuta workflow sin reescribir.
- Quita pin con Unpin al cambiar caso.
- Repite validación hasta formato deseado.

### Flujos de prueba ejecutados y resultados
- **Envío a Slack**: mensaje con email, nombre, texto del cliente en líneas separadas.
- **Correo de información**: saludo dinámico y enlace "n8n.io".
- **Correo de soporte**: asunto prioritario, saludo con nombre, cita problema del cliente.

¿Ya incorporaste campos del formulario a mensajes de Slack o correos? Comparte captura con mejor versión.</content>
</xai:function_call"> 

<xai:function_call name="todowrite">
<parameter name="todos">[{"content":"Improve 09.md content for coherence with previous classes","status":"completed","priority":"high","id":"improve_09"},{"content":"Remove student comments and personal names from 09.md","status":"completed","priority":"high","id":"remove_comments_09"},{"content":"Rename 09.md to a consistent name","status":"in_progress","priority":"high","id":"rename_09"}]