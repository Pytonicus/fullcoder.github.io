Análisis de datos
=================

.. image:: /logos/logo-pandas.png
    :scale: 22%
    :alt: Logo Pandas 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Análisis de datos con diferentes tecnologías

.. contents:: Índice
  
Anaconda 
########
* Para instalar Anaconda primero instalamos las siguientes dependencias: 
 
    .. code::

        sudo apt install libgl1-mesa-glx libegl1-mesa
        libxrandr2 libxrandr2 libxss1 libxcursor1
        libxcomposite1 libasound2 libxi6 libxtst6
        

* Vamos a https://www.anaconda.com/products/individual#Downloads descargamos e instalamos.
* Tras la instalación nos preguntará "Do you wish the installer to initialize Anaconda3 by running conda init?" -> decimos yes.
* Cerramos la terminal para que se actualicen los cambios.
* Ejecutamos en terminal: ``anaconda-navigator``
* Abrimos Jupyter y podemos trabajar con un cuaderno nuevo.

Jupyter
#######

JupyterLab 
**********

Si tan solo queremos Jupyter en nuestro equipo podemos instalarlo de la siguiente forma:

- Instalar JupyterLab: ``pip install jupyterlab``
- Ejecutar desde terminal: ``jupyter-lab``

De este modo se abrirá Jupiter lab que contiene una serie de herramientas entre ellas Notebook.

Solo Jupyter Notebook
*********************
Con esta instalación tendremos tan solo el notebook de jupyter:

- Instalar Jupyter Notebook: ``pip install notebook``
- Ejecutar Notebook: ``jupyter notebook``

Pandas
######
Pandas es la librería para trabajar con DataFrames.

* Comprobar versión:

.. code-block:: python
    :linenos:

    # Se importa pandas como pd:
    import pandas as pd 

    # de pd se irá ejecutando las distintas funciones:
    pd.show_versions() # como ver la versión a detalle.


DataFrames
**********
Los dataframes son conjuntos de datos ordenados por filas y columnas:


Crear un DataFrame a partir de Listado de objetos
+++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    # Creamos un listado con varios diccionarios:
    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    # Con esta función se crea un dataframe:
    pd.DataFrame(amigos)

.. note::
    Pandas asocia las keys de cada diccionario como título de columna y cada diccionario es una fila en el DataFrame 

Crear un DataFrame a partir de archivo CSV
++++++++++++++++++++++++++++++++++++++++++

* Tenemos el siguiente archivo CSV llamado amigos.csv:

.. code:: 

    nombre,apellidos
    Alfredo,Ramirez Alberti
    Laura,Plutarco Pitágoras
    Ernesto,Granada Aferez

* Lo leemos con Pandas y este lo convierte a DataFrame:

.. code-block:: python
    :linenos:

    import pandas as pd 

    # Ejecutamos la lectura del csv:
    pd.read_csv(r'amigos.csv')

.. note::
    Se puede saltar filas añadiendo el parametro skiprows y el valor que queramos 
    pd.read_csv(r'amigos.csv', skiprows=3), esto vale para el resto de funciones read_*.

Ver información del DataFrame
+++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # mostrará una información detallada:
    tabla_amigos.info()

Averiguar dimensión dataframe
+++++++++++++++++++++++++++++
Para averiguar la dimensión de un dataframe:

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    # Se guarda el dataframe:
    tabla_amigos = pd.DataFrame(amigos)

    # Y ahora podemos medir su tamaño:
    tabla_amigos.shape

Esto devuelve 3 filas y 2 columnas.

Ver los primeros registros
++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # ver los 5 primeros:
    tabla_amigos.head()

    # ver los primeros que queramos:
    tabla_amigos.head(100)

Ver los últimos registros
+++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # ver los 5 últimos:
    tabla_amigos.tail()

    # ver los últimos que queramos:
    tabla_amigos.tail(25)

Ordenar Registros
+++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Ordenar los registros:
    tabla_amigos.sort_values(by=['nombre'])

    # Ordenar por varios criterios y en orden descendente:
    tabla_amigos.sort_values(by=['apellidos', 'nombre'], ascending=False)

Buscar registros por un valor 
+++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti', 'edad': 19},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras', 'edad': 25},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez', 'edad': 22}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Recuperar todos los registros con el nombre alfredo:
    tabla_amigos[tabla_amigos['nombre'] == 'Alfredo']

Buscar registros por multiples valores 
++++++++++++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti', 'edad': 19},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras', 'edad': 25},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez', 'edad': 22}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Recuperar todos los registros con el nombre alfredo:
    tabla_amigos[(tabla_amigos['nombre'] == 'Alfredo') & (tabla_amigos['apellidos'] == 'Ramirez Alberti')]

Buscar registros que sean mayores o menores
+++++++++++++++++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti', 'edad': 19},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras', 'edad': 25},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez', 'edad': 22}
    ]
    tabla_amigos = pd.DataFrame(amigos)

    # Recuperar todos los amigos mayores de 20:
    tabla_amigos[tabla_amigos['edad'] > 20]

.. note::
    Del mismo modo podemos sacar los registros menores a.. con <

Eliminar un registro
++++++++++++++++++++
Para eliminar un registro basta con saber su fila:

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Recuperar todos los registros con el nombre alfredo:
    tabla_amigos = tabla_amigos.drop(1)

    tabla_amigos

.. note::
    Si queremos eliminar una columna: ``tabla_amigos = tabla_amigos.drop('apellidos', axis=1)``

Comprobar valores nulos
+++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti', 'edad': None},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras', 'edad': 25},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez', 'edad': None}
    ]
    tabla_amigos = pd.DataFrame(amigos)

    # Averiguar valores nulos:
    tabla_amigos.isnull()

Borrar registros con campos nulos
+++++++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti', 'edad': None},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras', 'edad': 25},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez', 'edad': None}
    ]
    tabla_amigos = pd.DataFrame(amigos)

    # Eliminar valores que contengan campos nulos:
    tabla_amigos.dropna()

Reemplazar campos nulos por un valor por defecto
+++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti', 'edad': None},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras', 'edad': 25},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez', 'edad': None}
    ]
    tabla_amigos = pd.DataFrame(amigos)

    # Rellenar valores nulos con otro valor como 0 o '':
    tabla_amigos.fillna('')



Series
******
Las series son definidas en el DataFrame como las columnas de una tabla.

* Si queremos acceder a una columna:

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    # Se guarda el dataframe:
    tabla_amigos = pd.DataFrame(amigos)

    # se llama a la serie:
    tabla_amigos['nombre']

    # también se puede hacer con notación de punto:
    tabla_amigos.apellidos

    # O las series que queramos a la vez:
    tabla_amigos[['nombre','apellidos']]

Contar registros
++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Hará un desglose de cuantas veces se repite cada elemento en una Serie:
    tabla_amigos['nombre'].value_counts()

Ordenar Series
++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Ordenará una serie de datos:
    tabla_amigos['nombre'].sort_values()

Indexación booleana
+++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Mostrará la posición de la serie junto a True o False si coincide el valor buscado:
    tabla_amigos['nombre'] == 'Alfredo'

Gráficos
********

* Ejemplo gráfico estandar: 

.. code-block:: python
    :linenos:

    import pandas as pd 

    import pandas as pd 

    ventas = [
        {'tomates': 23, 'lechugas': 44, 'zanahorias': 172},
        {'tomates': 434, 'lechugas': 156, 'zanahorias': 127},
        {'tomates': 222, 'lechugas': 32, 'zanahorias': 142}
    ]

    tabla_ventas = pd.DataFrame(ventas)

    # Imprime un gráfico en Jupyter:
    tabla_ventas.plot() # esto equivale por defecto a tabla_ventas.plot(kind='line')

Tipos de gráficos
+++++++++++++++++
Modificando el parámetro **kind** obtendremos distintos gráficos:

Tenemos el siguiente gráfico:

.. code-block:: python
    :linenos:

    import pandas as pd 

    ventas = [
        {'cantidad': 23, 'beneficio': 1280},
        {'cantidad': 123, 'beneficio': 640},
        {'cantidad': 11, 'beneficio': 380}
    ]

    tabla_ventas = pd.DataFrame(ventas)
    tabla_ventas.plot(kind='line')

* bar: gráfico de barras.
* barh: barras horizontales.
* pie: gráfico circular o de queso. Funciona con series. ``tabla_ventas['beneficio'].plot(kind='pie')``
* scatter: gráfico de dispersión, requiere valores x e y para poder dispersar.

.. note::
    Se puede ajustar un gráfico con dos valores de referencias por ejemplo en x la cantidad y en Y el beneficio:
    ``tabla_ventas.plot(kind='bar', x="cantidad", y="beneficio")``

Colores
+++++++
Para personalizar colores en los gráficos le pasamos a plot() el parámetro 
color seguido de un color hexadecimal o referencial:

.. code-block:: python
    :linenos:

    import pandas as pd 

    ventas = [
        {'cantidad': 23, 'beneficio': 1280},
        {'cantidad': 123, 'beneficio': 640},
        {'cantidad': 11, 'beneficio': 380}
    ]

    tabla_ventas = pd.DataFrame(ventas)

    # ponemos las barras amarillas:
    tabla_ventas.plot(kind='bar', color="yellow", x="cantidad", y="beneficio")

Mapa de colores
+++++++++++++++
Se pueden usar varios colores con colormap:

.. code-block:: python
    :linenos:

    import pandas as pd 

    ventas = [
        {'producto': 'Zanahorias', 'categoria': 'verduras', 'cantidad': 23, 'beneficio': 1280},
        {'producto': 'Puerros', 'categoria': 'verduras', 'cantidad': 123, 'beneficio': 640},
        {'producto': 'Lechugas', 'categoria': 'verduras', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Galletas', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Cereales', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Coca cola', 'categoria': 'refrescos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'desinfectante', 'categoria': 'limpieza', 'cantidad': 11, 'beneficio': 380}
    ]

    tabla_ventas = pd.DataFrame(ventas)

    # Vamos a usar value_counts() para contear todos los valores de una serie:
    tabla_ventas['categoria'].value_counts().plot(kind='pie', colormap="hot")

Tamaño del gráfico 
++++++++++++++++++
Se puede definir un tamaño de gráfico con figsize:

.. code-block:: python
    :linenos:

    import pandas as pd 

    ventas = [
        {'producto': 'Zanahorias', 'categoria': 'verduras', 'cantidad': 23, 'beneficio': 1280},
        {'producto': 'Puerros', 'categoria': 'verduras', 'cantidad': 123, 'beneficio': 640},
        {'producto': 'Lechugas', 'categoria': 'verduras', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Galletas', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Cereales', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Coca cola', 'categoria': 'refrescos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'desinfectante', 'categoria': 'limpieza', 'cantidad': 11, 'beneficio': 380}
    ]

    tabla_ventas = pd.DataFrame(ventas)

    # ponemos las barras amarillas:
    tabla_ventas['categoria'].value_counts().plot(kind='line', figsize=(10, 5))

Indexación 
**********
La indexación por defecto se establece por fila, pero podemos cambiarla.

Elegir columna como índice
++++++++++++++++++++++++++
Se puede elegir una columna que reemplazará los valores de fila:

.. code-block:: python
    :linenos:

    import pandas as pd 

    ventas = [
        {'producto': 'Zanahorias', 'categoria': 'verduras', 'cantidad': 23, 'beneficio': 1280},
        {'producto': 'Puerros', 'categoria': 'verduras', 'cantidad': 123, 'beneficio': 640},
        {'producto': 'Lechugas', 'categoria': 'verduras', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Galletas', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Cereales', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Coca cola', 'categoria': 'refrescos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'desinfectante', 'categoria': 'limpieza', 'cantidad': 11, 'beneficio': 380}
    ]

    tabla_ventas = pd.DataFrame(ventas)

    # cambiamos índice por categoria:
    tabla_ventas.set_index('categoria')

.. nota::
    set_index() solo imprime valores, si queremos que se guarde el nuevo índice tenemos que pasarle el parámetro inplace=True:
    ``tabla_ventas.set_index('categoria', inplace=True)``

.. attention::
    Si hemos guardado los índices podemos resetearlos ejecutando el método:
    ``tabla_ventas.reset_index(inplace=True)``

Ordenar índices
+++++++++++++++
Los índices nuevos tienen el mismo orden de fila, para cambiarlo usamos sort_index():

.. code-block:: python 
    :linenos:

    import pandas as pd 

    ventas = [
        {'producto': 'Zanahorias', 'categoria': 'verduras', 'cantidad': 23, 'beneficio': 1280},
        {'producto': 'Puerros', 'categoria': 'verduras', 'cantidad': 123, 'beneficio': 640},
        {'producto': 'Lechugas', 'categoria': 'verduras', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Galletas', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Cereales', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Coca cola', 'categoria': 'refrescos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'desinfectante', 'categoria': 'limpieza', 'cantidad': 11, 'beneficio': 380}
    ]

    tabla_ventas = pd.DataFrame(ventas)

    tabla_ventas.set_index('categoria', inplace=True)

    # ordenando por índices:
    tabla_ventas.sort_index(inplace=True)

    tabla_ventas

.. note:: 
    Si queremos ponerlos en orden descendiente le pasamos el parámetro ``ascending=False`` a sort_index()

Buscar grupos por su índice
+++++++++++++++++++++++++++
Al tener un índice personalizado podemos recuperar solo los registros que queramos:

.. code-block:: python 
    :linenos:

    import pandas as pd 

    ventas = [
        {'producto': 'Zanahorias', 'categoria': 'verduras', 'cantidad': 23, 'beneficio': 1280},
        {'producto': 'Puerros', 'categoria': 'verduras', 'cantidad': 123, 'beneficio': 640},
        {'producto': 'Lechugas', 'categoria': 'verduras', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Galletas', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Cereales', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Coca cola', 'categoria': 'refrescos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'desinfectante', 'categoria': 'limpieza', 'cantidad': 11, 'beneficio': 380}
    ]

    tabla_ventas = pd.DataFrame(ventas)

    tabla_ventas.set_index('categoria', inplace=True)

    # Localizar solo aquellos que sean desayunos:
    tabla_ventas.loc['desayunos']

Hojas de cálculo
****************

Cargar datos desde hoja local
+++++++++++++++++++++++++++++
Se puede abrir una hoja de calculo estableciendo su ruta y convertirla a DataFrame:

* Tenemos la siguiente hoja llamada amigos.xlsx:

+-----------------+------------------+------+
| Nombre          | Apellidos        | Edad |
+=================+==================+======+
| Antonio         | Flores Caracas   | 23   |
+-----------------+------------------+------+
| Laura           | Salazar Piraña   | 34   |
+-----------------+------------------+------+
| Iñigo           | Xavier Aguirre   | 47   |
+-----------------+------------------+------+

* Para generar un DataFrame:

.. code-block:: python 
    :linenos:

    import pandas as pd 

    # podemos abrir un excel con pandas:
    excel = pd.ExcelFile('amigos.xlsx')

    # Elegimos la hoja del excel que queremos trabajar:
    dataframe = excel.parse('Hoja 1')

    dataframe

Guardar DataFrame en Excel local
++++++++++++++++++++++++++++++++

.. code-block:: python 
    :linenos:

    import pandas as pd 

    ventas = [
        {'producto': 'Zanahorias', 'categoria': 'verduras', 'cantidad': 23, 'beneficio': 1280},
        {'producto': 'Puerros', 'categoria': 'verduras', 'cantidad': 123, 'beneficio': 640},
        {'producto': 'Lechugas', 'categoria': 'verduras', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Galletas', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Cereales', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Coca cola', 'categoria': 'refrescos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'desinfectante', 'categoria': 'limpieza', 'cantidad': 11, 'beneficio': 380}
    ]

    total_ventas = pd.DataFrame(ventas)

    # creamos un archivo excel:
    excel = pd.ExcelWriter('ventas_agosto.xlsx')

    # Pasamos el dataframe al excel (archivo excel, nombre hoja, índice si/no):
    total_ventas.to_excel(excel, 'Agosto 2020', index=True) # con el tercer parametro definimos si queremos añadir nuestro propio indice o no.

    # guardar el dataframe en el pc:
    excel.save()

Recorrer dataframe con for
**************************
Este es un ejemplo de como convertir un dataframe en JSON:

.. code-block:: python 
    :linenos:

    import pandas as pd 

    ventas = [
        {'producto': 'Zanahorias', 'categoria': 'verduras', 'cantidad': 23, 'beneficio': 1280},
        {'producto': 'Puerros', 'categoria': 'verduras', 'cantidad': 123, 'beneficio': 640},
        {'producto': 'Lechugas', 'categoria': 'verduras', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Galletas', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Cereales', 'categoria': 'desayunos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'Coca cola', 'categoria': 'refrescos', 'cantidad': 11, 'beneficio': 380},
        {'producto': 'desinfectante', 'categoria': 'limpieza', 'cantidad': 11, 'beneficio': 380}
    ]

    total_ventas = pd.DataFrame(ventas)

    # Preparar un listado:
    json_ventas = []

    # recorrer dataframe:
    for i in total_ventas.index:
        # construir formato y añadir:
        json_ventas.append({
            "Producto": total_ventas["producto"][i],
            "Categoría": total_ventas["categoria"][i],
            "Cantidad": total_ventas["cantidad"][i],
            "Beneficio": total_ventas["beneficio"][i]
        })

    print(json_ventas)



