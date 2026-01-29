# PRÁCTICA: Acelerando juegos de prueba con tmpfs (Docker)

# 1. Comprobar que Docker está instalado

docker --version
systemctl status docker

Si no está instalado :

sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

# 2. Comprobar que tenemos el archivo dump.sql

ls /home/$USER/dump.sql

# 3. Crear contenedor MySQL SIN tmpfs

docker run -d --rm \
--name mysqlsintmpfs \
-p 3306:3306 \
-v /home/$USER/dump.sql:/docker-entrypoint-initdb.d/dump.sql \
-e MYSQL_ALLOW_EMPTY_PASSWORD=TRUE \
-e MYSQL_USER=cefireuser \
-e MYSQL_PASSWORD=cefirepass \
mysql:5.6

Comprobar que está funcionando:

docker ps

# 4. Crear contenedor MySQL CON tmpfs

docker run -d --rm \
--name mysqlcontmpfs \
-p 3307:3306 \
-v /home/$USER/dump.sql:/docker-entrypoint-initdb.d/dump.sql \
--tmpfs /var/lib/mysql:rw,noexec,nosuid,size=1024m \
-e MYSQL_ALLOW_EMPTY_PASSWORD=TRUE \
-e MYSQL_USER=cefireuser \
-e MYSQL_PASSWORD=cefirepass \
mysql:5.6

Comprobar:

docker ps

# 5. Acceder al contenedor SIN tmpfs

docker exec -it mysqlsintmpfs bash

Dentro del contenedor:

mysql -u root

Dentro de MySQL:

USE test;
SELECT SQL_NO_CACHE * FROM posts;

exit;

# 6. Acceder al contenedor CON tmpfs

docker exec -it mysqlcontmpfs bash

Dentro:

mysql -u root

Ejecutar la misma prueba:

USE test;
SELECT SQL_NO_CACHE * FROM posts;

exit;

# 7. Comparar tiempos de respuesta

Observa el tiempo que devuelve MySQL tras la consulta:

Contenedor sin tmpfs → más lento

Contenedor con tmpfs → más rápido

En las pruebas realizadas, el contenedor con tmpfs obtiene mejores tiempos de respuesta al trabajar en memoria RAM.

# 8. Detener contenedores 

docker stop mysqlsintmpfs
docker stop mysqlcontmpfs
