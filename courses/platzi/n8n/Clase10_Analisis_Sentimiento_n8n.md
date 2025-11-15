# Análisis de sentimiento con n8n para tickets de soporte urgentes

**Curso de Automatizaciones con n8n**  
**Clase 10 de 14**

## Contexto de clases anteriores
Esta clase añade análisis de sentimiento al workflow para priorizar tickets urgentes. Construye sobre agentes IA de la [Clase 8](Clase8_Integracion_Agentes_IA_n8n.md), personalización de mensajes de la [Clase 9](Clase9_Personalizacion_Mensajes_Expresiones_n8n.md), y enrutamiento de la [Clase 7](Clase7_Configuracion_Credenciales_OAuth2_n8n.md). Aquí aprenderás a clasificar mensajes por sentimiento y rutear automáticamente a Slack o Gmail.

## Lecturas recomendadas
- Curso de OpenAI API

## Resumen
Cuando un cliente envía ticket de soporte enfadado, rapidez marca diferencia. Con n8n analiza sentimiento del mensaje y rutea: alerta urgente por Slack si negativo o correo genérico por Gmail si positivo. Reutiliza mensaje predefinido y modelo OpenAI para implementación ágil.

## Configurar análisis de sentimiento en n8n
Con flujo automatizado, inserta nodo que clasifique mensaje del formulario por sentimiento y active acciones distintas.

### Ubicar nodo de sentimiento
- Localiza zona del flujo que reacciona a soporte y haz zoom.
- Coloca ratón sobre línea que une nodos y pulsa botón Más.
- Elige AI y selecciona nodo específico para análisis de sentimiento, no AI agent general.
- Reordena para limpiar conexiones e integrar bien.

### Analizar y mapear campos
- Define “qué analizar”: mensaje del cliente.
- Entra a Edit Fields, toma campo mensaje y arrástralo al nodo.
- Recuerda: mapeo es expresión, toma dinámicamente texto del formulario.

### Categorías y modelo usar
- En Sentiment Categories aparecen tres por defecto: positiva, neutral, negativa.
- Conserva solo dos: positiva y negativa, eliminando neutral para simplificar decisión.
- Asigna “cerebro” al nodo: reutiliza modelo OpenAI para dejar de estar en rojo.
- Prueba nodo con Play para ejecutar aislado y validar salida antes de enviar correos.

## Enviar Slack urgente o correo Gmail genérico
Tras clasificar sentimiento, flujo bifurca en dos ramas. Decide canal según estado emocional del cliente.

### Decidir entre Slack y Gmail por sentimiento
- **Rama negativa**: envía aviso urgente por Slack al equipo soporte.
- **Rama positiva**: mantiene correo genérico por Gmail con mensaje predefinido.
- Verifica mensaje genérico conectado a rama positiva para no romper flujo existente.

### Duplicar y ajustar nodo Slack
- Duplica nodo Slack existente con clic derecho para reaprovechar configuraciones.
- Conéctalo a rama negativa y reordena flujo.
- Edita texto mensaje para urgencia: “Por favor, equipo. Un cliente tiene problemas y está enfadado.”.
- Reutiliza variables previas: email, nombre, mensaje del cliente para contexto completo.

### Crear canal Soporte y cambiar Channels
- Crea nuevo grupo en Slack llamado “Soporte”.
- En nodo, abre Channels y selecciona “Soporte” para redirigir alerta al canal correcto.
- Guarda y prueba: ahora tendrás canal para leads y otro para soporte.

## Habilidades y conceptos clave aplicados
Estos consolidan flujo sensible al cliente, manteniendo orden y trazabilidad.

### Conceptos que consolidan automatización
- **Análisis de sentimiento**: clasificación mensaje cliente como positivo/negativo para ruteo automático.
- **Ruteo condicional**: ramas positiva/negativa activan Slack o Gmail según caso.
- **Reutilización de nodos**: duplicar Slack acelera configuración.
- **Mapeo de datos con expresiones**: usar Edit Fields para arrastrar campo mensaje.
- **Optimización de categorías**: simplificar Sentiment Categories a dos clases para decisiones claras.
- **Selección de modelo**: asignar OpenAI como cerebro del nodo para funcionar.
- **Pruebas incrementales**: ejecutar con Play solo nodo análisis antes de notificar o enviar correos.
- **Gestión de canales**: configurar Channels para enviar a “Soporte” en vez de “ventas” o “sellers”.

¿Te animas a añadir nueva categoría y decidir: alerta por Slack o correo genérico por Gmail? Comparte captura de flujo.</content>
</xai:function_call"> 

<xai:function_call name="todowrite">
<parameter name="todos">[{"content":"Improve 10.md content for coherence with previous classes","status":"completed","priority":"high","id":"improve_10"},{"content":"Remove student comments and personal names from 10.md","status":"completed","priority":"high","id":"remove_comments_10"},{"content":"Rename 10.md to a consistent name","status":"in_progress","priority":"high","id":"rename_10"}]