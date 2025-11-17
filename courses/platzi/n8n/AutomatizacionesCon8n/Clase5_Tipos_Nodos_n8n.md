# Tipos de nodos en n8n para automatizar flujos de trabajo

**Curso de Automatizaciones con n8n**  
**Clase 5 de 14**

## Contexto de clases anteriores
Esta clase profundiza en los componentes básicos de n8n, explicando los tipos de nodos utilizados en el workflow creado en la [Clase 4](Clase4_Configuracion_Primer_Flujo_n8n.md). Aplica conceptos de automatización introducidos en la [Clase 1](Clase1_Automatizacion_Workflows_IA.md), flujos de soporte en la [Clase 2](Clase2_Flujos_Soporte_Automatizados.md) y diagramas de flujo en la [Clase 3](Clase3_Simbolos_Diagramas_Flujo.md). Aquí aprenderás a construir automatizaciones robustas conectando nodos inteligentes.

## Resumen
Aprende a construir automatizaciones robustas con n8n conectando bloques llamados nodos. Explora cinco tipos clave —trigger, acción, condición, transformación de datos, control y espera— para crear workflows eficientes que funcionen solos.

## Estructura de un workflow en n8n
Un flujo en n8n se crea conectando nodos con funciones específicas. La regla básica: sin un trigger, no hay workflow. Desde ahí, las acciones se encadenan, las decisiones se toman con condiciones y los datos se preparan.

- n8n conecta nodos con funciones concretas.
- Un trigger inicia el flujo automáticamente.
- El resto de nodos ejecutan, deciden, transforman y controlan tiempos.
- Combinar nodos ofrece flexibilidad total para automatizar tareas.

## Tipos de nodos clave en n8n
Dominar estos tipos acelera el aprendizaje. Cada uno responde a preguntas clave: cuándo iniciar, qué hacer, por dónde seguir.

### Nodos trigger
Inician el flujo sin intervención manual, detectando eventos y arrancando el proceso.

- **Formularios enviados**: inicio automático al enviar un formulario.
- **Correos recibidos**: arranque al llegar un email.
- **Hora específica**: ejecución programada a una hora concreta.

### Nodos de acción
Ejecutan tareas concretas una vez iniciado el flujo, realizando la operación necesaria.

- Enviar un correo a una persona o equipo.
- Crear una fila en una hoja de cálculo.
- Enviar un mensaje a Slack para notificar avances.

### Nodos de condición
Permiten bifurcar caminos según reglas, usando nodos como IF y SWITCH para decisiones lógicas.

- Si el mensaje dice "demo", sigue por la ruta A.
- Si el correo contiene "@miempresa.com", aplica la regla interna.
- Usa IF para verdadero/falso y SWITCH para múltiples casos.

### Nodos de transformación de datos
Sirven para limpiar, adaptar y estandarizar información antes de usar. El más usado es edit fields.

- Renombrar campos para consistencia.
- Cambiar formatos de fechas o números.
- Dejar datos listos para pasos posteriores.
- Habilidades ejercitadas: normalización de datos, mapeo de campos y preparación para integración.

### Nodos de control y espera
Gestionan cuándo y cuántas veces ejecutar, y qué hacer si algo falla. Usa wait, loop over items y error trigger.

- Esperar un día antes de una acción con wait.
- Repetir una acción para cada elemento de una lista con loop over items.
- Capturar errores y reaccionar con error trigger.
- Habilidades desarrolladas: control de flujos, manejo de errores y orquestación de procesos.

En conjunto, estos cinco tipos permiten construir casi cualquier flujo, combinándolos para automatizar con confianza. ¿Qué automatización te gustaría crear primero?