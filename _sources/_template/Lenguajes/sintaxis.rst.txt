Sintaxis LANG
============

.. image:: /logos/logo-[].png
    :scale: 15%
    :alt: Logo []
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Sintáxis básica de []
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################

Instalación
***********
* Instalación: []
* Extensión de archivos: **.[]**

Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: LANG
    :linenos:
 
    ...

* Comentarios multilínea:

.. code-block:: LANG
    :linenos:

    ...

Entrada y salida estandar
*************************
Datos de entrada y salida a través de la consola y/o el navegador.

.. code-block:: LANG 
    :linenos:

    ...

Estructura en LANG
*****************

* Código LANG puro:

.. code-block:: LANG
    :linenos:

    ...

* código LANG junto a HTML:

.. code-block:: LANG
    :linenos:

    ...

* También podemos cargar etiquetas HTML con LANG:

.. code-block:: LANG
    :linenos:

    ...

Concatenación
*************
Concatenación de variables y cadenas se realiza con **.**

.. code-block:: LANG 
    :linenos:

    ...

LANG-CLI - Comandos de LANG
*************************

Comandos de LANG:

* LANG -v: versión usada (EJEMPLO FALSO)

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: LANG 
    :linenos:

    ...

* Constantes:

.. code-block:: LANG
    :linenos:

    ...

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: LANG 
    :linenos:

    ...

* Incremento y decremento:

.. code-block:: LANG 
    :linenos:

    ...

* Asignar operación:

.. code-block:: LANG 
    :linenos:

    ...

Operadores relacionales CORROBORAR
***********************
Validación entre dos números.

* Mayor que: **>**.
* Menor que: **<**.
* Mayor o igual que: **>=**.
* Menor o igual que: **<=**.
* Igual que: **==**.

Operadores lógicos CORROBORAR
******************
Expresiones de operaciones lógicas.

* and: **&&**.
* or: **||**.
* not: **!**.

Estructuras de control
######################

Condicional if
**************

* if sencillo:

.. code-block:: LANG 
    :linenos:

    ...

* if / else:

.. code-block:: LANG 
    :linenos:

    ...

* else-if:

.. code-block:: LANG 
    :linenos:

    ...

* if alternativo:

.. code-block:: LANG 
    :linenos:

    ...

* Operador ternario:

.. code-block:: LANG 
    :linenos:

    ...

Condicional Switch
******************
Estructura de un switch:

.. code-block:: LANG 
    :linenos:

    ...

Bucle for
*********

* for básico:

.. code-block:: LANG 
    :linenos:

    ...

* foreach:

.. code-block:: LANG 
    :linenos:

    ...

* foreach clave / valor:

.. code-block:: LANG 
    :linenos:

    ...

Bucle while
***********

* While sencillo:

.. code-block:: LANG 
    :linenos:

    ...

* do-while:

.. code-block:: LANG 
    :linenos:

    ...

Detener secuenda de script
**************************

.. code-block:: LANG
    :linenos:

    ...

Punteros
########

.. code-block:: LANG 
    :linenos:

    ...

Tipos de datos avanzados
########################

Arrays
******

- Declaración tradicional:

.. code-block:: LANG 
    :linenos:

    ...

- Declaración con función array():

.. code-block:: LANG 
    :linenos:

    ...

- Array multidimensional:

.. code-block:: LANG 
    :linenos:

    ...

* Imprimir y asignar valores:

.. code-block:: LANG 
    :linenos:

    ...

Arrays asociativos
******************

- Declaración tradicional:

.. code-block:: LANG 
    :linenos:

    ...

- Declaración con función array():

.. code-block:: LANG 
    :linenos:

    ...

- Array multidimensional:

.. code-block:: LANG 
    :linenos:

    ...

- Imprimir y asignar valores:

.. code-block:: LANG 
    :linenos:

    ...

Control de errores
##################

.. code-block:: LANG
    :linenos:

    ...

Programación modular
####################

Funciones
*********

* Procedimienos:

.. code-block:: LANG 
    :linenos:

    ...

* funciones:

.. code-block:: LANG 
    :linenos:

    ...

* uso de parámetros:

.. code-block:: LANG 
    :linenos:

    ...

* Funciones anónimas:

.. code-block:: LANG 
    :linenos:

    ...

* Ámbito global:

.. code-block:: LANG 
    :linenos:

    ...

Programación orientada a objetos
################################

Los elementos de una clase se definen con ámbito **public**, **private** y **protected**. 
Adicionalmente se puede agregar el modificador **static** para poder acceder a los atributos y métodos sin crear un objeto.

Clases y objetos
****************

* Estructura clase:

.. code-block:: LANG 
    :linenos:

    ...


* Constructor:

.. code-block:: LANG 
    :linenos:

    ...

* Get y Set:

.. code-block:: LANG 
    :linenos:

    ...

* Modificar Get y Set de Atributos:

.. code-block:: C#
    :linenos:

    ...

* Creación de objeto:

.. code-block:: C#
    :linenos:

    ...

* Herencia:

.. code-block:: LANG 
    :linenos:

    ...

Clases abstractas y resolución de ámbito
****************************************

- uso de clases no instanciables:

.. code-block:: LANG 
    :linenos:

    ...

Interfaces
**********

.. code-block:: LANG 
    :linenos:

    ...

Structs
#######

.. code-block:: LANG
    :linenos:

    ...

Enums
#####

.. code-block:: LANG
    :linenos:

    ...


Importar y exportar
###################

include y require
*****************

* Importar archivos LANG:

.. code-block:: LANG 
    :linenos:

    ...

Namespace
*********

* Exportar (videojuegos.LANG):

    .. code-block:: LANG 
        :linenos:

        ...
    
    * Importar namespace (index.LANG):

    .. code-block:: LANG 
        :linenos:

        ...