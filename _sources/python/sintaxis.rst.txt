Sintaxis Python
===============

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Sintáxis básica de Python 3.8
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################
  
Instalación
***********
* Instalación: ``sudo apt install python3``
* Extensión de archivos: **.py**
    
Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: python
    :linenos:
 
    # Comentario de una sola línea

* Comentarios multilínea:

.. code-block:: python
    :linenos:

    """
    Este comentario 
    tiene más de una línea.
    Puede servir para escribir
    un manual u otras cosas.
    """

Entrada y salida estandar
*************************
 
.. code-block:: python 
    :linenos:

    # entrada estandar:
    dato = input('introduce un dato: ')

    # salida estandar:
    print(dato)

    # salida en una sola línea:
    for i in range(1,11):
        print("{}...".format(i), end="") 

Estructura en python
********************

.. code-block:: python
    :linenos:

    import random

    numero_aleatorio = random.randint(1, 20)

    print(numero_aleatorio)

.. attention::
    En Python no se hace uso de llaves ni de ; final

Concatenación
*************
Concatenación de variables y cadenas se realiza con **+**

.. code-block:: python 
    :linenos:

    # concatenación con +
    print("cadena concatenada a " + "otra cadena")

    variable = "Pepe"
    print("resultado en variable: " + variable)

    # usando format para colocar variables:
    nombre = "Guillermo"
    apellidos = "Granados Gómez"
    print("Me llamo {} y mis apellidos son {}.".format(nombre, apellidos))

Python-CLI - Comandos de python
*******************************

Comandos de python y pip:

* python3: abre la consola de python y con exit() se puede cerrar.
* python3 --version: versión usada
* python3 archivo.py: ejecuta un script python.

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: python 
    :linenos:

    cadena = "Cadena de texto"
    entero = 27
    decimal = 23.27
    booleano = True # False
    lista = ['datos', 2, 3.2, False]
    tupla = ('dato uno', 2)
    diccionario = {
        'nombre': 'Pepe',
        'telefono': 753283723
    }

* Constantes:

.. code-block:: python
    :linenos:

    CONSTANTE = "soy una presunta constante"

.. attention:
    Las constantes no existen como tales en Python, pero si se utiliza la convención de declararlas en mayúsculas para recordar que es un dato que no debería ser mutable.

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: python 
    :linenos:

    sumar = 3 + 6
    restar = 7 * 9
    multiplicar = 11 * 6
    dividir = 13 / 20
    resto = 54 % 7
    potencia = 3 ** 5

* Asignar operación:

.. code-block:: python 
    :linenos:

    # la variable debe tener un valor asignado:
    resultado = 0

    resultado += 12
    resultado -= 16
    resultado *= 19
    resultado /= 6
    resultado **= 5

Operadores relacionales
***********************
Validación entre dos números.

* Mayor que: **>**.
* Menor que: **<**.
* Mayor o igual que: **>=**.
* Menor o igual que: **<=**.
* Igual que: **==**.

Operadores lógicos
******************
Expresiones de operaciones lógicas.

* and: **and**.
* or: **or**.
* not: **!**.

Estructuras de control
######################

Condicional if
**************

* if sencillo:

.. code-block:: python 
    :linenos:

    edad = 18;

    if edad >= 18:
        print("Eres mayor de edad")

* if / else:

.. code-block:: python 
    :linenos:

    edad = 15

    if edad >= 18:
        print("Eres mayor de edad")
    else:
        print("Eres menor de edad")

* else-if:

.. code-block:: python 
    :linenos:

    edad = 45

    if edad >= 65 :
        print("Eres un anciano")

    elif edad >= 18:
        print("Eres mayor de edad")
    else:
        print("Eres menor de edad")

* Operador ternario:

.. code-block:: python 
    :linenos:

    edad = int(input("Introduce tu edad: "))
    print("eres mayor de edad") if (edad >= 18) else print("Todavía eres menor de edad")


Condicional Switch
******************
No existe el condicional Switch en Python, su alternativa es usar **if-elif-else**

Bucle for
*********

* for básico:

.. code-block:: python 
    :linenos:

    for i in range(1,10):
        print("Repetición nº {} \n".format(i))

* for clave / valor:

.. code-block:: python 
    :linenos:

    electrodomesticos = {
        "producto": "Nevera",
        "modelo": "FX27",
        "marca": "Fagor",
        "precio": 783.23
    }

    for key, value in electrodomesticos.items():
        print("{}: {} \n".format(key, value))

Bucle while
***********

* While sencillo:

.. code-block:: python 
    :linenos:

    num = 0

    while num < 10:
        print("código de mensaje - {}".format(num))
        num += 1

* While infinito:

.. code-block:: python 
    :linenos:

    numero = 10
    # al añadir True hacemos un bucle infinito:
    while True:
        adivina = int(input('Adivinia el número >> '))

        if adivina == numero:
            print('Acertaste!')
            # Con exit() finalizamos el programa
            exit()

        print('Fallaste!')

Detener secuenda de script
**************************

.. code-block:: python
    :linenos:

    for i in range(10):
        if(i == 5):
            print("Ya has llegado a 5 y no irás más lejos")
            exit()

    print("Esta frase no se mostrará")

Compresión de listas
********************
Las compresión de lista es un método para recuperar una serie de valores y agregarlos a una lista en una sola secuencia:

.. code-block:: python 
    :linenos:

    # tenemos un diccionario:
    lista_consolas = [
        {'marca': 'Sega', 'modelo':'Mega Drive', 'generación': '4ª Generación'},
        {'marca': 'Sega', 'modelo':'Master System', 'generación': '3ª Generación'},
        {'marca': 'Sony', 'modelo':'PlayStation', 'generación': '5ª Generación'},
        {'marca': 'Nintendo', 'modelo':'Gamecube', 'generación': '6ª Generación'}
    ]

    # se crea una lista y dentro lo primero que anotamos es el dato a recuperar y acto seguido el bucle sobre la lista de valores:
    consolas = [consola['modelo'] for consola in lista_consolas]

    print(consolas)

* Con condición: 

.. code-block:: python
    :linenos:

    lista_consolas = [
        {'marca': 'Sega', 'modelo':'Mega Drive', 'generación': '4ª Generación'},
        {'marca': 'Sega', 'modelo':'Master System', 'generación': '3ª Generación'},
        {'marca': 'Sony', 'modelo':'PlayStation', 'generación': '5ª Generación'},
        {'marca': 'Nintendo', 'modelo':'Gamecube', 'generación': '6ª Generación'}
    ]

    # Se añaden la condición después del bucle:
    consolas = [consola['modelo'] for consola in lista_consolas if consola['marca'] == 'Sega']

    print(consolas)

* Con un bucle for el resultado sería:

.. code-block:: python
    :linenos:

    consolas = []
    for consola in lista_consolas:
        if consola['marca'] == 'Sega':
            consolas.append(consola['modelo'])

.. note::
    Hay que tener en cuenta que el primer dato es solo el resultado de un bucle for, teniendo eso en cuenta se pueden hacer muchos tipos de operaciones.

Tipos de datos avanzados
########################

Listas
******

.. code-block:: python 
    :linenos:

    lista = ["cadena", 20, 18.27, False, ["otra cadena", 23, 18.77]]

    # asignación:
    lista[3] = "Morcilla"

    # impresión:
    print(lista[3])

Tuplas
******

.. code-block:: python 
    :linenos:

    tupla = ("cadena", 20, 18.27, False, ["otra cadena", 23, 18.77])
    
    # impresión
    print(tupla[2])

.. attention:: 
    Las tuplas son inmutables por lo tanto no se pueden asignar valores

Diccionarios
************

.. code-block:: python 
    :linenos:

    operadores = [
        {"suma": "+"},
        {"resta": "-"},
        {"multiplicación": "*"},
        {"división": "/"},
        {"resto": "%"},
        {"potencia": "**"}
    ]

    # ejemplo recorrido en listado de diccionarios:
    for operador in operadores:
        for key, value in operador.items():
            print("{}: {}".format(key, value))

    # asignación:
    operadores[0]["suma"] = "Sumar"

    # impresión: 
    print(operadores[0]["suma"])

Control de errores
##################

.. code-block:: python
    :linenos:

    try:
        print(nombre)
    except NameError:
        print('No has escrito un nombre')


Programación modular
####################

Funciones
*********

* Procedimienos:

.. code-block:: python 
    :linenos:

    def saludar():
        print("Hola persona")

    saludar()

* funciones:

.. code-block:: python 
    :linenos:

    def saludar():
        return "Hola persona"

    print(saludar())

* uso de parámetros:

.. code-block:: python 
    :linenos:

    def saludar(nombre):
        return "Hola {}".format(nombre)

    print(saludar("Antonio"))

* Funciones anónimas:

.. code-block:: python 
    :linenos:

    # lambda recibe uno o varios parámetros y hace un return directamente de forma anonima:
    sumar = lambda a,b,c: a+b+c 

    print(sumar(10,13,18))

* Ámbito global:

.. code-block:: python 
    :linenos:

    nombre = "Alberto"

    def saludar():
        return "¿Qué tal {}?".format(nombre)

    print(saludar())

.. note:: 
    Las variables en Python son por lo general de ámbito global

Programación orientada a objetos
################################

El ámbito de atributos y métodos de una clase en Python son globales.

Clases y objetos
****************

* Estructura clase:

.. code-block:: python 
    :linenos:

    class Videoconsola():
        # atributos:
        modelo = "Mega Drive"
        marca = "Sega"

        # los métodos reciben siempre self para hacer uso de los atributos de la clase:
        def descripcion(self):
            print("Es una {} {}".format(self.marca, self.modelo))


    # crear objeto:
    megaDrive = Videoconsola()

    # recuperar atributo:
    print(megaDrive.marca)

    # recuperar métodos:
    megaDrive.descripcion()


* Constructor:

.. code-block:: python 
    :linenos:

    class Videoconsola():
        # atributos:
        modelo = "Mega Drive"
        marca = "Sega"

        # El constructor recibe self y los parámetros que se pasan por el constructor:
        def __init__(self, modelo, marca):
            self.modelo = modelo 
            self.marca = marca

        def descripcion(self):
            print("Es una {} {}".format(self.marca, self.modelo))


    # crear objeto y pasar parámetros al constructor:
    megaDrive = Videoconsola("MegaDrive", "Sega")

    print(megaDrive.marca)

    megaDrive.descripcion()

* Get y Set:

.. code-block:: python 
    :linenos:

    class Persona:
        def __init__(self, nombre, apellido, edad, dni):
            self.nombre = nombre 
            self.apellido = apellido 
            self.edad = edad 
            # para atributos y métodos privados añadimos _ antes de forma simbólica:
            self._dni = dni

        # para evitar recuperar el atributo dni usamos el siguiente decorador que lo encapsula:
        @property # Este sería el get
        def dni(self):
            return self._dni

        @dni.setter # y este el set
        def dni(self, dni):
            self._dni = dni
        
        def saludar(self):
            print("Hola, me llamo {} {} y tengo {} años".format(self.nombre, self.apellido, self.edad))


    pedro = Persona("Pedro", "Martinez Sal", 37, "323223112V")
    pedro.saludar()

    # Uso de get:
    print("Mi DNI es: " + pedro.dni)

    # Uso de set:
    pedro.dni = "75753233X"
    print("Nuevo DNI: " + pedro.dni)

* Herencia:

.. code-block:: python 
    :linenos:

    class Persona():

        def __init__(self, nombre, genero):
            self.nombre = nombre
            self.genero = genero

        def datos(self):
            print("Su nombre es {} y su género es.".format(self.nombre, self.genero))


    class Luis(Persona):
        def __init__(self, nombre, genero, peso, estatura):
            # para los atributos del padre cargamos el superconstructor y le pasamos los atributos del padre:
            super().__init__(nombre, genero)
            self.peso = peso
            self.estatura = estatura

        # Podemos sobrecargar el método para que imprima más atributos:
        def datos(self):
            print("Su nombre es {}, su género {}, pesa {} kilos y mide {}.".format(self.nombre, self.genero, self.peso, self.estatura))

    # Objeto creado con padre y uso de metodo datos:
    pedro = Persona("Pedro", "Masculino")
    pedro.datos()

    # Objeto creado con hijo y uso de metodo datos:
    luis = Luis("Luis", "Masculino", 90, 1.75)
    luis.datos()

.. note::
    Se puede hacer herencia múltiple pasándole a la clase hija varias clases padres por parámetro y esta podrá trabajar con todos sus atributos y métodos. 
    Ej: class **Luis(Persona, Profesion):**

Clases abstractas
*****************
Es posible trabajar con clases abstactas gracias a la librería **abc**

.. code-block:: python
    :linenos:

    # se importa la librería para abstracciones:
    from abc import ABC, abstractmethod

    # se le indica a la clase que es abstracta con abc:
    class Videoconsola(ABC):
        modelo = "Super Nintendo"
        marca = ""

        def __init__(self, modelo, marca):
            self.modelo = modelo
            self.marca = marca

            print("Se ha creado el objeto")

        def juegos():
            print("La consola dispone de alrededor de 700 títulos")


        # las funciones abstractas se deben usar obligatoriamente en la clase hija:
        # Utilizan un decorador de abc:
        @abstractmethod
        def precio():
            """ Texto convencional: este método muestra el precio """
            pass

    # clase a partir de clase abstracta:
    class SuperNintendo(Videoconsola):
        def __init__(self):
            self.modelo = "SNES"
            self.marca = "Nintendo"


        def precio(self):
            print("La consola cuesta 200 €")



    # uso de clase hija:
    superNintendo = SuperNintendo()
    print(superNintendo.modelo)

    superNintendo.precio()

    # Desestructuración de métodos:
    Videoconsola.juegos()


Interfaces
**********
Las interfaces como tales no existen en python pero hay un modo de trabajar de forma similar

.. code-block:: python 
    :linenos:

    class VideoconsolaInterface():
        # En una supuesta interfaz creamos los métodos y le pasamos el valor pass para dejarlos vacíos:
        def descripcion():
            """ Muestra una descripción de la consola """
            pass


    class NeoGeo(VideoconsolaInterface):
        def __init__(self, modelo, marca, precio):
            self.modelo = modelo
            self.marca = marca
            self.precio = precio
            print(self.precio)

        def descripcion(self):
            print("Es la consola de {} {}".format(self.modelo, self.marca))


    neoGeo = NeoGeo("Neo Geo Pocket", "SNK", "149.99")
    neoGeo.descripcion()

Método "__str__"
****************
El método **__str__()** retorna una cadena al imprimir el objeto que se genera:

.. code-block:: python 
    :linenos:

    class Consola:
    
        def __init__(self, marca, modelo):
            self.marca = marca 
            self.modelo = modelo 

        # el método __str__ define una cadena que retorna al imprmir:
        def __str__(self):
            return "Es una videoconsola {} {}.".format(self.marca, self.modelo)

    playstation = Consola("Sony", "PlayStation")

    # Al imprimir el valor devolverá la cadena asignada en __str__:
    print(playstation)

Importar y exportar
###################

Módulos y paquetes
******************
Podemos crear nuestros propios módulos en python para cortar partes del código específicas:

* Lo primero es crear un nuevo archivo.py y guardar ahí por ejemplo una clase.
* Luego creamos un segundo archivo que será el principal.py y para importarlo basta con escribir ``import archivo`` al comienzo del proyecto.

Si lo que queremos es guardar el módulo en una carpeta entonces estamos hablando de un Paquete:

* Los paquetes son archivos.py que guardamos en una carpeta.
* Dentro de esa carpeta creamos siempre un archivo llamado ``__init__.py`` para que el interprete lo considere un paquete.
* Luego en el archivo principal.py lo importamos con la línea ``from carpeta import archivo``

Y para poner un alias a un paquete o módulo de python ya sea estandar o personalizado utilizamos ``as``:

.. code-block:: python

    from carpeta import archivo as traductor