Namespace System
================
 
.. image:: /logos/logo-csharp.png
    :scale: 80%
    :alt: Logo C#
    :align: center 

.. |date| date:: 
.. |time| date:: %H:%M
 

Namespace de uso común en C#

.. contents:: Índice

System.Collections
##################

ArrayList 
*********
 
Los arrayList son un tipo de array que puede contenter valores mixtos.

.. code-block:: C#
    :linenos:

    using System;
    // cargamos la librería Collections:
    using System.Collections;

    namespace Tipos
    {

        class Program
        {
            static void Main(string[] args)
            {
                // arrayList de tamaño definido:
                ArrayList miListaLimitada = new ArrayList(10);
                // arrayList de tamaño dinámico:
                ArrayList miLista = new ArrayList();

                // agregar elementos de cualquier tipo:
                miLista.Add(30);
                miLista.Add("Alfredo");
                miLista.Add(true);

                // eliminar elemento:
                miLista.Remove("Alfredo");

                // eliminar elementos de un arrayList por posición:
                miLista.RemoveAt(1);

                // eliminar por rango ej: a partir del índice 2 borrar dos elementos (índice 3 y 4):
                lista.RemoveRange(2, 2);

                // ordenar elementos por su valor:
                miLista.Sort();

                // Comprobar cuantos elementos tiene el ArrayList:
                Console.WriteLine(miLista.Count);

                // comprobar si existe un valor en la lista:
                Console.WriteLine(miLista.Contains(66.62));

                // encontrar la posición de un valor de la list:
                Console.WriteLine(miLista.FindIndex(x => x == 66.62));

                // vaciar lista
                miLista.Clear();

                Console.Read();

            }
        }
    }

Listas
******

Las listas son idénticas a los arrays salvo que se pueden añadir o quitar elementos del mismo a través de métodos específicos.

.. code-block:: C#
    :linenos:

    using System;
    // cargamos Collections generic para listas de un solo tipo:
    using System.Collections.Generic;

    namespace Tipos
    {
        class Program
        {
            static void Main(string[] args)
            {
                // crear una lista vacia:
                var precios = new List<double>();

                // crear una lista con valores asignados:
                var preciosIva = new List<double> { 5.23, 6.21, 32.26, 66.62 };

                // añadir valores:
                preciosIva.Add(15.23);

                // eliminar elemento por su valor:
                preciosIva.Remove(6.21);

                // eliminar elemento por su índice:
                preciosIva.Remove(0);

                // ordenar elementos por su valor:
                preciosIva.Sort();

                // Comprobar cuantos elementos tiene la lista:
                Console.WriteLine(preciosIva.Count);

                // comprobar si existe un valor en la lista:
                Console.WriteLine(preciosIva.Contains(66.62));

                // encontrar la posición de un valor de la list:
                Console.WriteLine(preciosIva.FindIndex(x => x == 66.62));

                // vaciar lista
                preciosIva.Clear();

                Console.Read();
            }
        }
    }

Diccionarios
************
Los diccionarios son un tipo de dato similar a sus homónimos en Python o los objetos en javaScript:

.. code-block:: C#
    :linenos:

    using System;
    using System.Collections.Generic;

    namespace diccio
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                // crear un diccionario:
                Dictionary<string, string> consolas = new Dictionary<string, string>();

                // agregar elementos
                consolas.Add("nombre", "PlayStation");
                consolas.Add("marca", "Sony");
                consolas.Add("lanzamiento", "1994");

                // utilizar elementos:
                Console.WriteLine("La videoconsola {0} {1} fue lanzada en el año {2}", consolas["marca"], consolas["nombre"], consolas["lanzamiento"]);


                // crear diccionario y asignar valores directamente:
                Dictionary<string, string> userPedro = new Dictionary<string, string>()
                {
                    {"nombre", "Pedro"},
                    {"apellidos", "Lopez Aguirrez"},
                    {"Edad", "33"}
                };

                // Recorrer elementos del diccionario:
                foreach (KeyValuePair<string, string> usuario in userPedro)
                {
                    Console.WriteLine("{0}: {1}", usuario.Key, usuario.Value);
                }



                Console.Read();
            }
        }
    }


* Ejemplo de listado de diccionarios:

.. code-block:: C#
    :linenos:

    using System;
    using System.Collections.Generic;

    namespace diccio
    {
        class MainClass
        {
            public static void Main(string[] args)
            {
                // crear un listado para diccionarios:
                List<Dictionary<string, string>> usuarios = new List<Dictionary<string, string>>();

                // crear diccionarios:
                Dictionary<string, string> userPedro = new Dictionary<string, string>()
                {
                    {"nombre", "Pedro"},
                    {"apellidos", "Lopez Aguirrez"}
                };
                Dictionary<string, string> userPaco = new Dictionary<string, string>()
                {
                    {"nombre", "Paco"},
                    {"apellidos", "Ortega Marín"}
                };
                Dictionary<string, string> userJulia = new Dictionary<string, string>()
                {
                    {"nombre", "Julia"},
                    {"apellidos", "Gamez Gómez" }
                };

                // añadir elementos al listado:
                usuarios.Add(userPedro);
                usuarios.Add(userPaco);
                usuarios.Add(userJulia);



                foreach (Dictionary<string, string> usuario in usuarios)
                {
                    Console.WriteLine("Usuario: {0} {1}", usuario["nombre"], usuario["apellidos"]);
                }

                Console.Read();
            }
        }
    }


System.IO
#########

Leer archivo 
************

.. code-block:: C#
    :linenos:

    using System;
    // Cargar librería:
    using System.IO;

    namespace Tipos
    {

        class Program
        {

            static void Main(string[] args)
            {
                // cargar texto. El caracter @ normaliza la ruta:
                string archivo = File.ReadAllText(@"C:\textos\texto.txt");

                Console.WriteLine(archivo);
                Console.Read();
            }
        }
    }

Manipulación de archivos
************************

* Escritura de archivos:

.. code-block:: C#
    :linenos:

    using System;
    using System.IO;

    namespace Tipos
    {

        class Program
        {

            static void Main(string[] args)
            {
                // se guarda en un array y esta vez usamos ReadAllLines:
                string[] archivo = File.ReadAllLines(@"C:\textos\texto.txt");

                // recorremos con un foreach:
                foreach(string linea in archivo)
                    Console.WriteLine("\t" + linea);
                    
                Console.Read();
            }
        }
    }

* Lectura de archivos:

.. code-block:: C#
    :linenos:

    using System;
    using System.IO;

    namespace Tipos
    {

        class Program
        {

            static void Main(string[] args)
            {
                // se genera un array con las líneas que irán en el texto:
                string[] lineas = { "Titulo: La casa de Cera", "Descripción: es una novela de miedito." };
                // se guarda en una ruta:
                File.WriteAllLines(@"C:\textos\novela.txt", lineas);

                Console.WriteLine("Se ha escrito el archivo");
                    
                Console.Read();
            }
        }
    }

* Actualización de archivos:

.. code-block:: C#
    :linenos:

    using System;
    using System.IO;

    namespace Tipos
    {
        class Program
        {

            static void Main(string[] args)
            {
                // para actualizar el archivo hacemos uso de Streamwritter, no olvides añadir true para que no sobreescriba:
                using(StreamWriter archivo = new StreamWriter(@"C:\textos\novela.txt", true))
                {
                    archivo.WriteLine("Calificación: 8/10");
                }
                Console.WriteLine("Añadido con éxito");
                    
                Console.Read();
            }
        }
    }

* Ejemplo: Uso de StreamWriter para crear un procesador de texto:

.. code-block:: C#
    :linenos:

    using System;
    using System.IO;

    namespace Tipos
    {
        class Program
        {

            static void Main(string[] args)
            {
                Console.Write("Título del archivo: ");
                string titulo = Console.ReadLine();

                string texto = "";

                using (StreamWriter archivo = new StreamWriter(@"C:\textos\" + titulo + ".txt", true))
                {

                    while (texto != "fin")
                    {
                        Console.WriteLine("Escribe una línea: ");
                        texto = Console.ReadLine();
                        archivo.WriteLine(texto);
                    }
                }
            }
        }
    }
  