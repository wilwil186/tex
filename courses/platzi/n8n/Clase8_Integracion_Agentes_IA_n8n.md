# Integración de agentes de IA en n8n para clasificar leads automáticamente

**Curso de Automatizaciones con n8n**  
**Clase 8 de 14**

## Contexto de clases anteriores
Esta clase eleva el workflow a inteligencia artificial, integrando agentes IA para clasificar leads sin palabras clave explícitas. Construye sobre el flujo de la [Clase 4](Clase4_Configuracion_Primer_Flujo_n8n.md), tipos de nodos de la [Clase 5](Clase5_Tipos_Nodos_n8n.md), formularios de la [Clase 6](Clase6_Configuracion_Formularios_Filtros_n8n.md), credenciales de la [Clase 7](Clase7_Configuracion_Credenciales_OAuth2_n8n.md), y conceptos de IA de las [Clases 1](Clase1_Automatizacion_Workflows_IA.md) y [2](Clase2_Flujos_Soporte_Automatizados.md). Aquí aprenderás a categorizar mensajes en info, demo o soporte con precisión.

## Lecturas recomendadas
- https://platform.openai.com/
- Curso de OpenAI API

## Resumen
Convierte tu automatización en inteligencia aplicada: integra un agente de IA en n8n, conecta OpenAI con credentials y enruta mensajes con switch para gestionar leads precisos. Aprende a categorizar mensajes, resolver errores de referencias y validar resultados en Slack y Gmail.

## Integrar un agente de IA en n8n para clasificar leads
Configura un nodo de agente IA tras el filtro para entender mensajes sin depender de palabras clave. Usa AI agent y define system message para estandarizar salida.

### Pasos para integrar:
1. Inserta nodo IA tras filtro usando botón sumar en línea verde.
2. Selecciona AI agent y conecta entrada con mensaje del lead desde source o prompt definiendo below.
3. Añade mensaje de sistema en add options > system message para orientar tarea.
4. Conecta modelo dando clic al botón de modelo y elige OpenAI.

## Instrucción en system message para categorías consistentes
Especifica objetivo y formato de salida para evitar ambigüedades.

- Indica: “cataloga este mensaje en una de estas opciones: info, demo y soporte. La respuesta debe ser una categoría en minúscula.”
- Beneficio: salida uniforme y fácil de enrutar.

## Conectar OpenAI con credentials y API key
Activa modelo desde OpenAI con credenciales seguras.

### Pasos:
1. Ve a credentials y crea nueva si no existe.
2. Desde dashboard de OpenAI, entra a API keys y presiona create new secret key.
3. Copia API key y pégala en n8n.
4. Elige modelo: GPT-4-1 mini suficiente para clasificar leads.

## Probar workflow con lead real
Ejecuta workflow y usa mensajes naturales que impliquen intención.

- Prueba con: “muéstrame tu producto” para validar ruta de demo.
- Guarda, ejecuta y verifica que nodo ya no esté en rojo.

## Depurar nodos en rojo y corregir referencias
Tras incorporar agente, if y Gmail quedan en rojo por referenciar campos antiguos. Apunta a salida del agente (output) y email correcto.

### Correcciones:
1. En if: reemplaza “mensaje del lead” por output del agente (categoría detectada).
2. En Gmail: abre table view, identifica nodo con email válido, pulsa edit fields y arrastra campo correcto. Borra referencias anteriores.
3. Vuelve a probar con mensaje de soporte (ej.: “tu producto falla mucho, necesito ayuda”) usando correo real para validar envío.
4. Confirma resultados: mensaje en Slack para demo y correo enviado para soporte. Todo en verde.

## Validar en Slack y correo que rutas funcionan
- Revisa canal de Slack tras enviar solicitud de demo.
- Verifica bandeja de entrada después de caso de soporte.
- Si falla: revisa referencias, arrastres de campos y guarda cambios.

## Reemplazar if por switch para enrutar info, demo y soporte
Para tres categorías, switch es más claro que if. Crea reglas de enrutamiento con nombres descriptivos.

### Pasos:
1. Inserta switch entre agente y siguiente paso.
2. Arrastra output del agente al campo valor del switch.
3. Crea reglas con add routing rule para: demo, info y soporte.
4. Usa rename output para nombrar salidas como: demo, info, soporte.
5. Elimina if y conecta: demo → Slack; info/soporte → Gmail.
6. Ordena flujo, guarda y ejecuta pruebas con mensajes reales.

## Habilidades desarrolladas
- Diseño de flujos en n8n: ubicación de nodos y orden visual.
- Ingeniería de prompts: system message para salidas estandarizadas.
- Integración con OpenAI: gestión de credentials y API key.
- Depuración: lectura de nodos en rojo, corrección de referencias, table view y edit fields.
- Enrutamiento avanzado: switch, add routing rule y rename output.
- Validación end-to-end: pruebas en workflow, verificación en Slack y Gmail.

¿Te gustaría variantes del system message o personalizar respuestas con expresiones según intención del cliente? Comparte casos a automatizar.</content>
</xai:function_call"> 

<xai:function_call name="todowrite">
<parameter name="todos">[{"content":"Improve 08.md content for coherence with previous classes","status":"completed","priority":"high","id":"improve_08"},{"content":"Remove student comments and personal names from 08.md","status":"completed","priority":"high","id":"remove_comments_08"},{"content":"Rename 08.md to a consistent name","status":"in_progress","priority":"high","id":"rename_08"}]