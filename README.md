
# Practica1
Practica Docker Despliegue de aplicaciones multientorno
# Setup:
## Requisitos previos
### Docker: Si no tienes Docker instalado, puedes descargarlo desde https://docs.docker.com/get-started/get-docker/. Docker se encargará del manejo de los contenedores
### Git: Para clonar el repositorio en tu máquina. Se puede descargar desde https://git-scm.com/downloads
## 1. Clonación del repositorio
### Una vez descargado git, accedemos en la consola a la ruta donde queremos clonar el repositorio.
### Cuando ya estemos en la ruta deseada, procedemos a clonar el repositorio con el comando "git clone https://github.com/JaviKed/Practica1.git"
## 2. Configuración y construcción de los contenedores
### Cuando ya tenegamos clonado el repositorio en nuestra máquina, abriremos Docker
### En la terminal de Docker entramos a la ruta de la carpeta del repositorio clonado
### A continuación, ejecutamos el comando "docker-compose up --build" de esta forma, docker construirá la imagen de flask y levantará la aplicación junto con los contenedores de Redis postgreSQL
## 3. Acceder a la Aplicación
### Una vez ejecutado el comando, se crearán los contenedores y tendremos acceso a las dos apps (prod, dev)
### Para acceder a ellas puedes acceder en tu buscador y entrar al enlace localhost:5000 para dev y localhost:5001 para prod
## 4. Administración de DB y cahcé
### El comando de build también nos ha levantado un contenedor con GUI para administrar la base de datos (Adminer) y la cache (RedisCommander)
### Para acceder a ellas se puede entrar en localhost:8080 para Adminer y localhost:8081 para la RedisCommander


# Partes del proyecto
### El proyecto se compone de dos bases de datos de postgreSQL, una para cada entorno de la app (prod y dev)
### Una cache de Redis que almacenera las consultas a la base de datos durante 60s para mejorar el rendimiento de la aplicación
### Los gestores de estos componentes Adminer para las bases de datos y RedisCommander para la cache
### Y, por último, un contenedor para cada uno de los entornos de la app de Flask

# Diagrama
### El diagrama de la arquitectura del proyecto es la siguiente:
### ![Diagrama](https://i.imgur.com/msMeQ56.png)

# Pruebas realizadas
## Cache
### La primera prueba realizada sobre la cache ha sido la mas simple, un ping. Para ello entramos en el contenedor de la web de producción con el comando "docker-compose exec -it web_prod /bin/sh" y una vez estemos dentro de la consola realizamos el comando "redis-cli -h redis ping". Esto hará que si la cache está conectada correctamente nos devuela un PONG.
### Y la siguiente prueba se basa en colocar manualmente contenido en la cache. Para ello con el comando "docker-compose exec -it redis redis-cli" entramos en el contenedor de la cache y con un comando SET con valor de llave "prueba" y contenido "test" "set prueba test" al realizar una peticion GET "get prueba" la cache nos devolvera "test". También se podrá comprobar en RedisCommander que se ha añadido a la cache correctamente.

## Base de datos
### Lo primero es que se produzca correctamente la ejecución del script init.sql. Simplemente, cuando se creen los contenedores, la base de datos no estará vacía, tendrá una tabla items que nos mostrará, en este caso, una tabla vacía para evitar que falle la aplicación. Esto se podrá comprobar también en Adminer.
### Se puede también realizar pruebas para introducir manualmente datos en las bases de datos y comprobar que se actualizan correctamente en los contenedores de web, por ejemplo, introduciendo un valor de prueba y hacer un refresh para comprobar que se actualizan de manera inmediata.

## Aplicacion Web
### Las pruebas realizadas sobre la web son principalmente el Stop de los contenedores de cache y base de datos y ver si el indicador de conexion de la aplicación web se realiza de manera correcta.
### en la producción también se ha probado la priorización de los datos de la cache (se muestran durante 60s) y que posteriormente al terminar su TTL se actualice con los datos realizados en su base de datos.

## Persistencia de datos
### Las pruebas realizadas sobre la persistencia de datos se ha realizado realizando un "docker-compose down" y comprobando que los volumenes al volver a levantar los contenedores han mantenido los últimos datos de las appweb tanto en base de datos como en cache

