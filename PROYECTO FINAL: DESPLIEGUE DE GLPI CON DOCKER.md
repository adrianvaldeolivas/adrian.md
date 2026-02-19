# PROYECTO FINAL: DESPLIEGUE DE GLPI CON DOCKER

# Preparación del entorno

Comprobar versiones:

docker --version  

docker compose version

<img width="485" height="60" alt="captura 1 docker" src="https://github.com/user-attachments/assets/f3269787-9cc2-4e67-b34b-6c3f6a7a91a5" />

Crear un directorio de trabajo:

mkdir proyecto_glpi  

cd proyecto_glpi

<img width="439" height="51" alt="captura 2 docker" src="https://github.com/user-attachments/assets/1b5bc969-ae88-4da5-98d3-3a38da7889cd" />

# Archivo docker-compose.yml

El despliegue se realizará mediante Docker Compose.

Ejemplo de archivo docker-compose.yml:

<img width="842" height="721" alt="captura 3 docker" src="https://github.com/user-attachments/assets/13db7f4d-ede1-4ed6-bc8d-e5c2751ec3b5" />

# Despliegue de la aplicación

Para iniciar el proyecto:

docker compose up -d

<img width="727" height="284" alt="captura 4 docker" src="https://github.com/user-attachments/assets/ecec5273-acb5-4ae1-838e-d072e3845ce1" />


Comprobar que los contenedores están en ejecución:

docker compose ps

<img width="890" height="112" alt="captura 5 docker" src="https://github.com/user-attachments/assets/1cf7f0cc-9052-4719-ac66-e85e2b6392ce" />


# Acceso a GLPI

Abrir el navegador y acceder a:

http://localhost:8080

<img width="1065" height="768" alt="captura 6 docker" src="https://github.com/user-attachments/assets/0d9f0113-3255-4780-81bc-1b8d303a958f" />

