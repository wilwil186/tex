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