# Caso práctico 06: Despliegue de Stable Diffusion con Docker

# 1-Requisitos previos

Antes de comenzar, comprobamos que tenemos Docker y Docker Compose instalados.

Comprobación de Docker:

docker --version

Comprobación de Docker Compose:

docker compose version

# 2-Descargar el repositorio de Stable Diffusion

Clonamos el repositorio oficial que contiene la configuración Docker:

git clone https://github.com/AbdBarho/stable-diffusion-webui-docker.git

Accedemos al directorio del proyecto:

cd stable-diffusion-webui-docker

# 3-Descarga inicial de modelos y dependencias

Antes de lanzar la interfaz, es necesario descargar los modelos y archivos necesarios.

Ejecutamos el siguiente comando:

docker compose --profile download up --build

# 4-Lanzar la interfaz de Stable Diffusion

Una vez finalizada la descarga, lanzamos la interfaz web.

El comando general es:

docker compose --profile [ui] up --build

Ejemplo: interfaz sin GPU (CPU)

Si no disponemos de GPU, usamos el perfil auto-cpu:

docker compose --profile auto-cpu up --build

# 5-Acceder a Stable Diffusion

Cuando el contenedor haya terminado de arrancar, abrimos un navegador web y accedemos a:

http://localhost:7860

# 6-Comprobar los contenedores en ejecución

Para verificar que los contenedores están activos, ejecutamos:

docker ps

# 7-Detener Stable Diffusion (opcional)

Cuando queramos detener el servicio, ejecutamos:

docker compose down
