======
Docker
======

.. image:: /logos/docker-logo.png
    :scale: 20%
    :alt: Logo Docker
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Última edición el día |date| a las |time|. 

Esta es la documentación que he recopilado para instalar y configurar docker en sistemas linux.
 
.. contents:: Índice
 
Instalar y configurar Docker  
############################

Para realizar la instalación de docker en nuestra máquina seguimos estos pasos:
- Instalar motor de docker: ``sudo apt install docker.io``
- Instalar docker desktop (para uso local): https://docs.docker.com/engine/install/

Ejecutar docker 
***************

- Para ejecutar docker en un terminal vez: ``dockerd``
- Para ejecutar docker mientras esta el equipo activo: ``systemctl start docker``
- Para ejecutarlo siempre al iniciar el sistema: ``systemctl enable docker`` (o disable para quitarlo del arranque)

- Probar si esta funcionando: ``sudo docker info`` o ``sudo docker --version``

Docker HUB
**********

Docker hub es un repositorio donde existen un montón de imágenes ya creadas por empresas o particulares en https://hub.docker.com/

Podemos bajarnos diferentes versiones de imágenes con pull: ``docker pull ubuntu:trusty`` esto nos bajará una versión diferente del sistema. Este comando se diferencia de run en que baja las imágenes pero no crea los contenedores como lo haría run.

Estas tags como __trusty__ podemos verlas en Docker Hub accediendo a la imagen que queremos recuperar.

Crear cuenta con Docker HUB
***************************
Creamos una cuenta en Docker para poder subir nuestra imágenes al repositorio público.

- Los repositorios con un nombre único son los repositorios oficiales de dicha tecnologías. Los que preceden un nombre y luego una barra son terceros por ejemplo python para centos: centos/python35

Para crear un repositorio pinchamos en create reopository y ponemos el nombre y la visibilidad.

Contenedores
############

Comandos básicos
****************

- Crear contenedor: ``sudo docker run hello-world``
    - Crear contenedor y abrirlo automáticamente: ``sudo docker run -it ubuntu``
    - Crear contenedor y ejecutar en segundo plano: ``sudo docker run -d nginx``
- Mostrar contenedores arrancados: ``sudo docker ps``
    - Mostrar también los parados: ``sudo docker ps -a``
    - Mostrar último contenedor ejecutado o editado: ``sudo docker ps -l``
    - Mostrar el espacio de todos los contenedores: ``sudo docker ps -a -s``
    - Mostrar una cantidad de resultados: ``sudo docker ps -a -n 3``
- Arrancar contenedor y abrir: ``sudo docker start -i 2351`` (4 primeros digitos del CONTAINER ID)
- Ejecutar contenedor ya arrancado: ``sudo docker exec -it f2ad9cdcc bash`` (usar CONTAINER ID y por último el programa con el que ejecutar "bash, python")
- Salir de contenedor: ``exit``
- Matar un contenedor en segundo plano: ``sudo docker kill 5e683ed457267``
- Borrar contenedor usando su CONTAINER ID: ``sudo docker rm 4703`` (4 primeros digitos)
- Borrar contenedor usando su NAME: ``sudo docker rm hello-world``

.. attention::
    Al crear un nuevo contenedor, docker buscará si existe imagen en local, luego lo hará en 
    repositorio y si no existe creará una nueva.

.. attention::
    No se pueden borrar imágenes que tengan vinculados contenedores, 
    para ello hay que borrar el contenedor primero. Para forzar borrado utilizar el flag ``-f``

Comandos de gestión 
*******************
- Comprobar actividad de un contenedor: ``sudo docker logs 5e68`` (4 primeros digitos o todos de CONTAINER ID)
    - Ver las últimas x lineas con: ``sudo docker logs 5e68 --tail 10``
- Ver detalles de un contenedor: ``sudo docker stats 5583``
- Comprobar comando que mas recursos gasta: ``sudo docker top 5583``
- Ver características de un contenedor: ``docker inspect bb51d87fba``
    - Guardar característcas en un json: ``docker inspect bb51d87fba > caracteristicas.json``


Imágenes
########

- Listar imagenes locales de contenedores: ``sudo docker images``
- Borrar imagen mediante su ID: ``docker rmi f2ad9cdcc``
- Ver características de una imagen: ``docker inspect bb51d87fba``
    - Guardar característcas en un json: ``docker inspect bb51d87fba > caracteristicas.json``
    

Redes en Docker 
###############
Para poder acceder a las aplicaciones de los contenedores docker dispone de puertos privados. Tenemos que hacer dichos puertos públicos y mapearlos en el host.

Si tenemos un TOMCAT en un contenedor podemos mapear el puerto 8080 del contenedor con el puerto 80 del servidor, de modo que se podrá acceder al tomcat desde otro dispositivo.

- Ver las redes disponibles: ``sudo docker network ls``

- bridge es la red que utilizan de manera predefinida los contenedores.
- host: esta red solo trabajan con el host principal, no se pueden ver entre si.
- none: es un contenedor que no tiene red. 

Las redes de tipo bridge asignan una ip a cada contenedor. 

Comandos de red
***************

- Ver que ip tiene un contenedor: ``sudo docker inspect nginx2 | grep IPAd``
- Ver la información de una red: ``sudo docker network inspect bridge > bridge.txt``
- Ver las redes disponibles: ``sudo docker network ls``
- Crear red: ``docker network create red1`` 
    - Crear red y definir el rango en la nueva red: ``docker network create --subnet=192.168.0.0/16 red2``


.. attention::
    Docker recomienda que crees tus propias redes si los contenedores van a relacionarse entre si

Gestionar puertos
*****************

- Averiguar que puerto utiliza un contenedor: ``sudo docker port 4279`` (4 primeros digitos de CONTAINER ID)
- Ejecutar contenedor con puertos públicos: ``sudo docker run -d -P nginx``
    - Utilizar el puerto que queramos: ``sudo docker run -d --name nginx2 -p 8080:80 nginx``

.. attention::
    Hay que definir un nombre de contenedor cuando personalizamos el mapeo del puerto.

Asociar contenedores a una nueva red
************************************

- Asociar contenedor ubuntu a la red2: ``sudo docker network connect red2 ubuntua``