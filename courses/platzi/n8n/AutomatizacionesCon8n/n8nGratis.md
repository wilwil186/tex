N8N gratis!!

Para instalar n8n en local en Debian (incluyendo Debian 13 Trixie), sigue estos pasos detallados:

## 1. Instalar Docker Engine

Actualiza el índice de paquetes:
```
sudo apt update
```

Instala los paquetes necesarios para permitir que apt use un repositorio sobre HTTPS:
```
sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release
```

Añade la clave GPG oficial de Docker:
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Añade el repositorio de Docker (usa "bullseye" para Debian 13 ya que es compatible):
```
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian bullseye stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Actualiza el índice de paquetes nuevamente:
```
sudo apt update
```

Instala Docker Engine:
```
sudo apt install docker-ce docker-ce-cli containerd.io
```

Inicia el servicio Docker y habilítalo para que se inicie automáticamente:
```
sudo systemctl start docker
sudo systemctl enable docker
```

Añade tu usuario al grupo docker para ejecutar comandos sin sudo (requiere cerrar sesión y volver a iniciar):
```
sudo usermod -aG docker $USER
```
Después de esto, cierra sesión y vuelve a iniciar sesión, o ejecuta `newgrp docker` para aplicar los cambios en la sesión actual.

Verifica que Docker esté instalado correctamente:
```
docker --version
```

## 2. Instalar y ejecutar n8n

Ejecuta el contenedor de n8n:
```
docker run -d --restart unless-stopped --name n8n \
  -p 5678:5678 \
  -e GENERIC_TIMEZONE="America/Bogota" \
  -e TZ="America/Bogota" \
  -e N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=false \
  -v n8n_data:/home/node/.n8n \
  docker.n8n.io/n8nio/n8n:latest
```

Abre n8n en tu navegador: http://localhost:5678

Para ver los logs: `docker logs -f n8n`

Para parar n8n: `docker stop n8n`

Para arrancar n8n: `docker start n8n`

Para eliminar el contenedor si es necesario: `docker rm n8n`