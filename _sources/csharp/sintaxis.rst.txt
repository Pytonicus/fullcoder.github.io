Sintaxis C#
===========

.. image:: /logos/logo-csharp.png
    :scale: 80% 
    :alt: Logo C#
    :align: center

.. |date| date::
.. |time| date:: %H:%M

  
Sintáxis básica de C#
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################
 
Instalación
***********
* Instalación: Mediante Visual Studio o Unity.

* Instalación Visual Studio 2019 Windows:
    * Descargamos la versión comunity
    * En carga de trabajo seleccionamos Desarrollo de escritorio de .NET y Desarrollo de la plataforma universal de Windows
    * En la siguiente pestaña de componentes individuales seleccionamos la opción Herramientas de LINQ to SQL

* Instalación Monodevelop Linux:
    * Para usar el IDE MonoDevelop:
        * Añadir Repositorio:
        
        .. code-block:: 
            :linenos:
        
            sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
            echo "deb https://download.mono-project.com/repo/ubuntu vs-bionic main" | sudo tee /etc/apt/sources.list.d/mono-official-vs.list
            sudo apt update
            sudo apt install apt-transport-https dirmngr
        
        * Instalar MonoDevelop:
        
        .. code-block:: 
        
            sudo apt-get install monodevelop

        * Instalar SDK .NET en Linux: https://dotnet.microsoft.com/download/dotnet/sdk-for-vs-code?utm_source=vs-code&amp;utm_medium=referral&amp;utm_campaign=sdk-install

* Extensión de archivos: **.cs**
 
Comentarios
***********

.. code-block:: C#
    :linenos:
 
    // comentario de una línea 

    /* Comentario 
    multilínea */

    /// <summary>
    /// Comentario de documentación XML </summary>

Entrada y salida estandar
*************************
Datos de entrada y salida a través de la consola y/o el navegador.


* Uso de la clase Console:

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            // Salida en consola:
            Console.Write("Mensaje - ");

            // Imprimir y saltar de línea:
            Console.WriteLine("Introduce un valor: ");

            // Leer valor y lo guarda en formato string:
            Console.Write("Escribe tu nombre: ");
            string leerOtroValor = Console.ReadLine();
            Console.WriteLine("Te llamas {0}", leerOtroValor);

            // Leer valor de consola y guardar en variable en formato ASCII:
            int leerValor = Console.Read();
            Console.WriteLine("El valor introducido es: {0}", leerValor);

            // Toma un solo caracter:
            Console.ReadKey();
        }

.. note::
    El uso de Console.Read() es muy útil para evitar que se cierre la consola.

Estructura en C#
*****************

* Crear proyecto: Abrimos VS y pinchamos en Crear un proyecto, luego elegimos Aplicación de consola (.NET Framework o la opción .NET Core si no esta la primera), cambiamos el nombre del proyecto y creamos.

* Código C# puro:

.. code-block:: C#
    :linenos:

    using System;

    namespace HolaMundo
    {
        class Program
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hola FullCoder!");
            }
        }
    }

Concatenación
*************
Concatenación de variables y cadenas se realiza con **+**

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            string nombre = "Guillermo";
            int edad = 33;

            // uso de +:
            Console.WriteLine("Me llamo " + nombre + " y tengo " + edad + " años");

            // uso de template:
            Console.WriteLine("Me llamo {0} y tengo {1} años.", nombre, edad);

            Console.ReadKey();
        }
    

C#-CLI - Comandos de C#
***********************
Al trabajar con C# es poco probable el uso de CLI, así que por ahora se omitirá este apartado.

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: C# 
    :linenos:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;

    namespace Tipos
    {
        class Program
        {
            static void Main(string[] args)
            {
                // declaración:
                int numero;


                // asignación de valores:
                int numeroEntero = 10;
                double comaFlotante = 2.832;
                float otroFlotante = 3.2f;
                string cadena = "cadena de texto";
                bool interruptor = true;

                // Impresión de valores::
                Console.WriteLine("Valor del número: " + numeroEntero);

                // dejamos el read abierto para que no se cierre la consola:
                Console.Read();
            }
        }
    }


* Constantes:

.. code-block:: C#
    :linenos:

    class Program
    {
        // se declara usando const y además se añade el tipo:
        const int fechaNacimiento = 1987;
        static void Main(string[] args)
        {
            Console.WriteLine(fechaNacimiento);
            Console.Read();
        }
    }

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            int operacion;

            int sumar = 2 + 2;
            int restar = 2 - 2;
            int multiplicar = 3 + 5;
            int dividir = 2 / 2;
            int resto = 2 % 1;
        }

* Incremento y decremento:

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            int valor = 10;

            valor = valor++;
            valor = ++valor;
            valor = valor--;
            valor = --valor;
        }

* Asignar operación:

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            int valor = 10;

            valor += 10;
            valor -= 5;
            valor *= 22;
            valor /= 11;
        }

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

* and: **&&**.
* or: **||**.
* not: **!**.

Estructuras de control
######################

Condicional if
**************

* if sencillo:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            int edad = 18;

            if(edad >= 18)
            {
                Console.Write("Eres mayor de edad");
            }

            Console.Read();
        }
    }

* if / else:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            int edad = 11;

            if(edad >= 18)
            {
                Console.Write("Eres mayor de edad");
            }
            else
            {
                Console.Write("Todavía eres menor");
            }

            Console.Read();
        }
    }

* else-if:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Introduce tu edad: ");
            string leer = Console.ReadLine();

            int edad = Convert.ToInt32(leer);

            if(edad >= 65)
            {
                Console.Write("Eres un anciano");
            }else if(edad >= 18)
            {
                Console.Write("Eres mayor de edad");
            }
            else
            {
                Console.Write("Eres menor de edad");
            }

            Console.Read();
        }
    }

* if alternativo:

.. code-block:: C# 
    :linenos:

    class Program
    {

        static void Main(string[] args)
        {
            int edad = 18;
            
            if(edad >= 18)
                Console.WriteLine("Eres mayor de edad");
                
            Console.Read();
        }
    }

.. note::
    Aparte de este if, existe for, foreach y while que comparten la misma forma de operar.

* Operador ternario:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            int cantidad = 200;
            string mensaje;

            mensaje = cantidad >= 500 ? "es una pechá" : "es una mijita";

            Console.Write(mensaje);
            Console.Read();
            
        }
    }

Condicional Switch
******************
Estructura de un switch:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Introduce un comando: ");
            string operacion = Console.ReadLine();

            switch (operacion)
            {
                case "saludar":
                    Console.WriteLine("Hola amigo");
                    break;
                case "fecha":
                    Console.WriteLine("Hoy es " + DateTime.Now.ToString());
                    break;
                case "lenguaje":
                    Console.WriteLine("Esta app esta escrita en C#");
                    break;
                default:
                    Console.WriteLine("Comando no reconocido...");
                    break;
            }

            Console.Read();
        }
    }

Bucle for
*********

* for básico:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            for(int i = 1; i <= 10; i++)
            {
                Console.WriteLine("El valor de contador es: {0}", i);
            }
            Console.Read();
        }
    }

* foreach:

.. code-block:: C# 
    :linenos:

    foreach (string consola in videconsolas)
    {
        Console.WriteLine("Consola: {0}", consola);
    }

Bucle while
***********

* While sencillo:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            int i = 1;
            while (i <= 10)
            {
                Console.WriteLine("El valor de contador es: {0}", i);
                i++;
            }
                
            Console.Read();
        }
    }

* do-while:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            int i = 2;
            do
            {
                Console.WriteLine("El valor de contador es: {0}", i);
            } while (i < 1);
                
            Console.Read();
        }
    }

Tipos de datos avanzados
########################

Arrays
******

* Declaración tradicional:

.. code-block:: C# 
    :linenos:

    // declaración array:
    string[] videconsolas = new string[3];
    // creación y asignación: 
    int[] fechas = new int[] {1987, 1983, 1990, 2011 };

    // carga de elementos manual:
    videconsolas[0] = "Mega Drive";
    videconsolas[1] = "Master System";
    videconsolas[2] = "Saturn";

    // Impresión de elementos:
    Console.WriteLine("Consola de Tercera generación: {0}", videconsolas[1]);

* Array multidimensional:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string[] videconsolas = new string[3];
            // array multidimensional, cuantos más puntos más dimensiones:
            string[,] tabla = new string[,]
            {
                {"", "Nombre", "Apellidos","Edad"},
                {"1", "Guillermo", "Granados Gómez", "33" },
                {"2", "Eduardo", "Lopez Martinez", "34" },
                {"3", "Alfredo", "Alferez Albeniz", "37" }
            };

            // imprimir valores: 
            Console.WriteLine("{0}: {1}, {2}: {3}, {4}: {5} ", tabla[0,1], tabla[1,1], tabla[0,2], tabla[1,2], tabla[0,3], tabla[1,3]);
           
           // insertar datos:
            tabla[4, 0] = "4";
            tabla[4, 1] = "Luna";
            tabla[4, 2] = "García Nuñez";
            tabla[4, 3] = "23";

            Console.Read();
        }
    }

* Array Irregular:

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            // definición y asignación de espacio en primera dimension:
            string[][] valores = new string[3][];

            // en cada dimensión se crea un array:
            valores[0] = new string[3];
            valores[1] = new string[6];
            valores[2] = new string[8];

            // inserción de registros:
            valores[0][3] = "Hola amigo";

            Console.Read();
        }
    }

* Arrays por parámetros:

.. code-block:: C#
    :linenos:

     class Program
    {
        static void Main(string[] args)
        {
            // crear el array:
            int[] numeros = new int[] { 8, 16 };

            // pasar array:
            sumar(numeros);
        }

        // recibir array por funciones:
        static void sumar(int [] numeros)
        {
            int num1 = numeros[0];
            int num2 = numeros[1];
            int total = num1 + num2;

            Console.WriteLine("Total de la operación: " + total);
            Console.Read();
        }
    }

Control de errores
##################

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Por favor introduce un número: ");
            string num = Console.ReadLine();
            // vamos a evitar caracteres no válidos:
            try
            {
                // convertimos el resultado a entero, de modo que si se introduce una letra habrá una excepción:
                int resultado = int.Parse(num);
                Console.WriteLine("El valor es: " + resultado);
            }
            catch (Exception)
            {
                Console.WriteLine("El valor introducido no es un número.");
            }
            Console.Read();
        }
    }

Programación modular
####################
El paradigma de programación de C# es POO, sin embargo es interesante ver en esta sección como crear métodos y llamarlos desde Main.

Métodos
*******

* Método void:

.. code-block:: C# 
    :linenos:

    class Program
    {
        // En la clase principal existe un método principal:
        static void Main(string[] args)
        {
            // ejecutamos el método:
            Mensaje(); // para poder llamarlo debe tener acceso static
            Console.Read(); 
        }

        // este es un método que no devuelve nada (void):
        public static void Mensaje()
        {
            Console.WriteLine("Este método devuelve un mensaje");
        }
    }

* uso de parámetros:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            // pasamos los parámetros:
            Sumar(10, 15); 
            Console.Read(); 
        }

        // se define el tipo de parámetro:
        public static void Sumar(int numUno, int numDos)
        {
            int resultado = numUno + numDos;
            Console.WriteLine("El resultado de {0} + {1} es: {2}", numUno, numDos, resultado);
        }
    }

* retorno de valores:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            // Guardamos la operación en una variable:
            string resultado = Sumar(12, 26);

            Console.WriteLine(resultado);
            Console.Read(); 
        }

        // Se utiliza string en lugar de void para devolver una cadena:
        public static string Sumar(int numUno, int numDos)
        {
            int resultado = numUno + numDos;
            // usamos return y aprovechamos el String.Format en este caso:
            return String.Format("El resultado de {0} + {1} es: {2}", numUno, numDos, resultado);
        }
    }

* Ámbito global o atributos estáticos:

.. code-block:: C# 
    :linenos:

    class Program
    {
        // Los atributos declarados estáticos podemos usarlos en Main:
        public static int num1;
        public static int num2;
        static void Main(string[] args)
        {
            // asignamos valores y usamos con el método Sumar:
            num1 = 10;
            num2 = 73;
            string resultado = Sumar(num1, num2);

            Console.WriteLine(resultado);
            Console.Read(); 
        }

        public static string Sumar(int numUno, int numDos)
        {
            int resultado = numUno + numDos;
            return String.Format("El resultado de {0} + {1} es: {2}", numUno, numDos, resultado);
        }
    }

Programación orientada a objetos
################################

Para crear una clase en Visual Studio hacemos clic derecho sobre el nombre deel proyecto y
le damos a agregar -> clase. Elegimos una clase en blanco.

Clases y objetos
****************

* Estructura clase:

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {
        class Persona
        {
            // atributos de la clase:
            public string nombre;
            public string apellidos;
            public int edad;

            // metodos:
            public void saludo()
            {
                Console.WriteLine("Hola, soy {0} {1}", this.nombre, this.apellidos);
            }
        }
    }
 
.. important::
    Respecto a los modificadores de acceso existen 4 tipos en C#. Public (acceso total), Private (solo acceso desde misma clase),
    Protected (acceso desde la misma clase e hijas), Internal (acceso desde cualquier clase).

* Constructor:

.. code-block:: C# 
    :linenos:

    using System;

    namespace Tipos
    {
        class Persona
        {
            public string nombre;
            public string apellidos;
            public int edad;

            // el constructor:
            public Persona(string nombre, string apellidos, int edad)
            {
                // asignar valores a los atributos de clase con this:
                this.nombre = nombre;
                this.apellidos = apellidos;
                this.edad = edad;
            }

            public void saludo()
            {
                Console.WriteLine("Hola, soy {0} {1}", this.nombre, this.apellidos);
            }
        }
    }

.. note:: 
    Puedes crear varios constructores en una clase que reciban uno o dos parámetros, o todos o ninguno.
    Esto permite que puedas crear objetos con más o menos información.

* Get y Set:

.. code-block:: C# 
    :linenos:

    using System;

    namespace Tipos
    {
        class Persona
        {
            public string nombre;
            public string apellidos;
            public int edad;
            private string dni;
            // método rápido de asignar get y set:
            private string enfermedades { get; set; }

            public Persona(string nombre, string apellidos, int edad)
            {
                this.nombre = nombre;
                this.apellidos = apellidos;
                this.edad = edad;
            }

            // Get y set para trabajar con atributos privados:
            public void SetDNI(string dni)
            {
                this.dni = dni;
            }

            public string GetDNI()
            {
                return this.dni;
            }

            public void saludo()
            {
                Console.WriteLine("Hola, soy {0} {1}", this.nombre, this.apellidos);
            }
        }
    }

* Modificar Get y Set de Atributos:

.. code-block:: C#
    :linenos:

    // tenemos un atributo declarado vacío:
    public int edad
        {
            get
            {
                return edad;
            }
            set
            {   // podemos decirle que si la edad es menor a 18 que ponga 18 siempre o sino la edad nueva: 
                edad = edad < 18 ? 18 : value;
            }
        }

    // versión reducida:
    public int edad
        {
            get => edad;
            set => edad = edad < 18 ? 18 : value;
        }

* Creación de objeto:

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            // crear objeto de la clase:
            Persona guillermo = new Persona("Guillermo", "Granados Gómez", 33);

            // uso de atributo público:
            guillermo.edad = 34;

            // uso de método público:
            guillermo.saludo();

            // uso de atributos privados:
            guillermo.SetDNI("34234234X");
            Console.WriteLine("El DNI: {0}",guillermo.GetDNI());


            Console.Read();
        }
    }

* Destructores:

.. code-block:: C#
    :linenos:

    using System;
    // usaremos esta libería para debug:
    using System.Diagnostics;

    namespace Tipos
    {
        class Persona
        {
            public string nombre;
            public string apellidos;
            public int edad;
            private string dni;

            public Persona(string nombre, string apellidos, int edad)
            {
                this.nombre = nombre;
                this.apellidos = apellidos;
                this.edad = edad;
            }

            public void SetDNI(string dni)
            {
                this.dni = dni;
            }

            public string GetDNI()
            {
                return this.dni;
            }

            public void saludo()
            {
                Console.WriteLine("Hola, soy {0} {1}", this.nombre, this.apellidos);
            }

            // destructor solo se puede usar desde su clase y solo uno:
            ~Persona()
            {
                // vamos a imprmir por depurador:
                Debug.Write("Se ha destruido el objeto");
            }
        }
    }


.. attention::
    Los destructores solo se deben usar cuando se va a devolver algún valor.

Herencia
########

* Clase padre:

.. code-block:: C# 
    :linenos:

    using System;

    namespace Tipos
    {
        // clase padre:
        class Vehiculo
        {
            // crear atributos privados con getter y setters:
            protected int idVehiculo { get; set; }
            protected string marca { get; set; }
            protected string modelo { get; set; }

            // creamos un constructor por defecto por si no establecemos valores en los parámetros:
            public Vehiculo()
            {
                this.idVehiculo = 000000;
                marca = "Marca vehículo";
                modelo = "Modelo del vehículo";
            }

            // constructor parametrizado:
            public Vehiculo(int id, string marca, string modelo)
            {
                this.idVehiculo = id;
                this.marca = marca;
                this.modelo = modelo;
            }

            // arrancar el vehiculo:
            public void Arrancar()
            {
                Console.WriteLine("El vehículo {0} {1} se ha puesto en marcha", this.marca, this.modelo);
                Console.Read();
            }
        }
    }

* Clase hija que hereda:

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {// con : le decimos la clase de donde debe heredad:
        class Formula:Vehiculo
        {
            public int velocidadMax { get; set; }

            // podemos usar los métodos del padre sin problemas:
            public Formula(int id, string marca, string modelo) {
                this.idVehiculo = id;
                this.marca = marca;
                this.modelo = modelo;

            }
            // métodos propios de la clase hija:
            public void Turbo()
            {
                Console.WriteLine("El {0} {1} ha metido el turbo!", this.marca, this.modelo);
                Console.Read();
            }
        }
    }

* Creando objetos:

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {
        class Program
        {
            static void Main(string[] args)
            {
                Vehiculo ford = new Vehiculo(073233, "Ford", "Mustang");
                ford.Arrancar();

                Formula mclaren = new Formula(234323, "Mercedes", "McLaren");
                mclaren.Arrancar();
                mclaren.Turbo();
            }
        }
    }


Interfaces
##########

.. code-block:: C# 
    :linenos:

    interface IPersona
    {
        // definir métodos que tendrán la clase:
        void Comer();
        string Saludar();

    }

    class Gente : IPersona
    {
        public string nombre;

        Gente(string nombre)
        {
            this.nombre = nombre;
        }
        public void Comer()
        {
            Console.WriteLine("{0} va a comer", this.nombre);
            Console.Read();
        }

        public string Saludar()
        {
            return String.Format("{0} dice hola.", this.nombre);
        }
    }

.. note:: 
    En Visual Studio se puede crear una interfaz haciendo click derecho en 
    el nombre del proyecto, agregar y seleccionamos interfaz.

Structs
#######

.. code-block:: C#
    :linenos:

    using System;
    using System.IO;

    namespace Tipos
    {
        class Program
        {   
            // creamos la estructura en la clase:
            struct Videoconsola
            {
                // atributos del struct:
                public string marca;
                public string modelo;

                // constructor:
                public Videoconsola(string marca, string modelo)
                {
                    this.marca = marca;
                    this.modelo = modelo;
                }

                // metodos del struct:
                public void ImprimirMensaje()
                {
                    Console.WriteLine("La videoconsola es {0} {1}", this.marca, this.modelo);
                }
            }

            static void Main(string[] args)
            {
                // declaramos el struct:
                Videoconsola megadrive;

                // asignamos valores y se quita el error:
                megadrive.marca = "Sega";
                megadrive.modelo = "Mega Drive";

                // la diferencia con las clases es que hasta que no asignamos valores a los atributos no podemos usar sus métodos:
                megadrive.ImprimirMensaje();

                Console.Read();
            }
        }
    }

Enums
#####

.. code-block:: C#
    :linenos:

    using System;

    namespace Tipos
    {
        // los enum se declaran a nivel de namespace:
        enum Semana { L, M, X, J, V, S, D=0}; // podemos reorganizar asignando indices numéricos
        class Program
        {   
            static void Main(string[] args)
            {
                // asignar un día:
                Semana lunes = Semana.L;
                // imprimir valor:
                Console.WriteLine(lunes);
                // imprimir posición:
                Console.WriteLine((int)Semana.D);
                Console.Read();
            }
        }
    }


Importar y exportar
###################

Namespace
*********
Los namespace o espacios de nombre en C# sirven para organizar sus clases.
Puedes ver más detalles en su documentación oficial: https://docs.microsoft.com/es-es/dotnet/csharp/programming-guide/namespaces/

