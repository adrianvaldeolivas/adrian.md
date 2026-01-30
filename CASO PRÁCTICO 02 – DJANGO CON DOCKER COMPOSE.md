# CASO PRÁCTICO 02 – DJANGO CON DOCKER COMPOSE

# 1-Crear directorio del proyecto

mkdir django-docker

cd django-docker

# 2-Crear el fichero requirements.txt

nano requirements.txt

Contenido:

Django>=3.0,<4.0

psycopg2-binary>=2.8

# 2-Crear el fichero Dockerfile

nano Dockerfile

Contenido:

FROM python:3

ENV PYTHONUNBUFFERED=1

WORKDIR /code

COPY requirements.txt /code/

RUN pip install -r requirements.txt

# 3- Crear el fichero docker-compose.yml

nano docker-compose.yml

Contenido:

version: "3.9"

services:

  db:
  
    image: postgres
    
    volumes:
    
      - ./datos/db:/var/lib/postgresql/data
      
    environment:
    
      - POSTGRES_DB=postgres
      
      - POSTGRES_USER=postgres
      
      - POSTGRES_PASSWORD=postgres

  web:
  
    build: .
    
    command: python manage.py runserver 0.0.0.0:8000
    
    volumes:
    
      - ./codigo:/code
      
    ports:
    
      - "8000:8000"
      
    depends_on:
    
      - db

# 4-Construir la imagen

docker compose build

# 5-Poner en marcha el sistema

docker compose up -d

# 6-Crear el proyecto Django

Ejecutamos el comando dentro del contenedor:

docker compose run web django-admin startproject ejemplodjango .

Esto crea el proyecto Django dentro del volumen ./codigo.

# 7-Cambiar permisos del código

sudo chown -R $USER:$USER ./codigo

# 8-Configurar Django para usar PostgreSQL

Editamos el fichero de configuración:

nano ./codigo/ejemplodjango/settings.py

Comentar o borrar SQLite:

DATABASES = {

    'default': {
    
        'ENGINE': 'django.db.backends.sqlite3',
        
        'NAME': BASE_DIR / 'db.sqlite3',
        
    }
    
}

Sustituir por PostgreSQL:

DATABASES = {

    'default': {
    
        'ENGINE': 'django.db.backends.postgresql',
        
        'NAME': 'postgres',
        
        'USER': 'postgres',
        
        'PASSWORD': 'postgres',
        
        'HOST': 'db',
        
        'PORT': 5432,
        
    }
    
}
# 9-Reiniciar el sistema

docker compose down

docker compose up -d

# 10-Comprobar contenedores

docker compose ps

Ambos deben estar running.

# 11-Acceder a la aplicación

Abrir navegador:

http://localhost:8000
