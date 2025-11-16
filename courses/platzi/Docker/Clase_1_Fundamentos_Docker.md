# Clase 1: Fundamentos de Docker y Contenedores para Desarrolladores

**Curso de Docker: Fundamentos**  
**Clase 1 de 19**

## Resumen
Docker se ha convertido rápidamente en una herramienta esencial para gestionar y publicar soluciones de software mediante contenedores. La esencia y punto fuerte de Docker radica en su capacidad para aislar aplicaciones, asegurando que estas funcionen de manera consistente en diferentes sistemas operativos o entornos, resolviendo así la clásica situación de "en mi máquina sí funciona". Puedes encontrar el repositorio de este curso en https://github.com/platzi/curso-de-docker-fundamentos, donde cada rama contiene los archivos que se usarán al final del curso.

## ¿Qué es realmente un contenedor en Docker?
Aunque pueda confundirse con máquinas virtuales, un contenedor es algo distinto: es un espacio aislado donde empaquetas toda tu solución, incluyendo dependencias y configuraciones. Esto permite que el proyecto, al transportarse de un lugar a otro, funcione exactamente igual sin importar factores externos, como el sistema operativo o ambiente.

- **Aislamiento**: Los contenedores encapsulan una aplicación y su entorno, asegurando que las aplicaciones se ejecuten de manera independiente y sin interferencias entre sí. [00:00].
- **Ligereza**: A diferencia de las máquinas virtuales, los contenedores comparten el mismo sistema operativo subyacente, lo que los hace más eficientes en términos de recursos. [00:00].
- **Portabilidad**: Los contenedores pueden ejecutarse en cualquier sistema que soporte Docker, garantizando que el software funcione de la misma manera en desarrollo, pruebas y producción. [00:00].

Gracias al docker daemon, o el corazón de Docker, puedes gestionar eficazmente redes, volúmenes e imágenes previas necesarias para crear nuevos contenedores.

## ¿Qué diferencia a Docker de otros conceptos tecnológicos?
A menudo se mezclan términos como microservicios, Kubernetes y Docker, pensando equivocadamente que son sinónimos. En realidad, estas tecnologías tienen definiciones y aplicaciones particulares que, aunque participen integradas en ciertos procesos, presentan diferencias considerables entre ellas.

- **Docker**: Te permite específicamente crear y gestionar contenedores individuales. [00:00].
- **Kubernetes**: Se centra en la gestión, orquestación y despliegue de múltiples contenedores dentro de infraestructuras más grandes, proporcionando capacidades avanzadas de automatización, escalabilidad y gestión de recursos. [00:00].
- **Microservicios**: Describen un estilo arquitectónico en el que las aplicaciones se componen de módulos pequeños e independientes que se comunican entre sí. [00:00].

## ¿Qué conocimientos previos facilitan el aprendizaje de Docker?
Tener experiencia en bash o manejo de terminal y sistemas operativos basados en Linux facilitará mucho la transición al uso de Docker y sus contenedores. Experimentar comandos directamente en una terminal te dará confianza y hará que usar Docker sea más sencillo y natural.

- **Conocimientos recomendados**: Bash, terminal, sistemas Linux. [00:00].
- **Beneficio**: Comprender cómo Docker encapsula todo y evita problemas de compatibilidad. [00:00].

La idea es comprender progresivamente qué es exactamente un contenedor, cómo funciona dentro del entorno Docker y cómo aprovecharlo para tus soluciones de software. Así, serás capaz de integrarlo y aplicarlo efectivamente en tus propios desarrollos.

## Beneficios y características de Docker
Docker ofrece múltiples ventajas que lo hacen esencial en el desarrollo moderno de software.

- **Consistencia**: Garantiza que las aplicaciones se ejecuten de manera uniforme en diferentes entornos, eliminando problemas de "funciona en mi máquina". [00:00].
- **Escalabilidad**: Facilita la escalabilidad horizontal al permitir la creación rápida de múltiples instancias de contenedores. [00:00].
- **Eficiencia en Recursos**: Los contenedores consumen menos recursos en comparación con las máquinas virtuales, ya que no requieren un sistema operativo completo. [00:00].
- **Desarrollo Ágil**: Permite a los desarrolladores crear y destruir entornos de desarrollo rápidamente, facilitando pruebas y desarrollo continuos. [00:00].
- **Aislamiento**: Cada contenedor opera de manera aislada, mejorando la seguridad y reduciendo conflictos entre aplicaciones. [00:00].
- **Integración Continua y Despliegue Continuo (CI/CD)**: Se integra perfectamente con herramientas de CI/CD, permitiendo la automatización del proceso de construcción, prueba y despliegue. [00:00].

## ¿Quién te guía en este curso?
Amin Espinoza, instructor de Platzi, te acompañará en este curso para que aprendas Docker de manera efectiva. Si tienes dudas, puedes compartirlas para resolverlas.

## ¿Qué vas a lograr paso a paso?
- Comprender los fundamentos de Docker y los contenedores. [00:00].
- Diferenciar Docker de otras tecnologías como Kubernetes y microservicios. [00:00].
- Aplicar Docker en tus propios proyectos para mejorar la consistencia y eficiencia. [00:00].
- Integrar Docker en flujos de desarrollo modernos. [00:00].



Oscar Danilo Guzmán Villanueva
Oscar Danilo Guzmán Villanueva

student
•
hace un año
Docker es una plataforma de software que permite crear, probar y desplegar aplicaciones rápidamente en entornos aislados llamados contenedores. Estos contenedores agrupan el código de una aplicación junto con todas sus dependencias y configuraciones necesarias para que funcione de manera consistente en diferentes entornos, desde una máquina de desarrollo hasta servidores en producción.

### Principales Características de Docker

1. **Contenedores**:

- **Aislamiento**: Los contenedores encapsulan una aplicación y su entorno, asegurando que las aplicaciones se ejecuten de manera independiente y sin interferencias entre sí.

- **Ligereza**: A diferencia de las máquinas virtuales, los contenedores comparten el mismo sistema operativo subyacente, lo que los hace más eficientes en términos de recursos.

2. **Portabilidad**:

- Los contenedores pueden ejecutarse en cualquier sistema que soporte Docker, garantizando que el software funcione de la misma manera en desarrollo, pruebas y producción.

3. **Imagen de Docker**:

- Una imagen es una plantilla de solo lectura utilizada para crear contenedores. Incluye todo lo necesario para ejecutar una aplicación: código, dependencias, bibliotecas, configuraciones, etc.

- Las imágenes se pueden almacenar y compartir a través de registros de imágenes, como Docker Hub.

4. **Orquestación**:

- Herramientas como Docker Compose permiten definir y ejecutar aplicaciones multi-contenedor.

- Kubernetes es una plataforma de orquestación más avanzada que gestiona la implementación, escalado y operación de aplicaciones contenedorizadas.

### Beneficios de Docker

1. **Consistencia**:

- Garantiza que las aplicaciones se ejecuten de manera uniforme en diferentes entornos, eliminando problemas de "funciona en mi máquina".


2. **Escalabilidad**:

- Facilita la escalabilidad horizontal al permitir la creación rápida de múltiples instancias de contenedores.


3. **Eficiencia en Recursos**:

- Los contenedores consumen menos recursos en comparación con las máquinas virtuales, ya que no requieren un sistema operativo completo.

4. **Desarrollo Ágil**:

- Permite a los desarrolladores crear y destruir entornos de desarrollo rápidamente, facilitando pruebas y desarrollo continuos.

### Casos de Uso de Docker

1. **Desarrollo y Pruebas**:

- Facilita la creación de entornos de desarrollo consistentes y la ejecución de pruebas automatizadas en entornos idénticos al de producción.

2. **Despliegue de Aplicaciones**:

- Simplifica el proceso de despliegue, permitiendo la entrega continua y la implementación rápida de aplicaciones.

3. **Microservicios**:

- Docker es ideal para arquitecturas de microservicios, donde cada servicio puede ejecutarse en su propio contenedor, facilitando el desarrollo, despliegue y escalado independientes.

Docker ha transformado la manera en que se desarrollan, despliegan y gestionan las aplicaciones, ofreciendo una solución eficiente y flexible que responde a las necesidades modernas de agilidad y escalabilidad en el desarrollo de software.


17

Responder

Reportar
Gilberto Pérez Garrido
Gilberto Pérez Garrido

student
•
hace un año
no entiendo porqué quitaron el anterior, estaba más completo


12

Responder

Reportar
Sergio de Jesús Huesca Nieva
Sergio de Jesús Huesca Nieva

student
•
hace 10 meses
coincido, tome todos los anteriores y me quedo la duda de por que sacaron un nuevo curso si los anteriores eran excelentes


4
Will Lainez
Will Lainez

student
•
hace 7 meses
Pregunta, no tienes el link de alguna clase? porque generalmente yo guardo los link y las clases aun estan ahi con los mismo link, no las borran solo que el acceso ya no es facil.


4

Ver 2 respuestas más
Juan Manuel Hincapié
Juan Manuel Hincapié

student
•
hace 2 años
Los siguientes conceptos son diferentes aunque en una aplicación real pueden usarse todos para desplegar tus aplicaciones:

- Microservicios: Son una forma de diseñar y construir aplicaciones que promueve la modularidad, la independencia, la escalabilidad y la flexibilidad

- Kubernetes: Es una herramienta poderosa para la gestión de contenedores y aplicaciones, que proporciona capacidades avanzadas de automatización, escalabilidad y gestión de recursos.

- Docker: Es una herramienta que te permite gestionar y publicar contenedores.



- Contenedores: Permiten que cualquier persona ejecute tu aplicación en su dispositivo sin importar el sistema operativo, el lenguaje de programación, etc.


8

Responder

Reportar
Iván Andrés Pineda Salazar
Iván Andrés Pineda Salazar

student
•
hace 2 años
El primer curso de Docker que estoy tomando, espero aprender mucho y comenzar a utilizar Docker en mis proyectos.


4

Responder

Reportar
Harry Oswaldo Martel Benites
Harry Oswaldo Martel Benites

student
•
hace 2 años
Es el curso que esperaba. ¡Empecesmos!


4

Responder

Reportar
Amin Espinoza
Amin Espinoza

teacher
•
hace 2 años
¡Adelante! Si tienes alguna duda acá estamos para resolverla!


2
Miguel Giraldo Duque
Miguel Giraldo Duque

student
•
hace un año
Bueno ! vamos a aprender , siempre quise entender y con este curso lo logramos💪

¿Qué es Docker?

Docker es una plataforma de contenedores que nos permite encapsular nuestro código en una "caja" que puede ser compartida con otros desarrolladores. Estos desarrolladores podrán ejecutar el código en sus propias máquinas de forma eficiente y sin problemas de compatibilidad.

Docker surgió con el propósito de resolver un problema común: que el código que funciona en nuestro entorno local no siempre se ejecuta de la misma manera en los equipos de otras personas, debido a diferencias en las configuraciones o dependencias. Docker garantiza que el código funcione de manera consistente sin importar el entorno en el que se ejecute.


4

Responder

Reportar
Juan Manuel Hincapié
Juan Manuel Hincapié

student
•
hace 2 años
Los siguientes conceptos son diferentes aunque en una aplicación real pueden usarse todos para desplegar tus aplicaciones:

- Microservicios: Son una forma de diseñar y construir aplicaciones que promueve la modularidad, la independencia, la escalabilidad y la flexibilidad

- Kubernetes: Es una herramienta poderosa para la gestión de contenedores y aplicaciones, que proporciona capacidades avanzadas de automatización, escalabilidad y gestión de recursos.

- Docker: Es una herramienta que te permite gestionar y publicar contenedores.

![](https://imgur.com/m9WZ8In)

- Contenedores: Permiten que cualquier persona ejecute tu aplicación en su dispositivo sin importar el sistema operativo, el lenguaje de programación, etc.


2

Responder

Reportar
Michael Nicolas De La Cruz Sanchez
Michael Nicolas De La Cruz Sanchez

student
•
hace un año
¿Qué es Docker?

Imagina que tienes una caja mágica donde puedes guardar todas las piezas necesarias para que un juego funcione, como los juguetes, el manual, las baterías, y las reglas del juego. Luego, puedes llevar esta caja a cualquier parte, abrirla, y el juego funcionará siempre igual, sin importar si estás en la casa de tu amigo, en la escuela, o en otro país. ¡Eso es Docker!

Docker es una herramienta que guarda aplicaciones (como si fueran juegos) en contenedores, para que puedas llevarlos de un lugar a otro y asegurarte de que siempre funcionen bien, sin preocuparte por si el lugar donde los usas es diferente.

¿Qué es un contenedor?

Ahora imagina que dentro de esa caja mágica (el contenedor) guardamos:

El juguete principal (la aplicación o programa que queremos usar).
Las baterías (librerías y herramientas necesarias para que funcione).
Las reglas del juego (cómo debe ejecutarse el programa).
Un contenedor es como esa caja que tiene todo lo necesario para que un programa funcione sin problemas, sin importar en qué computadora lo uses. Esto evita que tengas problemas porque a una computadora le falta algo o porque tiene algo diferente.

Ejemplo práctico

Piensa en tu videojuego favorito. Si tratas de instalarlo en una computadora vieja, puede que no funcione porque no tiene la versión correcta del sistema. Con Docker, metemos ese videojuego y todo lo que necesita (controladores, herramientas, etc.) dentro de un contenedor. Ahora puedes abrir ese contenedor en cualquier computadora, ¡y el juego funcionará perfecto, como en la tuya!

Así que Docker hace que mover y ejecutar aplicaciones sea tan fácil como llevar una caja con juguetes de un lugar a otro.


2

Responder

Reportar
Joaquin Andres Vargas Villalobos
Joaquin Andres Vargas Villalobos

student
•
hace 8 meses
Docker es una plataforma que permite crear, ejecutar y gestionar aplicaciones dentro de contenedores, que son entornos ligeros, portátiles y aislados. Estos contenedores incluyen todo lo necesario para que una aplicación funcione (código, dependencias, configuraciones), asegurando que se ejecute de manera consistente en cualquier entorno. Es más rápido y eficiente que las máquinas virtuales, ideal para desarrollo, despliegue y escalado de aplicaciones.


2

Responder

Reportar
Andres de Jesus Romo Quintero
Andres de Jesus Romo Quintero

student
•
hace 2 años
Hola a todos, vamos empezando este nuevo curso, Gracias Platzi por este curso.


2

Responder

Reportar
Amin Espinoza
Amin Espinoza

teacher
•
hace 2 años
¡Y gracias a tí por verlo! Ojalá aprendas mucho!


2
Diego Alejandro Pinto Moreno
Diego Alejandro Pinto Moreno

student
•
hace un año
Hola vengo del curso con Curso de Python: PIP y Entornos Virtuales por que no pude hacer correr docker


2

Responder

Reportar
Ivan Camilo Buitrago Buitrago
Ivan Camilo Buitrago Buitrago

student
•
hace un año
Por Qué Deberías Aprender Docker

1. Portabilidad

Docker encapsula aplicaciones y sus dependencias en contenedores, haciendo que puedan ejecutarse de manera consistente en cualquier entorno, ya sea en desarrollo, pruebas o producción.

2. Eficiencia de Recursos

Los contenedores de Docker comparten el mismo sistema operativo host, lo que resulta en un uso más eficiente de los recursos comparado con las máquinas virtuales tradicionales.

3. Escalabilidad

Docker facilita la escalabilidad de aplicaciones al permitir la creación rápida y eficiente de múltiples instancias de contenedores, lo cual es esencial para aplicaciones modernas y microservicios.

4. Integración Continua y Despliegue Continuo (CI/CD)

Docker se integra perfectamente con herramientas de CI/CD, permitiendo la automatización del proceso de construcción, prueba y despliegue de aplicaciones.

5. Consistencia del Entorno de Desarrollo

Con Docker, puedes garantizar que el entorno de desarrollo sea idéntico al de producción, eliminando problemas relacionados con "funciona en mi máquina".

6. Aislamiento

Cada contenedor opera de manera aislada, lo que mejora la seguridad y reduce los conflictos entre aplicaciones y sus dependencias.

7. Facilidad de Gestión

Docker permite gestionar y orquestar contenedores de manera sencilla utilizando herramientas como Docker Compose para definir y ejecutar aplicaciones multi-contenedor.

8. Amplia Adopción en la Industria

Docker se ha convertido en un estándar en la industria para la entrega y gestión de aplicaciones, lo que significa que su conocimiento es altamente valorado y demandado en el mercado laboral.

9. Documentación y Comunidad

Docker cuenta con una extensa documentación y una comunidad activa que facilita el aprendizaje y la resolución de problemas.

10. Compatibilidad con Tecnologías Modernas

Docker se integra bien con tecnologías modernas como Kubernetes para la orquestación de contenedores, facilitando la creación de entornos de nube nativa.

Aprender Docker te permitirá desarrollar, desplegar y gestionar aplicaciones de manera más eficiente, consistente y escalable, alineándote con las prácticas modernas de desarrollo y operaciones en la industria.


2

Responder

Reportar
Ray Trápala
Ray Trápala

student
•
hace un mes
Docker permite crear y gestionar contenedores, lo que significa que puedes iniciar, detener, eliminar y modificar contenedores según tus necesidades. Cuando se habla de "gestionar" en este contexto, se hace referencia a estas acciones básicas que realizas sobre los contenedores, no a su orquestación. Kubernetes, por otro lado, se encarga de la orquestación, es decir, gestionar múltiples contenedores a gran escala, asegurando su disponibilidad, escalabilidad y resistencia. Docker es ideal para trabajar a nivel de un solo contenedor, mientras que Kubernetes es más adecuado para aplicaciones distribuidas y complejas.


1

Responder

Reportar
Edinson Manuel Mejia Torres
Edinson Manuel Mejia Torres

student
•
hace 2 meses
Docker es una plataforma de software que permite crear, ejecutar y administrar contenedores. Un contenedor es una unidad liviana y autónoma que incluye todo lo necesario para ejecutar una aplicación: el código, las bibliotecas, las dependencias y las configuraciones, todo empaquetado en un solo contenedor.

Ventajas de Docker:

Portabilidad: Los contenedores Docker funcionan de la misma manera en cualquier entorno (desarrollo, pruebas, producción), independientemente del sistema operativo o la infraestructura.
Aislamiento: Cada contenedor está aislado, lo que significa que las aplicaciones pueden ejecutarse sin interferir entre sí, lo que mejora la seguridad y el manejo de conflictos.
Eficiencia: Los contenedores son más livianos que las máquinas virtuales, lo que significa que puedes ejecutar más instancias en menos recursos y arranques más rápidos.
Consistencia: Docker asegura que una aplicación funcione de la misma manera, sin importar dónde se ejecute, resolviendo problemas de "en mi máquina funciona".
Escalabilidad: Docker facilita el escalado de aplicaciones, ya sea agregando más contenedores para balancear carga o integrando herramientas de orquestación como Kubernetes.
Desarrollo más rápido: Docker permite crear entornos de desarrollo reproducibles rápidamente, lo que acelera la creación y prueba de aplicaciones.
En resumen, Docker facilita la creación de aplicaciones consistentes, escalables y portables, y mejora la eficiencia del desarrollo y la infraestructura.


1

Responder

Reportar
German Pinilla
German Pinilla

student
•
hace 3 meses
📘 Apuntes Clase 01 - Fundamentos de Docker y Contenedores para Desarrolladores

🔹 1. ¿Qué es Docker y por qué es importante?

- Docker es una plataforma que permite crear, ejecutar y gestionar contenedores.

- Su principal ventaja es que proporciona aislamiento:

- La aplicación, sus dependencias y configuraciones se encapsulan en un contenedor.

- No importa dónde se ejecute (Windows, Linux, Mac, servidor físico o nube), siempre funcionará igual.

- Resuelve el clásico problema de desarrollo: 👉 “En mi máquina sí funciona, pero en producción no”.

🔹 2. ¿Qué es un contenedor?

Un contenedor es una unidad ligera y aislada de ejecución, similar a una máquina virtual, pero más eficiente.

Contiene:

- El código de la aplicación.

- Sus dependencias (librerías, binarios).

- La configuración necesaria.

Beneficio: se transporta fácilmente y funciona igual en cualquier entorno.

Diferencia con Máquinas Virtuales (VMs):

- Las VMs emulan un sistema operativo completo.

- Los contenedores comparten el kernel del sistema host → más ligeros, rápidos y con menor consumo de recursos.

🔹 3. Docker Daemon: el corazón de Docker

El Docker Daemon es el servicio que corre en segundo plano y se encarga de:

- Crear y ejecutar contenedores.

- Gestionar imágenes (plantillas de contenedores).

- Administrar redes entre contenedores.

- Manejar volúmenes para persistencia de datos.

👉 El usuario interactúa con Docker mediante la CLI (Command Line Interface) o la API de Docker.

🔹 4. Diferencias con otros conceptos tecnológicos

Es común confundir Docker con otros términos, pero es importante diferenciarlos:

- Microservicios:

- Es un estilo arquitectónico.

- Divide una aplicación en módulos pequeños e independientes que se comunican entre sí.

- No son lo mismo que contenedores, pero se suelen implementar con Docker.

- Kubernetes: Es un orquestador de contenedores. Su función es administrar muchos contenedores a gran escala:

- Despliegue automático.

- Escalabilidad.

- Balanceo de carga.

- Docker → crea y corre un contenedor. Kubernetes → maneja cientos o miles de contenedores.

- Docker:

- Se enfoca en crear y gestionar contenedores individuales.

🔹 5. Conocimientos previos recomendados

Para aprender Docker con mayor facilidad es útil:

- Conocer Bash o terminal (Linux/Unix).

- Tener nociones de comandos de sistemas operativos Linux.

- Haber trabajado con entornos de desarrollo donde se instalan dependencias manualmente (ej: Node.js, Python, PHP).

👉 Esto ayuda a comprender mejor cómo Docker encapsula todo y evita problemas de compatibilidad.

🔹 6. ¿Por qué usar Docker en desarrollo?

- Consistencia: el mismo contenedor funciona igual en local, en pruebas y en producción.

- Rapidez: arrancar un contenedor es mucho más rápido que levantar una máquina virtual.

- Portabilidad: puedes mover tus proyectos entre distintos equipos y servidores sin preocuparte por dependencias.

- Aislamiento: cada proyecto corre en su propio entorno, sin interferir con otros.


1

Responder

Reportar
Daniel Guerrero
Daniel Guerrero

student
•
hace 5 meses
Docker es algo nuevo para mí no porque viva en otra galaxia, sino que hasta el momento mi compu 'tiraba' haciendo con VMs como virtual box las pruebas o relativos a... que necesitaba en el ambiente 'estudiante', una mirada rápida sobre N8N que le echo un ojo desde que empezo a hacer buzzz me indico que era hora de saber sobre docker, especialmente me llamó la atención lo 'liviano' que es frente a las Virtuals. Pero claro, hay mucho mas que eso, verdad?


1

Responder

Reportar
Amin Espinoza
Amin Espinoza

teacher
•
hace 5 meses
Muchisimo más, ahora Docker domina ampliamente sobre las máquinas virtuales.


1
Jorge Guevara
Jorge Guevara

student
•
hace 6 meses
Docker: Creación, gestión y publicación de contenedores. Diferente a Microservicios, Kubernetes, otros. Permite estandarización de los proyectos, es decir que sirvan en cualquier máquina.

Estructura: Daemon Rest API Cocker CLI

No es crear máquina virtual. Es empaquetar la solución y permitir el despliegue de la misma por cualquier otra persona.

Conocimientos previos: Bash. Linux


1

Responder

Reportar
Mauro Manuel García Vilchis
Mauro Manuel García Vilchis

student
•
hace 7 meses
Docker y Kubernetes son tecnologías complementarias pero distintas. Docker se centra en la creación y gestión de contenedores, permitiendo empaquetar aplicaciones con todas sus dependencias. Kubernetes, por otro lado, es un sistema de orquestación que gestiona la implementación, el escalado y la operación de contenedores en múltiples hosts.

Mientras Docker se ocupa de la construcción y ejecución de contenedores, Kubernetes gestiona cómo esos contenedores se comunican, se escalan y se mantienen en un entorno de producción. En resumen, Docker es para contenedores individuales y Kubernetes para la orquestación de múltiples contenedores.


1

Responder

Reportar
Juan Pablo Mendieta Castillo
Juan Pablo Mendieta Castillo

student
•
hace 7 meses
Lo único que consideraría importante mencionar es que, en casos donde las imágenes de Docker tengan una alta dependencia del sistema operativo, una imagen diseñada, por ejemplo, para sistemas basados en UNIX podría no funcionar de manera óptima al ejecutarse en Windows.


1

Responder

Reportar
