# Clase 3: Instalación de Docker

**Curso de Docker: Fundamentos**
**Clase 3 de 19**

## Resumen
Instalar Docker es el primer paso práctico para comenzar a trabajar con contenedores. En esta clase aprenderás los requisitos previos, cómo instalar Docker en diferentes sistemas operativos (Windows, macOS y Linux), y cómo verificar que la instalación sea correcta. Además, se cubrirán conceptos básicos como el Docker Daemon y la interfaz de línea de comandos (CLI), manteniendo la coherencia con los fundamentos de aislamiento y portabilidad discutidos en clases anteriores.

## ¿Cuáles son los requisitos previos para instalar Docker?
Antes de instalar Docker, asegúrate de cumplir con los siguientes requisitos:

- **Sistema operativo compatible**: Docker Desktop para Windows y macOS, o Docker Engine para Linux.
- **Hardware**: Al menos 4 GB de RAM y 2 GB de espacio en disco.
- **Virtualización habilitada**: En Windows, activa Hyper-V o WSL2; en macOS, asegúrate de que la virtualización esté disponible.
- **Conocimientos básicos**: Familiaridad con la terminal o línea de comandos, como se mencionó en la Clase 1.

Estos requisitos garantizan que Docker funcione eficientemente, aprovechando el aislamiento y la ligereza de los contenedores sobre las máquinas virtuales.

## ¿Cómo instalar Docker en Windows?
Para instalar Docker en Windows:

1. Descarga Docker Desktop desde el sitio oficial de Docker (docker.com).
2. Ejecuta el instalador y sigue las instrucciones.
3. Habilita WSL2 si es necesario (recomendado para mejor rendimiento).
4. Reinicia tu sistema y abre Docker Desktop.
5. Verifica la instalación ejecutando `docker --version` en PowerShell o CMD.

Docker Desktop incluye el Docker Daemon y la CLI, facilitando el desarrollo local.

## ¿Cómo instalar Docker en macOS?
Para instalar Docker en macOS:

1. Descarga Docker Desktop para Mac desde docker.com.
2. Abre el archivo .dmg y arrastra Docker a Applications.
3. Abre Docker Desktop y acepta los términos.
4. Espera a que se inicie el Docker Daemon.
5. Verifica con `docker --version` en Terminal.

En macOS, Docker utiliza Hypervisor.framework para la virtualización, asegurando portabilidad similar a la discutida en clases anteriores.

## ¿Cómo instalar Docker en Linux?
Para instalar Docker en distribuciones Linux como Ubuntu:

1. Actualiza el sistema: `sudo apt update`.
2. Instala paquetes necesarios: `sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release`.
3. Agrega la clave GPG oficial de Docker: `curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg`.
4. Agrega el repositorio: `echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null`.
5. Instala Docker Engine: `sudo apt update && sudo apt install docker-ce docker-ce-cli containerd.io`.
6. Agrega tu usuario al grupo docker: `sudo usermod -aG docker $USER`.
7. Reinicia sesión y verifica: `docker --version`.

En Linux, Docker se integra directamente con el kernel, aprovechando el aislamiento eficiente de los contenedores.

## ¿Cómo verificar que Docker esté funcionando correctamente?
Después de la instalación:

- Ejecuta `docker --version` para ver la versión instalada.
- Ejecuta `docker run hello-world` para probar un contenedor básico.
- Usa `docker ps` para listar contenedores en ejecución.
- Revisa el estado del Docker Daemon con `docker info`.

Estos comandos confirman que Docker está listo para crear y gestionar contenedores, alineándose con los beneficios de consistencia y eficiencia mencionados en la Clase 1.

## ¿Qué es el Docker Daemon y cómo interactuar con él?
El Docker Daemon es el servicio en segundo plano que gestiona contenedores, imágenes y redes, como se explicó en la Clase 1. Interactúas con él a través de:

- **CLI (Command Line Interface)**: Comandos como `docker run`, `docker build`.
- **API REST**: Para integraciones avanzadas.
- **Docker Desktop**: Interfaz gráfica para gestión visual.

Entender esto refuerza el concepto de aislamiento y portabilidad de Docker.

## ¿Qué hacer si hay problemas durante la instalación?
- **Errores comunes**: Virtualización no habilitada, permisos insuficientes.
- **Solución**: Revisa la documentación oficial de Docker o foros como Stack Overflow.
- **Recursos adicionales**: Visita docs.docker.com para guías detalladas.

Con Docker instalado, estás preparado para las próximas clases sobre creación de imágenes y ejecución de contenedores.