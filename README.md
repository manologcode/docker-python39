# DOCKER PYTHON 3.10

Se trata de un entorno sencillo docker para crear y desarrollar aplicaciones en phyton y deployarlas.

Tiene dos dockerfiles, uno para cada entorno son contenedores ligeros de con python 3.10 sobre Alpine

## ENTORNO DESARROLLO

se ha creado un archivo sh para automatizar el proceso de puesta en marcha de contenedor

    ./runDocker.sh

Cuando ejecutamos el script si es la primera wez copia los paquetes iniciales , crear site-packages para tener persistencia de los mismos y los comparte con el contenedor

el entorno de desarrollo cargar un contenedor con el que comporte mediante volúmenes los archivos de las librerías y la capeta de desarrollo para ir almacenado los cambios y ir incorporando nuevas librerías sin tener que volver a reconstruir la imagen del contenedor


### Ejecutamos pythom dentro del contenedor

editar el archivo requirements.txt y añadir los paquete que necesitemos

 	pip3 install  --no-cache-dir -r requirements.txt

para correr la aplicación

    python app.py

para ver la aplicación en el navegador

    http://localhost:5000/

### reconstruir la imagen para añadir nuevos elementos

Si necesitamos reconstruir la imagen para ponerle nuevo o personalizarla (poner cada uno el nombre que quiera)

    docker build -f DockerfileDevelopment --no-cache --pull . -t manologcode/mypyal-dev3.10

para subirla a docker-hub

    docker login --username=manologcode

    docker push manologcode/mypyal3.10

## ENTORNO PRODUCCIÓN

En producción esta pensado que los archivos y las librerías se copien dentro de la imagen y use gunicorn para servir aplicación.

para corre la imagen

    docker run -it -rm --name=appflask -p 8080:80 -v $PWD/app:/app manologcode/mypyal3.10

    http://localhost:8080/
