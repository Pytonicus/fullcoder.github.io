Funciones predefinidas
======================

.. image:: /logos/logo-csharp.png
    :scale: 80%
    :alt: Logo C#
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M
  

Funciones más usadas en C#

.. contents:: Índice

Manipulación de variables
#########################

Averiguar tipo de dato
**********************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string nombre = "Guillermo";

            Console.WriteLine(nombre.GetType());
            Console.Read();
        }
    }

Validación
**********

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string nombre = "";

            Console.WriteLine(String.IsNullOrEmpty(nombre));
            Console.Read();
        }
    }

Manipulación de Strings
#######################

Longitud de un String 
*********************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            string nombre = "Guillermo";

            // devuelve un valor entero que se puede imprimir directamente: 
            int longitudNombre = nombre.Length;

            Console.WriteLine(longitudNombre);

            Console.Read();
        }

Conversión a String 
*******************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            int numero = 27;

            // convertir a string:
            string numeroStr = Convert.ToString(numero);

            Console.WriteLine(numeroStr);

            Console.Read();
        }

Conversión String a Array
*************************

.. code-block:: C#
    :linenos:

    class Program
    {

        static void Main(string[] args)
        {
            string frutas = "pera limón piña naranja pomelo manzana";

            string[] fruta = frutas.Split(' ');

            Console.WriteLine(fruta[2]);ç
            Console.Read();
        }
    }

Reemplazar palabras
*******************

.. code-block:: C#
    :linenos:

    class Program
    {

        static void Main(string[] args)
        {
            string deseo = "Me voy a convertir en un desarrollador C#";

            string alcance = deseo.Replace("voy a convertir", "he convertido");

            Console.WriteLine(alcance);
            Console.Read();
        }
    }

Conversión a mayúsculas
***********************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string nombre = "Guillermo";

            Console.WriteLine(nombre.ToUpper());

            Console.Read();
        }
    }

Conversión a minúsculas
***********************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string nombre = "Guillermo";

            Console.WriteLine(nombre.ToLower());

            Console.Read();
        }
    }

Eliminar espacios en blanco a los lados
***************************************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string frase = "   Esta frase esta mal formada   ";

            // imprimir quitando espacios a los lados:
            Console.WriteLine(frase.Trim());
            Console.Read();
        }
    }

Localizar posición de caracteres en cadena
******************************************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string frase = "En esta frase se esconde Pepe";

            if (frase.Contains("Pepe"))
            {
                Console.WriteLine("Hemos encontrado a Pepe!");
                Console.Read();
            }
        }
    }

Formatear contenido de una variable con otras
*********************************************

.. code-block:: C#
    :linenos:
    
    class Program
    {
        static void Main(string[] args)
        {
            string frase;

            Console.Write("Introduce tu nombre: ");
            string nombre = Console.ReadLine();
            // con string format podemos usar el formateo:
            frase = String.Format("Te llamas {0}", nombre);

            Console.WriteLine(frase);
            Console.Read();
        }
    }

Manipulación de Números
#######################

Conversión String a Integer
***************************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            string edad = "33";
            int total = Convert.ToInt32(edad);

            Console.WriteLine(total + 10);
            Console.ReadKey();
        }

Conversión String a Double
**************************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            // Reconoce decimales solo con , si tienen punto los tomará como entero Ej: 7866
            string peso = "78,66";

            double pesoReal = Convert.ToDouble(peso);

            Console.WriteLine(pesoReal);
            Console.ReadKey();
        }

Conversión a Double
*******************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            int peso = 78;

            double pesoReal = Convert.ToDouble(peso) + 0.55;

            Console.WriteLine(pesoReal);
            Console.ReadKey();
        }

Double a entero
***************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            double altura = 1.67;

            // Parsing a entero:
            int conversion = Convert.ToInt32(altura);

            Console.WriteLine(conversion);
            Console.ReadKey();

            Console.Read();
        }

Manipulación de Arrays
######################
  
Comprobar tamaño
****************

.. code-block:: C#
    :linenos:

    int[] fechas = new int[] {1987, 1983, 1990, 2011 };
    // ver el tamaño del array:
    Console.WriteLine(fechas.Length);

    // uso en bucle for:
    for(int i = 0; i < fechas.Length; i++)
    {
        Console.WriteLine("Fecha: {0}", fechas[i]);
    }
 
Manipulación de fechas 
######################

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {
        class Program
        {   
            static void Main(string[] args)
            {
                // creamos un objeto datetime con un fecha:
                DateTime fecha = new DateTime(1987, 06, 06);
                // imprimir:
                Console.WriteLine("Nací el " + fecha);

                // Mostrar el día de hoY:
                Console.WriteLine(DateTime.Today);

                // hoy con la hora:
                Console.WriteLine(DateTime.Now);

                // Conocer Mañana:
                Console.WriteLine(DateTime.Today.AddDays(1));

                // Ver solo la fecha:
                Console.WriteLine(DateTime.Now.ToString("F"));

                // Ver solo la hora:
                Console.WriteLine(DateTime.Now.ToString("F"));

                // Fecha formateada:
                Console.WriteLine(DateTime.Now.ToString("dd/MM/yyyy"));

                Console.Read();
            }   
        }
    }

* Códigos comunes para Fecha: 

+----------------------------------------------+---------+
| Tipo de valor                                | símbolo |
+==============================================+=========+
| Día en notación numeral                      | dd      |
+----------------------------------------------+---------+
| Día por inicial                              | ddd     | 
+----------------------------------------------+---------+
| Día de la semana                             | dddd    |
+----------------------------------------------+---------+
| Mes actual en notación numeral               | MM      |
+----------------------------------------------+---------+
| Mes actual en notación numeral sin cero      | M       |
+----------------------------------------------+---------+
| Iniciales del mes corriente                  | MMM     |
+----------------------------------------------+---------+
| Mes en notacion textual                      | MMMM    |
+----------------------------------------------+---------+
| Año corriente en notación numeral            | yyyy    |
+----------------------------------------------+---------+
| Año con notación numeral abreviada           | yy      |
+----------------------------------------------+---------+

* Códigos comunes para Hora:

+----------------------------------------------+---------+
| Tipo de valor                                | símbolo |
+==============================================+=========+
| Hora en formato 12                           | h       |
+----------------------------------------------+---------+
| Hora en formato 24                           | H       |
+----------------------------------------------+---------+
| Hora en formato 12 con 0 inicial             | hh      |
+----------------------------------------------+---------+
| Hora en formato 24 con 0 inicial             | HH      |
+----------------------------------------------+---------+
| Minutos                                      | mm      |
+----------------------------------------------+---------+
| Segundos                                     | ss      |
+----------------------------------------------+---------+
| Milésimas                                    | FFF     |
+----------------------------------------------+---------+
| Zona Horaria                                 | e       |
+----------------------------------------------+---------+
| Horario de sol reducido                      | I       |
+----------------------------------------------+---------+
| Desfase meridiano de Greenwitch              | zz      |
+----------------------------------------------+---------+

Math: operaciones matemáticas
#############################

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {
        class Program
        {   
            static void Main(string[] args)
            {
                // uso de Math:
                Console.WriteLine("Redondeo hacia arriba: " + Math.Ceiling(18.432));
                Console.WriteLine("Redondeo hacia abajo: " + Math.Floor(51.70));
                Console.WriteLine("Valor mas bajo entre {0} y {1} es: {2}", 10, 6, Math.Min(10, 6));
                Console.WriteLine("Valor mas alto entre {0} y {1} es: {2}", 10, 6, Math.Max(10, 6));
                Console.WriteLine("2 elevado a 3 es: " + Math.Pow(2, 3));
                Console.WriteLine("El valor de PI es: " + Math.PI);
                Console.WriteLine("La raiz cuadrada de 12 es: " + Math.Sqrt(12));
                Console.WriteLine("El absoluto de -10 es: " + Math.Abs(10));
                Console.WriteLine("El coseno de 5 es: " + Math.Cos(5));

                Console.Read();
            }
        }
    }

Random: Números aleatorios
##########################

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {
        class Program
        {   
            static void Main(string[] args)
            {
                // Crear objeto random:
                Random aleatorio = new Random();

                // asignar valor aleatorio a numero:
                int numero = aleatorio.Next(1,10); // se puede establecer valor minimo y valor máximo (10 no se incluye en este caso)

                Console.WriteLine(numero);
                Console.Read();
            }
        }
    }