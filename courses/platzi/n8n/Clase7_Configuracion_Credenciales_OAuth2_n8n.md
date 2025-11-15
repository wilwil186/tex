# Configuración de credenciales OAuth 2 en n8n para Slack y Gmail

**Curso de Automatizaciones con n8n**  
**Clase 7 de 14**

## Contexto de clases anteriores
Esta clase completa el workflow iniciado en la [Clase 4](Clase4_Configuracion_Primer_Flujo_n8n.md) conectando credenciales reales para Slack y Gmail. Aplica tipos de nodos de la [Clase 5](Clase5_Tipos_Nodos_n8n.md), formularios y filtros de la [Clase 6](Clase6_Configuracion_Formularios_Filtros_n8n.md), y conceptos de automatización de las [Clases 1](Clase1_Automatizacion_Workflows_IA.md) y [2](Clase2_Flujos_Soporte_Automatizados.md). Aquí aprenderás a activar nodos y autenticar con OAuth 2 para flujos productivos.

## Resumen
Configurar credenciales en n8n es clave para automatizar con confianza. Aquí verás paso a paso cómo activar nodos, autenticar con OAuth 2, y verificar envíos por Slack y Gmail, dejando un flujo funcional.

## ¿Qué es una credencial en n8n y por qué importa?
Una credencial es el permiso para conectarse con aplicaciones de terceros como Slack o Gmail, enviando mensajes con autorización segura. n8n guarda la autorización y la reutiliza.

- Credencial: autorización que habilita conexiones externas.
- OAuth 2: método recomendado por seguridad y control de permisos.
- Activar nodos: requisito previo para integraciones.

## ¿Por qué usar OAuth 2?
Es la opción más recomendada por su seguridad.

- Permite iniciar sesión y aprobar permisos con Allow guiado.
- Muestra estados de conexión como Successful y “conectado”.

## Habilidades prácticas aplicadas
- Activar nodos con clic derecho y doble clic para credentials.
- Crear credenciales con Create new credentials y seleccionar OAuth 2.
- Verificar resultados: “OK, true”, mensajes en Slack y correos recibidos.

## Conectar Slack con OAuth 2 y elegir canal dinámicamente
1. Habilitar nodo Slack: clic derecho “activar”, doble clic y credentials.
2. Si no hay credencial, crear con OAuth 2, aprobar permisos con Allow; aparece Successful y “conectado”.
3. Iniciar conexión: Connect y aprobar en cuenta correcta de Slack.
4. Confirmar estado: pantalla Successful sin errores.
5. Elegir canal dinámico: en “lista”, Select a channel muestra disponibles, escoger “Sellers”.

## Validar envío a Slack
1. Ejecutar flujo con Execute workflow y abrir formulario.
2. Completar datos: nombre “Idir”, correo “idir.idir.com”, mensaje “quiero una demo”, submit.
3. Revisar nodo Slack: estado “OK, true”.
4. Verificar en app: en “Sellers” aparece “nuevo lead”.

## Conectar Gmail con OAuth 2 y comprobar envío
1. Con nodo Gmail: activar, doble clic, Create new credentials, OAuth 2, autenticar con Sign in with Google.
2. Si varias cuentas, elegir correcta, marcar permisos; n8n muestra “conectado”.
3. Autenticar con Google: seleccionar cuenta y aprobar permisos.
4. Confirmar conexión: vuelta al flujo con “conectado” sin errores.
5. Preparar prueba: ingresar correo verificable.

## Testear dos escenarios: lead y no lead
- **Escenario 1 (lead)**: “Idir”, “idir.idir.com”, “quiero una demo” → mensaje en Slack “nuevo lead”.
- **Escenario 2 (no lead)**: “Idir”, “promptandplay@gmail.com”, “no quiero su producto” → correo “gracias por su interés”.

Evidencias de éxito: estado “OK, true” y confirmación en bandeja.

## Datos que confirman flujo productivo
- Ambos nodos activados y conectados con OAuth 2.
- Canales listados automáticamente desde Slack y envío validado en “Sellers”.
- Correo “gracias por su interés” recibido en Gmail.

¿Te animas a explorar otros nodos como Telegram, Outlook o Teams? Conéctalos y comparte captura.</content>
</xai:function_call"> 

<xai:function_call name="todowrite">
<parameter name="todos">[{"content":"Improve 07.md content for coherence with previous classes","status":"completed","priority":"high","id":"improve_07"},{"content":"Remove student comments and personal names from 07.md","status":"completed","priority":"high","id":"remove_comments_07"},{"content":"Rename 07.md to a consistent name","status":"in_progress","priority":"high","id":"rename_07"}]