# Configuración de formularios y filtros en n8n

**Curso de Automatizaciones con n8n**  
**Clase 6 de 14**

## Contexto de clases anteriores
Esta clase continúa el desarrollo del workflow iniciado en la [Clase 4](Clase4_Configuracion_Primer_Flujo_n8n.md), reemplazando datos estáticos por formularios reales y añadiendo filtros para calidad de datos. Aplica tipos de nodos explicados en la [Clase 5](Clase5_Tipos_Nodos_n8n.md), diagramas de flujo de la [Clase 3](Clase3_Simbolos_Diagramas_Flujo.md), y conceptos de automatización de las [Clases 1](Clase1_Automatizacion_Workflows_IA.md) y [2](Clase2_Flujos_Soporte_Automatizados.md). Aquí aprenderás a capturar leads reales y filtrarlos efectivamente.

## Resumen
Captura leads reales con confianza usando el form trigger nativo de n8n. Crea formularios, pruébalos, mapea datos dinámicos y filtra contactos no deseados por dominio para mantener workflows limpios.

## Crear un formulario con el form trigger de n8n
Crear un punto de entrada claro asegura que el workflow reciba datos reales desde el inicio.

### Pasos para configurar el form trigger:
1. Desactiva nodos en rojo para evitar fallos antes de agregar el trigger.
2. Añade el form trigger de n8n desde la búsqueda de nodos.
3. Usa la URL de test para pruebas y la de production para clientes.
4. Da título y descripción al formulario, ej.: “lead” y “quiero comprar tu producto”.
5. Crea campos obligatorios: nombre (texto), email (correo), mensaje (textarea).
6. Define placeholders para guiar al usuario.
7. Guarda, reordena en el canvas y elimina el trigger manual anterior.

## Campos a configurar para captar datos clave
- **Nombre**: tipo texto, obligatorio.
- **Email**: tipo email, obligatorio.
- **Mensaje**: tipo textarea, obligatorio.

## Probar el formulario con datos reales
1. Abre la URL de test y llena nombre, email y mensaje.
2. Pulsa submit y verifica que el trigger cambia a verde.
3. Confirma que la información quedó registrada correctamente.

## Mapear y validar datos en el workflow
Reemplaza valores estáticos por referencias dinámicas para que el flujo use datos reales.

### Pasos para mapear datos:
1. Abre el nodo set y elimina valores estáticos previos.
2. Arrastra nombre, email y mensaje desde el trigger a sus campos correspondientes.
3. Ejecuta de nuevo, envía datos de ejemplo y valida en el nodo if.
4. Verifica la ruta verdadera cuando el criterio se cumpla.

### Por qué usar set e if con datos dinámicos
- **Set**: mapea campos del formulario a variables del flujo.
- **If**: comprueba condiciones y enruta según el resultado.
- Beneficio: datos actualizados en tiempo real y decisiones automáticas.

## Filtrar leads por dominio con el nodo filter
Evita procesar contactos internos o no deseados añadiendo un filtro entre nodos.

### Configuración del filtro:
1. Inserta el nodo filter entre conexiones del flujo.
2. Arrastra el campo email al filtro.
3. En “value 2”, define el dominio a bloquear, ej.: @platzi.com.
4. Elige condición de texto: categoría string y opción does not contain para que no contenga ese dominio.
5. Ejecuta el workflow y verifica que los leads con ese dominio sean descartados.

### Ventajas del filtro
- Bloqueo de leads internos o de prueba.
- Datos más limpios para análisis y automatización.
- Menos ruido en integraciones posteriores como Slack o Gmail.

El siguiente paso será conectar Slack y Gmail con credenciales para operar en producción. ¿Dudas sobre el form trigger, mapeo con set o filtro por dominio? Comparte tu caso.</content>
</xai:function_call"> 

<xai:function_call name="todowrite">
<parameter name="todos">[{"content":"Improve 06.md content for coherence with previous classes","status":"completed","priority":"high","id":"improve_06"},{"content":"Remove student comments and personal names from 06.md","status":"completed","priority":"high","id":"remove_comments_06"},{"content":"Rename 06.md to a consistent name","status":"in_progress","priority":"high","id":"rename_06"}]