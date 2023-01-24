==========
Linux Bash
==========

.. image:: /logos/bash-logo.png
    :scale: 60%
    :alt: Logo Bash 
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Última edición el día |date| a las |time|. 

Esta es la documentación que he recopilado para bash.
 
.. contents:: Índice
 
Redireccionamiento y tuberías
#############################

Estándares
**********

Existen tres tipos de salida estandar:

- stdin (input): Entrada estandar (cualquier cosa que introducimos por terminal ya sea un comando o la ejecución de un archivo)
- stdout (output): Salida estandar (respuesta que se devuelve por consola)
- stderr (error): Salida de error estandar (error que se devuelve por consola)

Redirecciones de archivo 
************************

- Crear fichero o lo sobreescribe y añade el contenido mostrado en la salida estandar o stdout (>): `ls -l > listado.txt` 
- Actualiza un fichero desde la salida estandar o stdout (>>): `ls -l >> listado.txt` 
- Crear fichero con la salida de error o stderr (2>): `cd directorio_inexistente/ 2> error.txt` 
- Actualiza un fichero con la salida de error o stderr (2>>): `cd directorio_inexistente/ 2>> error.txt` 
- Utilizar el contenido de un fichero como comandos en la entrada o stdin (<): `rev < prueba.txt >> prueba.txt`

Tuberías o redirección de salida 
********************************

Las tuberías se utilizan para redireccionar la salida estandar de un programa hacia la entrada estandar de otro programa. Osea que 
la salida de un comando será parte del siguiente proceso. Esto se hace con el símbolo |

- Ejemplo de uso: ``ls | more`` redirecciona un listado a la salida more para poder ir viendo poco a poco los resultados.

Búsqueda de texto 
*****************

Para buscar tenemos dos modos:

- ``locate nombrearchivo``: buscamos archivos que contengan el nombre indicado.
- ``grep palabracontenida``: buscamos cadenas de texto.
- ``locate nombrearchivo | grep ruta``: buscamos archivos que tengan un nombre y que se encuentren en un directorio. 


Monitorización de procesos 
##########################

Comando PS 
**********
Es el comando mas utilizado para listar procesos:

- ``ps -e`` : muestra los procesos del equipo.
- ``ps -x`` : mostrar todos los procesos ejecutados por mi.
- ``ps -u nombreusuario`` : mostrar procesos de un usuario.
- ``ps -e --forest`` : mostrar la jerarquía de procesos con --forest (valido con otros comandos).

Comando top 
***********
Ejecutando top podemos ver una lista de procesos activos en tiempo real.

Comando Htop 
************
Es una versión mejorada de top, un administrador de tareas mas colorido.

- Hay que instalarlo ejecutando: ``sudo apt install htop``
- Para ejecutarlo solo hay que escribir: ``htop``

Comandos:
- F4: filtramos los procesos.
- F9: Para matar. Se utiliza la opción 9 SIGKILL 

Gestión de paquetes 
###################

Comandos apt 
************

El gestor de paquetes de sistemas debian es APT:
- ``apt search paquete``: busca paquetes con el nombre indicado.
- ``apt update``: actualiza los repositorios y avisa de los paquetes que pueden actualizarse.
- ``apt upgrade``: actualiza los paquetes detectados con update.
- ``apt install paquete``: instala el paquete mencionado.
- ``apt install -f``: instala dependencias necesarias cuando hemos instalado un paquete al que le faltan dependencias.
- ``apt remove paquete``: desinstala el paquete mencionado.
- ``apt autoremove``: elimina paquetes que han sido instalados como dependencias y ya no se usan.

- Para instalar paquetes deb ejecutamos: ``sudo dpkg -i paquete.deb``
- Para instalar paquetes sh ejecutamos: ``sudo ./install.sh``


.. important::
    Hay que ejecutar el comando ``sudo``en sistemas basados en Ubuntu o el comando ``su root`` y trabajar con superusuario para gestionar paquetes.

Listado de repositorios
***********************

- El listado de repositorios se encuentra en: ``cat /etc/apt/sources.list``