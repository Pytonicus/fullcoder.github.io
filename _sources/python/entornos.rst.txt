Entornos Virtuales
==================

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Entornos virtuales para trabajar con proyectos de forma segura y minimizando errores de versión

.. contents:: Índice
 
pipenv: entorno virtual Python 
##############################

* Instalación: ``pip3 install pipenv``
 
* Creación de entorno virtual (directorio raiz del proyecto): ``pipenv shell``

.. note::
    Verás en la consola justo antes del prompt entre paréntesis el nombre del directorio raiz 
    cuando estás en entorno virtual.

* Salir del entorno virtual: ``exit``
* Acceder al entorno virtual: ``pipenv shell``
* Instalar paquete: ``pipenv install <paquete>``
* Desinstalar paquete: ``pipenv uninstall <paquete>``
* Ver paquetes instalados: ``pipenv graph``
* Ejecutar script: ``pipenv run python prueba.py``
* Guardar dependencias de entorno: ``pipenv run pip freeze > requirements.txt``
 
  