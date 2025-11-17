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