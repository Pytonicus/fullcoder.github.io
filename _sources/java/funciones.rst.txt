Funciones
=========

.. image:: /logos/java-logo.png
    :scale: 25%
    :alt: Logo Java 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Funciones básica de Java
  
.. contents:: Índice

Manipulación de Strings
#######################

 
Conversión número a String 
**************************

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            // Valor numérico:
            int num = 27;
            
            // conversión a cadena:
            String numString = String.valueOf(num);
            
            System.out.println(numString);
        }
    }


Conversión String a char (una letra)
************************************

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            // Tomar un caracter:
            char l = "hola".charAt(2);
            System.out.println(l);
        }
    }

Manipulación de Números
#######################

Conversión String a Integer
***************************

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            
            // numero:
            var edad = "35";
            
            // conversión a entero: 
            int edadInt = Integer.parseInt(edad);
            
            System.out.println(edadInt + 10);
        }
    }


Conversión String a Double 
**************************

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            
            // numero:
            var edad = "35.27";
            
            // conversión a entero: 
            double edadInt = Double.parseDouble(edad);
            
            System.out.println(edadInt + 10);
        }
    }


Redondeo de decimales
*********************
 
.. code-block:: javascript
    :linenos:

    var numero = 27.29;
    // ajustamos la cantidad de decimales a mostrar:
    console.log(numero.toFixed(0));

Casting 
*******

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            // Tenemos un short:
            short a = 10;
            
            // con el casting podemos convertir a un valor inferior con perdida de datos si el dato es mayor:
            byte b = (byte) a;
            
            System.out.println(b);
        }
    }
