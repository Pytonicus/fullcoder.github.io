Eventos y Delegados
===================

.. image:: /logos/logo-csharp.png
    :scale: 80%
    :alt: Logo C#
    :align: center
 
.. |date| date:: 
.. |time| date:: %H:%M
 

Delegados y eventos que corresponden al lenguaje C#

.. contents:: Índice 

Delegados
#########

* Funcionamiento básico de un delegado:

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {
        class Program
        {
            // declaración de un delegado:
            public delegate int RealizarOperacion(int num1, int num2);

            // método suma:
            public static int Suma(int a, int b)
            {
                return a + b;
            }

            // metodo resta:
            public static int Resta(int a, int b)
            {
                return a - b;
            }

            static void Main(string[] args)
            {
                // crear instancia de un delegado y apuntar al metodo suma:
                RealizarOperacion suma = Suma;
                RealizarOperacion resta = Resta;

                // pasarle los valores e imprimir:
                Console.WriteLine(suma(5,18));
                Console.WriteLine(resta(10, 3));

                Console.Read();
            }   
        }
    }

Métodos anónimos
################

Las funciones anónimas se han añadido en este lugar ya que dependen de los delegados para ser creadas:

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {
        class Program
        {
            // se crea un delegado para la función anónima:
            public delegate string RealizarSaludo(string nombre);
            
            static void Main(string[] args)
            {
                // definimos la función anónima con el uso del delegate:
                RealizarSaludo saludar = delegate (string nombre)
                {
                    return "Hola, me llamo " + nombre;
                };

                // uso de la función anónima:
                Console.WriteLine(saludar("Guillermo"));
                Console.Read();
            }   
        }
    }

Expresiones Lambda
##################
 
.. code-block:: C#
    :linenos:
  
    using System;
    using System.Collections.Generic;

    namespace Tipos
    {
        class Program
        {                
            static void Main(string[] args)
            {
                // creamos una lista sencilla:
                List<int> listadoBase = new List<int> { 2, 4, 3, 6, 4, 3, 2, 1, 5, 3 };

                // se puede filtrar la lista usando expresiones lambda:
                List<int> listaPares = listadoBase.FindAll(i => i % 2 == 0);

                foreach(int listado in listaPares)
                {
                    Console.WriteLine(listado);
                }
                Console.Read();
            }   
            
        }
    }

Eventos
#######

PROXIMAMENTE...