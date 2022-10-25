Funciones
=========

.. image:: /logos/JavaScript-logo.png
    :scale: 25%
    :alt: Logo JavaScript
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Sintáxis básica de JavaScript
  
.. contents:: Índice

Manipulación de variables
#########################

Averiguar tipo de dato
**********************

.. code-block:: javascript
    :linenos:

    var cadena = "PlayStation";

    console.log(typeof cadena);

Manipulación de Strings
#######################

Longitud de un String 
*********************

.. code-block:: javascript
    :linenos:

    var consola = "La videoconsola PlayStation fue lanzada en 1995";
    // ajustamos la cantidad de decimales a mostrar:
    console.log(consola.length);
 
Conversión número a String 
**************************

.. code-block:: javascript
    :linenos:

    var num = 23;

    var cadena = String(num);

Conversión String a Array
*************************

.. code-block:: javascript
    :linenos:

    var videoconsolas = "Playstation, Gameboy, PS Vita";

    var arrayConsolas = videoconsolas.split(", ");

    console.log(arrayConsolas);

Reemplazar palabras
*******************

.. code-block:: javascript
    :linenos:

    ...

Primera letra mayúscula
***********************

.. code-block:: javascript
    :linenos:

    ...

Conversión a mayúsculas
***********************

.. code-block:: javascript
    :linenos:

    mensaje = "Cadena de texto";

    // Cadena puesta toda en mayúsculas:
    resultado = mensaje.toUpperCase();

Conversión a minúsculas
***********************

.. code-block:: javascript
    :linenos:

    mensaje = "Cadena de texto";

    // Cadena puesta toda en minúsculas:
    resultado = mensaje.toLowerCase();

Eliminar espacios en blanco a los lados
***************************************

.. code-block:: javascript
    :linenos:

    var mensaje = "         mensaje sin espacios        ";

    resultado = mensaje.trim();

    console.log(resultado);

Localizar posición de caracteres en cadena
******************************************

.. code-block:: javascript
    :linenos:

    var consola = "La videoconsola PlayStation fue lanzada en 1995";
    
    // primera posición de elemento localizado:
    console.log(consola.indexOf("videoconsola"));
    
    // primera posición último elemento localizado:
    console.log(consola.lastIndexOf("videoconsola"));

Manipulación de Números
#######################

Conversión String a Integer
***************************

.. code-block:: javascript
    :linenos:

    var numeroTexto = "25";

    // conversión con función:
    var numero = Number.parseInt(numeroTexto);

Conversión String a Float
*************************

.. code-block:: javascript
    :linenos:

    var numeroTexto = "25.72";

    // conversión con función:
    var numero = Number.parseFloat(numeroTexto);
    console.log(numero);

Redondeo de decimales
*********************

.. code-block:: javascript
    :linenos:

    var numero = 27.29;
    // ajustamos la cantidad de decimales a mostrar:
    console.log(numero.toFixed(0));

Validar numeros
***************

.. code-block:: javascript
    :linenos:

    var numero = NaN;

    console.log(Number.isNaN(numero));
    console.log(Number.isInteger(numero));

Manipulación de Arrays
######################

Comprobar tamaño
****************

.. code-block:: javascript
    :linenos:

    var consolas = ["Playstation", "Gameboy", "Nintendo DS"];

    console.log(consolas.length);

Imprimir contenido
******************

.. code-block:: javascript
    :linenos:

    ...

Rango de números
****************

.. code-block:: javascript
    :linenos:

    ...

Recuperar valor máximo
**********************

.. code-block:: javascript
    :linenos:

    ...

Recuperar valor mínimo
**********************

.. code-block:: javascript
    :linenos:

    ...

Suma total de todos los valores
*******************************

.. code-block:: javascript
    :linenos:

    ...

Manipulación JSON
#################

Convertir Array en JSON 
***********************

.. code-block:: javascript
    :linenos:

    var datoJSON = JSON.stringify(persona);

Convertir JSON en Array 
***********************

.. code-block:: javascript
    :linenos:

    var datoObjeto = JSON.parse(datoJSON);


Manipulación de fechas 
######################

.. code-block:: javascript
    :linenos:

    // Creamos el objeto date con la clase date:
    var fecha = new Date();

    // Cada vez que escribimos new Date() generará una nueva fecha.

    // Ahora podemos obtener el día:
    fecha.getDay();

    // Podemos ver cual es el día del mes:
    fecha.getDate();

    // Y así podemos obtener más tipos de datos como la hora:
    fecha.getHours();

    // Y podemos asignarle fechas:
    fecha.setDate(5);


Tratamiento de archivos
#######################

Recuperar contenido de archivo 
******************************

.. code-block:: javascript
    :linenos:

    ...

Manipulación de archivos
************************

* Escritura de archivos:

.. code-block:: javascript
    :linenos:

    ...

* Lectura de archivos:

.. code-block:: javascript
    :linenos:

    ...

* Actualización de archivos:

.. code-block:: javascript
    :linenos:

    ...

Manipulación de cabeceras
#########################

Redirección
***********

.. code-block:: javascript
    :linenos:

    ...

Modificar el comportamiento de un script
****************************************

.. code-block:: javascript
    :linenos:

    ...

* Lista de MIMES más comunes: https://developer.mozilla.org/es/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types

Descargar un archivo desde un script
************************************

.. code-block:: javascript
    :linenos:

    ...

Tratamiento de CORS
*******************

.. code-block:: javascript
    :linenos:

    ...
 
Manipulación del Sistema
########################

Averiguar el Sistema operativo
******************************

.. code-block:: javascript 
    :linenos:

    ...

Averiguar la arquitectura
*************************

.. code-block:: javascript
    :linenos:

    ...

Math: operaciones matemáticas
#############################

.. code-block:: javascript
    :linenos:

    ...

Random: Números aleatorios
##########################

.. code-block:: javascript
    :linenos:

    ...