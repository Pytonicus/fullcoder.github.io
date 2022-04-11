Bases de datos
==============

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M

  
Trabajando con bases de datos en Python 

.. contents:: Índice
  
Conexión SQLITE 3
#################
 
.. code-block:: python 
    :linenos:
 
    # importar modulo sqlite 3:
    import sqlite3

    # Seleccionar archivo de conexión:
    conexion = sqlite3.connect("prueba.db")

    # Realizar conexión con un cursor:
    cursor = conexion.cursor()

    # Guardar operacion:
    conexion.commit()

    # Cerar conexion:
    conexion.close()


Conexión MySQL
##############

Pasos iniciales:

* Paso 1: Instalar la librería MySQL: ``sudo apt-get install python-mysqldb``

.. code-block:: python 
    :linenos:

    # importar modulo mysql:
    import MySQLdb

    # preparar conexión:
    host = 'localhost'
    username = 'guillermo'
    password = 'guillermo'
    database = 'pruebas'

    try:
        # Realizar conexión:
        conexion = MySQLdb.connect(user=username, passwd=password, host=host, db=database)
        
        # establecer cursor:
        cursor = conexion.cursor()
        
        print("Conexión realizada con éxito")
    except:
        print("Error de conexión") 

    conexion.close()

Operaciones CRUD
################
Despues de realizar la conexión a la base de datos se pueden ejecutar las sentencias SQL del siguiente modo
 
Crear base de datos
*******************
 
.. code-block:: python 
    :linenos:

    # Crear una base de datos:
    cursor.execute("CREATE DATABASE python_db")

    conexion.commit()

    conexion.close()


Crear una tabla
***************

.. code-block:: python 
    :linenos:

    # Crear una tabla:
    cursor.execute('CREATE TABLE usuario(nombre VARCHAR(100), edad INTEGER, email VARCHAR(100))')

    conexion.commit()

    conexion.close()

Insertar registros
******************

.. code-block:: python 
    :linenos:

    # creamos una lista con varias tuplas:
    usuarios = [
        ('Luis', 20, 'luis@luiser.com'),
        ('Mira', 27, 'mira@ynomira.com'),
        ('Juan', 90, 'ju@n.com')
    ]
    # ahora podemos ejecutar la consulta que introduce varios registros a la vez:
    cursor.executemany("INSERT INTO usuario VALUES (?,?,?)", usuarios)
    conexion.commit()

    conexion.close()

Leer registros
**************

.. code-block:: python 
    :linenos:

    # Realizar consulta:
    cursor.execute('SELECT * FROM usuario')
    usuarios = cursor.fetchall() # recuperamos con este metodo una lista de registros.

    print(usuarios)

    # recorremos todos los registros:
    for usuario in usuarios:
        print("Nombre: {} \nEdad: {} \nEmail: {}\n\n".format(usuario[0], usuario[1], usuario[2]))

    conexion.close()

Borrar registros
****************

.. code-block:: python 
    :linenos:

    # Realizar consulta:
    cursor.execute('DELETE FROM usuario WHERE nombre="Luis"')

    conexion.commit()

    conexion.close()

Actualizar registros
********************

.. code:: python 

    # Realizar consulta:
    cursor.execute('UPDATE usuario SET nombre="Alberto" WHERE nombre="Juan"')

    conexion.commit()

    conexion.close()