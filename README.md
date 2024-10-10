
# Practica1
Practica Docker Despliegue de aplicaciones multientorno
# Setup:
## Docker: Si no tienes Docker instalado, puedes descargarlo desde https://docs.docker.com/get-started/get-docker/. Docker se encargará del manejo de los contenedores
## Git: Para clonar el repositorio en tu máquina. Se puede descargar desde https://git-scm.com/downloads
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


