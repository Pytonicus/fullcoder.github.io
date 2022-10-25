Manejo de paquetes
==================

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Manejo de paquetes con pip

.. contents:: Índice

Instalar pip3 
#############

* Ejecutar en terminal ``sudo apt install python3-pip``
 
  
Archivo de configuración
########################
 
En la raiz del proyecto se crea un archivo llamado requirements.txt:
* Para guardar la lista de paquetes instalados en nuestro entorno: ``pip3 freeze > requirements.txt``
* Para instalar dependencias ``pip3 install -r requirements.txt``

Comandos mas destacados
#######################

* **pip3 install <paquete>**: Instala un paquete.
* **pip3 uninstall <paquete>**: Desinstala un paquete.
* **pip3 freeze**: Comprobar los paquetes instalados.

.. important::
    Los paquetes siempre se instalan globalmente. Para instalarlos de forma específica
    en un proyecto debemos crear un entorno virtual.

.. note::
    Se pueden encontrar paquetes Python en: https://pypi.org/

  