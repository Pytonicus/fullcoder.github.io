
Documentación en Java 
=====================

.. image:: /logos/java-logo.png
    :scale: 25%
    :alt: Logo Java
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Sintáxis básica de Java
  
.. contents:: Índice

Javadoc
#######

Crear documentación 
*******************

En un archivo java se crea la documentaación con comentarios:

.. code-block:: java 
    :linenos:

    package com.mycompany.videoconsolas;

    /**
    * Prueba de documentación Javadoc
    * 
    * @author Guillermo Granados Gómez
    * @version 1.0
    */

    public class Consola {
        /**
        * Marca de Consola
        */
        public String marca;
        /**
        * Modelo de Consola
        */
        public String modelo;
        /**
        * Año de lanzamiento de Consola
        */
        public int lanzamiento;
        
        /**
        * Constructor padre, lanza un mensaje cuando se crea el objeto
        */
        private Consola(){
            System.out.println("Se ha creado el objeto consola");
        }
        
        /**
        * Constructor hijo, carga los parámetros en los atributos de la clase
        */
        public Consola(String marca, String modelo, int lanzamiento){
            this();
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
        }
        
        /**
        * Muestra informaación de un objeto consola.
        */
        public void info(){
            System.out.println("La consola " + marca + " " + modelo + " fue lanzada en " + lanzamiento);
        } 

        /**
        * Muestra el nombre completo del dispositivo.
        */
        public String nombre(){
            return marca + " " + modelo;
        }

        /**
        * Recibe un nombre e indica de quién es la consola.
        */
        public String propietario(String nombre){
            return "La consola " + marca + " " + modelo + " es de " + nombre;
        }
        
    }

Compilar y crear javadoc 
************************

1. Hacemos click derecho en el nombre del proyecto y seleccionar la opción **Click and build**
2. Nuevamente click derecho en el nombre del proyecto y seleccionar **Generate Javadoc**
3. El archivo html se genera dentro de la ruta **nombreProyecto/target/site/apidocs/allpackages-index.html**

En la carpeta apidocs tenemos toda la documentación estructurada de todas las clases.

