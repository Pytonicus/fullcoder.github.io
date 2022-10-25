PostgreSQL
==========

.. image:: /logos/basic64-logo.png
    :scale: 100%
    :alt: Logo PostgreSQL
    :align: center

.. |date| date::
.. |time| date:: %H:%M
 

Funcionamiento de PostgreSQL
  
.. contents:: Índice

Primeros pasos   
##############

Instalación de PostgreSQL 
*************************

Para instalar PostgreSQL desde cualquier sistema operativo es recomendable seguir los pasos de su web oficial: https://www.postgresql.org/download/

Conceptos básicos
*****************

- Cluster: Áreas de almacenamiento con una o más bases de datos.
- Bases de datos: Colecciones de datos (igual que MySQL)
- Esquemas: Colecciones de tablas en bases de datos. 
- Tablespaces: Almacenamiento en disco desde punto de vista entre tabla e índices.
- Rol: Entidades que pueden ser dueñas de bases de datos o permisos (Usuarios y Grupos)
- Tabla: Colecciones de datos relacionales.
- Vista: Sentencias SQL que afectan a una o varias tablas.
- Disparador (Trigger): Disparadores de eventos que se activan cuando se actua sobre alguna tabla.

Seguridad 
*********

PostgreSQL cuenta con opciones para limitar el acceso a diferentes tipos de usuario en cada cluster, el tipo de ip permitida, el host si es local o externo, el método, y las direcciones permitidas.

Sentencias SQL 
##############

Crear base de datos
*******************

.. code-block:: PostgreSQL 
    :linenos:

    CREATE DATABASE prueba_base_datos
    WITH
    OWNER = guillermo
    ENCODING = 'UTF8'
    LC_COLLATE = 'Spanish_Spain.1252'
    LC_CTYPE = 'Spanish_Spain.1252'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1
    IS_TEMPLATE = False;

Eliminar base de datos 
**********************

.. code-block:: PostgreSQL
    :linenos:

    DROP DATABASE prueba_base_datos;

Crear rol tipo usuario 
**********************

.. code-block:: PostgreSQL
    :linenos:

    CREATE ROLE guillermo WITH LOGIN CREATEROLE PASSWORD '1234';

.. attention::
    El usuario creado en esta sentencia es superusuario, si quisieramos un usuario base habría que quitar la palabra CREATEROLE 

Crear rol tipo grupo  
********************

.. code-block:: PostgreSQL
    :linenos:

    CREATE ROLE grupo_prueba WITH LOGIN CREATEDB PASSWORD NULL ADMIN guillermo;

.. attention::
    En este ejemplo se asigna como administrador del grupo al usuario creado.

EN PROCESO...