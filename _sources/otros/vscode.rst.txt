Visual Studio Code 
==================

.. image:: /logos/logo-vsc.png
    :scale: 15%
    :alt: Logo Visual Studio Code
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Tutorial y herramientas para optimizar visual studio code 
  
.. contents:: Índice

Utilidades 
##########

Extensiones
***********

Las siguientes extensiones son muy útiles para desarrollar con visual studio code:

- Material Theme: Tema muy visual que contiene distintos tipos de colores.
- Material Icon Theme: Tema de iconos que muestra el logo de la tecnología a la que corresponde cada archivo del proyecto y decora carpetas estándares.

Tips
####

Atajos de teclado 
*****************

- Comentar y descomentar varias líneas: **Mayuscula + Alt + a**
- Mover lineas de código: Alt + flecha arriba o abajo. (seleccionar una o varias)
- Tabular líneas: seleccionar líneas y presionar tabulador.
- Quitar tabulación de varias líneas: seleccionar líneas y pulsar mayúscula + tab hasta posicionar.
- Acceder a una función, clase o paquete externo: mantener presioando Ctrl y hacer click con el cursor en el mismo.
- Seleccionar varios elementos con el mismo texto: Seleccionar un texto y presionar ctrl + d varias veces hasta tener todos los que quieras.
- Ocultar sidebar: Ctrl + b
- Activar modo zen: presionar ctrl+k y luego z
- copiar una o varias líneas arriba o abajo: mayuscula + alt + arriba o abajo
- Crear un multicursor para escribir líneas simultaneas: ctrl + alt + flecha arriba o abajo.
- Crear multicursor en líneas separadas: con alt presionado hay que ir seleccionando cada líena o elemento con el ratón.
- Seleccionar uno o varios textos: ctrl + mayuscula + flecha izquierda o derecha una o varias veces.
- Abrir buscador: Ctrl + f

Snippets
########

Crear snippet personalizado  
***************************
 
En Visual Studio Code podemos crear un pedazo de código personalizado para utilizar comunmente:

Paso 1. Pulsamos ctrl + mayuscula + p y escribimos snippet. 
Paso 2. Elegimos la opción configure user snippet y el lenguaje de programación del mismo.
Paso 3. Creamos un snippet:

.. code-block:: javascript
    :linenos:

    {
        "Imprimir mensaje": {
            "prefix": "pt",
            "body": [
                "print(${1:'Imprimiendo un mensaje'})"
            ],
            "description": "Imprime un mensaje escribiendo su prefijo"
        }
    }

Paso 4. Podemos ahora usarlo en un archivo correspondiente con su prefix introduciendo el valor **pt** nos mostrará la opción para rellenar.

.. attention::
    En la siguiente línea **${1:'Imprimiendo un mensaje'}** significa que el cursor cubra ese area para ser reemplazada por otro contenido.
    