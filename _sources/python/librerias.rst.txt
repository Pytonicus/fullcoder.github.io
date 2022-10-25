Librería Estandar
=================

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Módulos básicos de Python 3.8
 
.. contents:: Índice

platform: Manipulación del Sistema
##################################
   
Información del sistema operativo
*********************************
 
.. code-block:: python 
    :linenos:

    # Importar platform:
    import platform

    # Información del sistema:
    print(platform.uname())

    # Tipo de kernel:
    print(platform.platform())

    # Versión de Kernel:
    print(platform.release())

    # Arquitectura:
    print(platform.architecture())

    # Típo de máquina:
    print(platform.machine())

    # hostname:
    print(platform.node())

    # Tipo de sistema operativo:
    print(platform.system())

    # Versión del sistema operativo:
    print(platform.version())

    # Versión de python instalada:
    print(platform.python_version())

json: Manipulación JSON
#######################

Convertir Diccionario en JSON 
*****************************

.. code-block:: python
    :linenos:

    # se importa la librería json:
    import json

    # Esto es un diccionario:
    listado_dict = [
        {"nombre": "Pepe", "edad": 27},
        {"nombre": "Antonia", "edad": 47},
        {"nombre": "Paco", "edad": 17},
        {"nombre": "Ana", "edad": 23}
    ]

    # parsear Json en Diccionario:
    listado_json = json.dumps(listado_dict)

    # Lo convertirá en un str con formato JSON:
    print(type(listado_json))


Convertir JSON en Diccionario 
*****************************

.. code-block:: python
    :linenos:

    # se importa la librería json:
    import json

    # Los archivos JSON suelen recuperarse en formato cadena:
    listado_json = '[{"nombre": "Pepe", "edad": 27},{"nombre": "Antonia", "edad": 47},{"nombre": "Paco", "edad": 17},{"nombre": "Ana", "edad": 23}]'

    # parsear Json en Diccionario:
    listado_dict = json.loads(listado_json)

    print(type(listado_dict))

datetime: Manipulación de fechas 
################################

.. code-block:: python
    :linenos:

    # importar datetime para fecha y hora:
    from datetime import datetime

    # Imprimir fecha y hora:
    print(datetime.now())

    # Fecha personalizada:
    fecha = datetime.now()
    print(fecha.strftime("%d/%m/%Y"))

    # hora personalizada:
    print(fecha.strftime("%H:%M:%S"))  # también vale strftime("%X")

* Códigos comunes para Fecha: 

+----------------------------------------------+---------+
| Tipo de valor                                | símbolo |
+==============================================+=========+
| Día en notación numeral                      | %w      |
+----------------------------------------------+---------+
| Día por inicial                              | %a      | 
+----------------------------------------------+---------+
| Día de la semana                             | %A      |
+----------------------------------------------+---------+
| Dias transcurridos desde comienzos de año    | %j      |
+----------------------------------------------+---------+
| Semanas transcurridas desde comienzos de año | %W      |
+----------------------------------------------+---------+
| Mes actual en notación numeral               | %m      |
+----------------------------------------------+---------+
| Iniciales del mes corriente                  | %b      |
+----------------------------------------------+---------+
| Nombre completo mes corriente                | %B      |
+----------------------------------------------+---------+
| Año corriente en notación numeral            | %Y      |
+----------------------------------------------+---------+
| Año con notación numeral abreviada           | %y      |
+----------------------------------------------+---------+
| Fecha en formato ISO-8601                    | %u      |
+----------------------------------------------+---------+

* Códigos comunes para Hora:

+----------------------------------------------+---------+
| Tipo de valor                                | símbolo |
+==============================================+=========+
| Ver si la hora es AM o PM                    | %p      |
+----------------------------------------------+---------+
| Hora en formato 12                           | g       |
+----------------------------------------------+---------+
| Hora en formato 24                           | G       |
+----------------------------------------------+---------+
| Hora en formato 12 con 0 inicial             | %I      |
+----------------------------------------------+---------+
| Hora en formato 24 con 0 inicial             | %H      |
+----------------------------------------------+---------+
| Minutos                                      | %M      |
+----------------------------------------------+---------+
| Segundos                                     | %S      |
+----------------------------------------------+---------+
| Microsegundos                                | %f      |
+----------------------------------------------+---------+
| Zona Horaria                                 | %Z      |
+----------------------------------------------+---------+

requests: Manipulación de HTTP 
##############################

Petición HTTP
*************

.. code-block:: python
    :linenos:

    # importar requests:
    import requests

    # Realizar petición básica y obtener código resultado:
    r = requests.get('https://www.fullcoder.org/')
    print(r.status_code)

    # Realizar una petición avanzada:
    headers = {
    'Content-Type': 'application/json',
    'Accept': '*/*'
    }

    data = '{ "user":"pepe", "password":"clave" }'

    r = requests.post('https://fakeapi.com', headers=headers, data=data)
    print(r.status_code)


* Lista de MIMES más comunes: https://developer.mozilla.org/es/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types

Averiguar el tipo de dato recibido
**********************************

.. code-block:: python
    :linenos:
  
    print(r.headers['content-type'])

Recuperar contenido de la petición
**********************************

.. code-block:: python
    :linenos:

    print(r.content)

Recuperar contenido de la petición formato texto 
************************************************

.. code-block:: python
    :linenos:

    print(r.text)


Recuperar contenido de la petición formato JSON 
***********************************************

.. code-block:: python
    :linenos:

    print(r.json())

Haciendo una petición contra API con JWT
****************************************
La petición se podría dividir en dos partes:

1. Solicitud de token:

.. code-block:: python 
    :linenos:

    import requests

    headers = {
        'Content-Type': 'application/json',
        'Accept': '*/*',
    }

    data = '{"username":"misterg@gmail.com", "password":"sabotaje"}'

    r = requests.post('http://127.0.0.1:8000/api/token', headers=headers, data=data)
    print(r.status_code)
    token = r.json()

2. Petición de datos (listado de series):

.. code-block:: python 
    :linenos:

    headers['Authorization'] = 'Bearer ' + token['access']

    r = requests.get('http://127.0.0.1:8000/api/series/', headers=headers)
    print(r.status_code)
    print(r.content)
    
 
os: Manipulación del Sistema
############################

Listar directorio
*****************

.. code-block:: python 
    :linenos:

    # importar os:
    import os 

    # listar una carpeta mediante su ruta o la ruta actual:
    print(os.listdir("./"))

Crear directorio
****************

.. code-block:: python 
    :linenos:

    # importar os:
    import os 

    # Crear una carpeta:
    os.makedirs("carpeta python")

Mostrar directorio actual
*************************

.. code-block:: python 
    :linenos:

    # importar os:
    import os 

    # Mostrar directorio:
    print(os.getcwd())

Mostrar tamaño del archivo o directorio
***************************************

.. code-block:: python 
    :linenos:

    # importar os:
    import os 

    # Mostrar tamaño:
    print(os.path.getsize("carpeta python"))

Comprobar si es archivo o carpeta
*********************************

.. code-block:: python 
    :linenos:

    # importar os:
    import os 

    # Comprobar si es carpeta:
    print(os.path.isfile("carpeta python"))

    # comprobar si es directorio:
    print(os.path.isdir("carpeta python"))

Renombrar archivo o carpeta
***************************

.. code-block:: python 
    :linenos:

    # importar os:
    import os 

    # Comprobar si es carpeta:
    os.rename("carpeta python", "Python mola!")

    print(os.listdir('./'))

Eliminar un archivo o carpeta
*****************************
Suponiendo que tenemos en el directorio en el que ejecutamos el script un directorio llamado
Python mola! y un archivo llamado texto.txt:

.. code-block:: python 
    :linenos:

    # importar os:
    import os 

    # eliminar carpeta:
    os.rmdir("Python mola!")

    # eliminar archivo:
    os.remove("texto.txt")

    print(os.listdir('./'))

shutil: Manipulación de archivos
################################

.. code-block:: python
    :linenos:

    # Importar shutil:
    import shutil

    # Copiar un archivo:
    shutil.copyfile('archivo.txt', 'nuevo.txt')

    # mover un archivo:
    shutil.move('/carpeta/origen', '/carpeta/destino')

Random: Números aleatorios
##########################

.. code-block:: python
    :linenos:

    # Importar random:
    import random

    # Elegir un elemento al azar:
    lista = ['galletas', 'tortitas', 'sandwich']
    print(random.choice(lista))
    # Dame un número al azar que puede ser decimal:
    print(random.random())

    # Y un número al azar basado en un rango de enteros:
    print(random.randrange(15))

    # Y un rango establecido de inicio a fin:
    print(random.randint(2, 8))


Argparse: Pasar argumentos por consola
######################################
Para pasar argumentos a un script de python:

.. code-block:: python 
    :linenos:

    # importamos la librería:
    import argparse

    # Crear objeto parser:
    parser = argparse.ArgumentParser(description="Recibiendo argumentos")

    # creamos los argumentos:
    parser.add_argument('-x', '--saludo', help="Es solo un saludo")

    # añadimos los argumentos:
    parser = parser.parse_args()

    # Se comprueba el argumetno recibido:
    if parser.saludo:
        # se puede también recuperar el valor del argumento:
        print("Hola " + parser.saludo)

Time: manipulación de tiempo
############################
Su uso más frecuente es para crear pausas en el código.

.. code-block:: python
    :linenos:

    # importar librería 
    import time

    print("Hola")
    # establece pausa de 5 segundos:
    time.sleep(5)

    print("Hola de nuevo")


.. note::
    Más modulos de Python en la guía oficial: https://docs.python.org/3/library/
