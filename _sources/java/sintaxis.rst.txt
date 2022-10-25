Sintaxis Java 
=============

.. image:: /logos/java-logo.png
    :scale: 25%
    :alt: Logo Java
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Sintáxis básica de Java
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################

Instalación
***********
* Instalación: Instalar el JDK de Java desde su página oficial.
* Extensión de archivos: **.java**
 
Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: java
    :linenos:
 
    // comentario de una sola linea

* Comentarios multilínea:

.. code-block:: java
    :linenos:

    /* Comentario 
    multilinea 
    en Java */

Entrada, salida estandar y concatenación 
****************************************
Datos de entrada y salida a través de la consola y/o el navegador.

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;
    // para la entrada estandar hay que cargar la librería scanner:
    import java.util.Scanner;


    public class HolaMundo {
        
        public static void main(String args[]){
            
            // Salida estandar
            System.out.println("Entrada estandar");
            
            System.out.println("Introduce tu nombre: ");
            // entrada estandar:
            Scanner scanner = new Scanner(System.in);
            // guardamos el valor en una nueva variable (var es la versión mas moderna):
            var nombre = scanner.nextLine();
            // hay que usar la variable en java siempre:
            System.out.println("Te llamas " + nombre);
            
        }
    }


Estructura en Java
******************

* Código java del archivo principal:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        
        public static void main(String args[]){
            System.out.println("Hola amigo desde java");
        }
    }


Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            
            // tipos primitivos:
            byte byteVar = 15; // valor máximo 127 (byte.MAX_VALUE . byte.MIN_VALUE)
            short shortVar = 100; // valor máximo 32767 (short.MAX_VALUE . short.MIN_VALUE)
            int intVar = 25054; // valor máximo  2147483647 (Integer.MAX_VALUE . (Integer.MIN_VALUE)
            long longVar = 1839744L; // usa L final, valor máximo 9223372036854775808 (long.MAX_VALUE . long.MIN_VALUE)
            
            // tipos binario, octal y hexadecimal:
            int numeroDecimal = 10;
            int numeroOctal = 012; // añadir un 0 para que reconozca valor octal
            int numeroHexadecimal = 0xA; // añadir 0x para reconocer un hexadecimal
            int numeroBinario = 0b1010; // se añade 0b al inicio para reconocer binario
            
            // tipos flotantes:
            float floatVar = 10.73F; // tipo coma flotante (requiere F si no es double)
            double doubleVar = 12.373; // tipo double
            
            // tipos caracteres:
            char charVar  = 'a'; // comillas simples un caracter
            String stringVar = "Hola"; // comillas dobles para cadenas
            
            // tipo booleano:
            boolean boolVar = true; // o false
            
            // tipo abierto (int, long, string):
            var edad = 85; // si ponemos una L al final se convierte en long
        }
    }

* Constantes:

.. code-block:: java
    :linenos:

    static final DIAS_SEMANA = 7;

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: java
    :linenos:

    var suma = 10 + 20;
    var resta = 10 - 10;
    var multiplicar = 10 * 2;
    var division = 6 / 2;
    var resto = 10 % 3;

* Incremento y decremento:

.. code-block:: java
    :linenos:

    // Incremento
    var dato = 10;
    dato++
    // decremento:
    dato--

* Asignar operación:

.. code-block:: java
    :linenos:

    suma += 10 ;
    resta -= 10;
    multiplicar *= 10;
    division /= 6;
    resto %= 10;

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

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    import java.util.Scanner;

    public class HolaMundo {
        
        public static void main(String args[]){
            // se prepara la entrada:
            Scanner scanner = new Scanner(System.in);
            
            // Se imprime un mensaje:
            System.out.println("Introduce tu edad: ");
            System.out.print(">>> ");
            
            // recibimos la edad:
            int edad = scanner.nextInt();
            
            if(edad >= 18){
                System.out.println("Eres un anciano");
            }
            
        }
    }


* if / else:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    import java.util.Scanner;

    public class HolaMundo {
        
        public static void main(String args[]){
            // se prepara la entrada:
            Scanner scanner = new Scanner(System.in);
            
            // Se imprime un mensaje:
            System.out.println("Introduce tu edad: ");
            System.out.print(">>> ");
            
            // recibimos la edad:
            int edad = scanner.nextInt();
            
            if(edad >= 18){
                System.out.println("Eres un anciano");
            }else{
                System.out.println("Eres menor de edad");
            }
            
        }
    }


* else-if:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    import java.util.Scanner;

    public class HolaMundo {
        
        public static void main(String args[]){
            // se prepara la entrada:
            Scanner scanner = new Scanner(System.in);
            
            // Se imprime un mensaje:
            System.out.println("Introduce tu edad: ");
            System.out.print(">>> ");
            
            // recibimos la edad:
            int edad = scanner.nextInt();
            
            if(edad >= 65){
                System.out.println("Eres un anciano");
            }else if(edad >= 18){
                System.out.println("Eres mayor de edad");
            }else{
                System.out.println("Eres menor de edad");
            }
            
        }
    }


* Operador ternario:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    import java.util.Scanner;

    public class HolaMundo {
        
        public static void main(String args[]){
            // se prepara la entrada:
            Scanner scanner = new Scanner(System.in);
            
            // Se imprime un mensaje:
            System.out.println("Introduce tu edad: ");
            System.out.print(">>> ");
            
            // recibimos la edad:
            int edad = scanner.nextInt();
            
            // realizar el ternario:
            var resultado = edad >= 18 ? "Eres mayor de edad" : "Eres menor de edad";
            
            System.out.println(resultado);
            
        }
    }

.. attention::
    Para utilizar el operador ternario solo se puede usar la expresión var para declarar el resultado.


Condicional Switch
******************
Estructura de un switch:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import java.util.Scanner;

    public class HolaMundo {
        
        public static void main(String args[]){
            // se prepara la entrada:
            Scanner scanner = new Scanner(System.in);
            
            // Se imprime un mensaje:
            System.out.println("Introduce una opción del 1 al 5: ");
            System.out.print(">>> ");
            
            // recibimos la opción:
            String opcion = scanner.nextLine();
            
            // switch:
            switch(opcion){
                case "1":
                    System.out.println("Elegiste la opción 1");
                    break;
                case "2":
                    System.out.println("Elegiste la opción 2");
                    break;
                case "3":
                    System.out.println("Elegiste la opción 3");
                    break;
                case "4":
                    System.out.println("Elegiste la opción 4");
                    break;
                case "5":
                    System.out.println("Elegiste la opción 5");
                    break;
                default:
                    System.out.println("Opción no reconocida");
            }
        }
    }

Bucle for
*********

* for básico:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        
        public static void main(String args[]){
            for(var i = 0; i <= 10; i++){
                System.out.println("Iteración nº " + i);
            }
        }
    }


* foreach:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String[] args) {
            // array numerico:
            int fechas[] = {1997, 2001, 2018, 2022};

            // foreach en array:
            for(int fecha: fechas){
                System.out.println("- Fecha: " + fecha);
            }
        }
    
    }


Bucle while
***********

* While sencillo:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            var contador = 0;
            while(contador < 10){
                System.out.println("Ejecución nº " + contador);
                contador++;
            }
        }
    }


* do-while:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            var contador = 10;
            do{
                System.out.println("Ejecución nº " + contador);
                contador++;
            }while(contador < 10);
        }
    }

Detener secuenda de script
**************************

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            var contador = 0;
            while(contador < 10){
                System.out.println("Ejecución nº " + contador);
                contador++;
                if(contador == 5){
                    break;
                }
            }
        }
    }



Tipos de datos avanzados
########################

Arrays
******

- Declaración tradicional:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    import com.mycompany.videoconsolas.Consola;

    public class HolaMundo {
        
        public static void main(String args[]){
            // los arrays en java son de tipo object así que hay que construirlos:
            String consolas[] = new String[3]; // definimo por ejemplo 3 casillas.
            
            // asignar valores usando indices (no es neceasrio usar todas las casillas:
            consolas[0] = "Nintendo Switch";
            consolas[1] = "Sega MegaDrive";
            consolas[2] = "Super Nintendo";
            
            // acceder a datos de un índice:
            System.out.println(consolas[1]);
            
            // se puede también crear arreglos de tipo objeto en base a una clase
            Consola videoconsolas[] = new Consola[2];
            
            // y creamos objetos:
            videoconsolas[0] = new Consola("Nintendo", "Switch", 2017);
            videoconsolas[1] = new Consola("Sega", "Dreamcast", 1998);
            // acceder a métodos y atributos:
            System.out.println(videoconsolas[1].getMarca());
        }
    }


- Recorrer array con bucle for:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        
        public static void main(String args[]){
            String consolas[] = new String[3]; 
            
            consolas[0] = "Nintendo Switch";
            consolas[1] = "Sega MegaDrive";
            consolas[2] = "Super Nintendo";
            
            // recorrer elementos de un array:
            for(int i = 0; i < consolas.length; i++){
                System.out.println(consolas[i]);
            }
        }
    }

Matrices o arrays multidimensional 
**********************************

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            // las matrices cuentan con múltiples dimensiones [fila][columna]:
            String consolas[][] = new String[3][2]; 
            
            consolas[0][0] = "Nintendo Switch";
            consolas[0][1] = "2017";
            consolas[1][0] = "Sega MegaDrive";
            consolas[1][1] = "1989";
            consolas[2][0] = "Super Nintendo";
            consolas[2][1] = "1992";
            
            // recorrer elementos de un array anidando for:
            for(int i = 0; i < consolas.length; i++){
                for(int j = 0; j < consolas[i].length; j++){
                    System.out.print(consolas[i][j] + " ");
                }
                System.out.println("");
            }
        }
    }


Colecciones
***********

Las colecciones son similares a objetos literales, diccionarios y otros terminos en otros lenguajes de programación.
Estas colecciones tienen tres tipos de formatos **List**, **Set** y **Map**, pero cada uno tiene sus limitaciones.

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    // se importa del paquete util las arraylist y las list:
    import java.util.*; // o todos con *

    public class HolaMundo {
        
        public static void main(String[] args) {
        
            // creamos una lista con la clase list:
            List consolas = new ArrayList();
            
            // añadir elementos:
            consolas.add("Nintendo switch");
            consolas.add("Nintendo switch");
            consolas.add("Nintendo DS");
            
            // recorrer lista:
            for(Object consola: consolas){
                System.out.println(consola);
            }
            
            // Hacemols lo mismo con los sets:
            Set videoconsolas = new HashSet();
            
            // añadir elementos:
            videoconsolas.add("Nintendo switch");
            videoconsolas.add("Nintendo switch");
            videoconsolas.add("Nintendo DS");
            
            // al recorrer lista vemos que ha ordenado elementos y que no añade el elemento repetido:
            for(Object consola: videoconsolas){
                System.out.println(consola);
            }
            
            // Los mapas usan clave-valor:
            Map vConsolas = new HashMap();
            
            // añadir elemento con su clave y su valor:
            vConsolas.put("marca", "Nintendo");
            vConsolas.put("Modelo", "Switch");
            vConsolas.put("Lanzamiento", 2017);
            
            // para imprimir las claves usamos el metodo keySet:
            System.out.println(vConsolas.keySet());
            // para imprimir los valores usamos values:
            System.out.println(vConsolas.values());
            
            // recorrer elementos (solo se pueden recorrer claves o valores:
            for(Object key: vConsolas.keySet()){
                System.out.print("- " + key);
            }
        }
    
    }


Control de errores
##################

Crear excepciones
*****************

- Se crea una nueva clase en el proyecto en un paquete nuevo para controlar los errores:

.. code-block:: java 
    :linenos:

    package com.mycompany.errors;

    // la clase para crear el error hereda del padre Exception:
    public class EdadException extends Exception {
        // se crea un constructor que recibirá un mensaje de error:
        public EdadException(String mensaje){
            // al constructor padre se le pasa el mensaje:
            super(mensaje);
        }
    }

* Ahora se utiliza la excepción en una clase:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import com.mycompany.errors.EdadException;

    public class HolaMundo {
        // al método utilizado se le debe añadir los throws de la excepción creada:
        public static void main(String[] args) throws EdadException {
        int edad = -10;
        
        // si la edad es menor a 0:
        if(edad < 0){
            // se lanzará nuestra excepción:
            throw new EdadException("La edad no puede ser un valor negativo");
        }
        }
    
    }

Esto lanzará un mensaje de error con la excepción que mostrará el mensaje que hemos creado.

Controlar excepción 
*******************

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import com.mycompany.errors.EdadException;

    public class HolaMundo {
        // al método utilizado se le debe añadir los throws de la excepción creada:
        public static void main(String[] args) {
        int edad = -10;
        
        // controlamos la excepción con try catch:
        try{
            // si la edad es menor a 0:
                if(edad < 0){
                    // se lanzará nuestra excepción:
                    throw new EdadException("La edad no puede ser un valor negativo");
                }
        }catch(EdadException error){ // evitamos así que finalice la ejecución abruptamente
            // se puede recuperar el mensaje de error:
            System.out.println(error.getMessage());
            // se puede recuperar la traza de error:
            error.printStackTrace();
        }
        
        System.out.println("Ya no se interrumpe la ejecución");
        
        
        }
    
    }


Programación modular
####################

El tipo de paradigma que usa Java es usualmente Programación orientada a objeto, de modo que utiliza métodos en lugar de funciones.

Programación orientada a objetos
################################

Los elementos de una clase se definen con ámbito **public**, **private** y **protected**. 
Adicionalmente se puede agregar el modificador **static** para poder acceder a los atributos y métodos sin crear un objeto.

Clases y objetos
****************

En un IDE como NetBeans se hace click derecho en Source packages y en la opción New class.

* Estructura clase:

.. code-block:: java
    :linenos:

    // se genera la ruta al paquete si lo hemos seleccionado:
    package com.mycompany.holamundo;

    // se crea el nombre de la clase:
    public class Consola {
        // atributos:
        String marca;
        String modelo;
        int lanzamiento;
        
        // metodos:
        public void info(){
            System.out.println("La consola " + marca + " " + modelo + " fue lanzada en " + lanzamiento);
        } 
    }

* Métodos:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    public class Consola {
        String marca;
        String modelo;
        int lanzamiento;
        
        // metodo que no retorna nada o void:
        public void info(){
            System.out.println("La consola " + marca + " " + modelo + " fue lanzada en " + lanzamiento);
        } 
        
        // método que retorna un valor:
        public String nombre(){
            return marca + " " + modelo;
        }
        
        // metodo que recibe parámetros:
        public String propietario(String nombre){
            return "La consola " + marca + " " + modelo + " es de " + nombre;
        }
    }

* Operador spread:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            // cargar distintos elementos en la función:
            listaConsolas("Nintendo Switch", "PS4", "Xbox One");
        }
        
        // cargar el operador spread el cual creará un array de strings:
        public static void listaConsolas(String... consolas){
            for(var i = 0; i < consolas.length; i++){
                System.out.println("- " + consolas[i]);
            }
        }
    }



* Creación de objeto en clase principal:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        
        public static void main(String args[]){
            // crear objeto:
            Consola nsw = new Consola();
            
            // asignar datos:
            nsw.marca = "Nintendo";
            nsw.modelo = "Switch";
            nsw.lanzamiento = 2017;
            
            // Ejecutar método:
            nsw.info();
            
            // pasar parámetros:
            String propietario = nsw.propietario("Guillermo");
            
            System.out.println(propietario);
        }
    }

* Constructores en clases:

.. code-block:: java 
    :linenos:
    
    package com.mycompany.holamundo;

    public class Consola {
        // lo normal es tener encapsulado los atributos como este caso:
        private String marca;
        private String modelo;
        private int lanzamiento;
        
        // método constructor lleva exactamente el mismo nombre que la clase:
        public Consola(String marca, String modelo, int lanzamiento){
            // cargar valores proporcionados al objeto en el constructor:
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
            
            // mensaje de prueba:
            System.out.println("Se ha creado el objeto consola");
        }
        
        public void info(){
            System.out.println("La consola " + marca + " " + modelo + " fue lanzada en " + lanzamiento);
        } 
        
        public String nombre(){
            return marca + " " + modelo;
        }
        
        public String propietario(String nombre){
            return "La consola " + marca + " " + modelo + " es de " + nombre;
        }
    }


.. attention::
    Se pueden crear mas de un constructor según la necesidad, por ejemplo si queremos tener valores default creamos un
    constructor vacío con los valores que queramos y otro para añadir valores personalizados como el caso anterior.

* Constructores en objetos:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        
        public static void main(String args[]){
            // crear objeto y añadir datos al constructor:
            Consola nsw = new Consola("Nintendo", "Switch", 2017);
            
            
            nsw.info();
            
            String propietario = nsw.propietario("Guillermo");
            
            System.out.println(propietario);
        }
    }

* Sobrecarga de constructores:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    public class Consola {
        public String marca;
        public String modelo;
        public int lanzamiento;
        
        // constructor padre:
        private Consola(){
            System.out.println("Se ha creado el objeto consola");
        }
        
        // constructor hijo:
        public Consola(String marca, String modelo, int lanzamiento){
            // requiere la función reservada this:
            this();
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
        }
        
        public String getMarca(){
            return this.marca;
        }
        
        public void setMarca(String marca){
            this.marca = marca;
        }
        
        public void info(){
            System.out.println("La consola " + marca + " " + modelo + " fue lanzada en " + lanzamiento);
        } 

        public String nombre(){
            return marca + " " + modelo;
        }

        public String propietario(String nombre){
            return "La consola " + marca + " " + modelo + " es de " + nombre;
        }
        
    }

.. attention::
    Java llama a todos los constructores a la hora de crear objetos

* Get y Set (clase):

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    public class Consola {
        // los atributos son privados y no se puede acceder a ellos fuera de la clase:
        private String marca;
        private String modelo;
        private int lanzamiento;
        
        public Consola(String marca, String modelo, int lanzamiento){
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
            
            System.out.println("Se ha creado el objeto consola");
        }
        
        // para ello usamos los getters y setters:
        public String getMarca(){
            // el get retorna el atributo:
            return this.marca;
        }
        
        public void setMarca(String marca){
            // modificar el atributo externamente:
            this.marca = marca;
        }
        
        // se hace lo mismo con el resto de atributos que vayan a usarse externamente
        
    }

.. attention:: 
    Si el atributo con el que trabajamos es booleano se cambia el get por is es decir **isReal()** que retorna True o False.

* Get y Set (objeto):

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        
        public static void main(String args[]){
            Consola nsw = new Consola("Nintendo", "Switch", 2017);
            
            // modificar la marca:
            nsw.setMarca("Sega");
            
            // ver la marca (el único valor que podemos cargar:
            System.out.println(nsw.getMarca());
        }
    }

* Información encapsulada con toString (clase):

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    public class Consola {
        private String marca;
        private String modelo;
        private int lanzamiento;
        
        public Consola(String marca, String modelo, int lanzamiento){
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
            
            System.out.println("Se ha creado el objeto consola");
        }
        
        public String getMarca(){
            return this.marca;
        }
        
        public void setMarca(String marca){
            this.marca = marca;
        }
        
        // toString hace referencia informativa con que atributos cuenta la clase:
        @Override // al existir el método toString de la clase raiz object se anota la sobrecarga
        public String toString(){
            return "Consola(" + "marca=" + this.marca + ", modelo=" + this.modelo + ", lanzamiento=" + this.lanzamiento + ")";
        }
        
    }

* Información encapsulada con toString (objeto):

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        
        public static void main(String args[]){
            Consola nsw = new Consola("Nintendo", "Switch", 2017);
            
            // uso del método toString:
            System.out.println(nsw.toString());
        }
    }

* Ámbito estático:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        // en la clase principal no se puede acceder a atributos a menos que sean estaticos:
        public static String nombre = "Guillermo";
        
        public static void main(String args[]){
            
            hola();
            
            nombre = "Pepe";
        }
        // pasa lo mismo con los métodos:
        public static void hola(){
            System.out.println("Hola colega");
        }
    }


* Herencia (clase padre Consola):

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    // tenemos la clase Padre:
    public class Consola {
        private String marca;
        public String modelo;
        public int lanzamiento;
        
        public Consola(String marca, String modelo, int lanzamiento){
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
            
            System.out.println("Se ha creado el objeto consola");
        }
        
        public String getMarca(){
            return this.marca;
        }
        
        public void setMarca(String marca){
            this.marca = marca;
        }
        
        public void info(){
            System.out.println("La consola " + marca + " " + modelo + " fue lanzada en " + lanzamiento);
        } 

        public String nombre(){
            return marca + " " + modelo;
        }

        public String propietario(String nombre){
            return "La consola " + marca + " " + modelo + " es de " + nombre;
        }
        
        @Override 
        public String toString(){
            return "Consola(" + "marca=" + this.marca + ", modelo=" + this.modelo + ", lanzamiento=" + this.lanzamiento + ")";
        }
        
    }

.. attention::
    Si agregamos el modificador final en la declaración de la clase **public final class Consola** no se podrá heredar de esta.
    En caso de utilizarlo en atributos o métodos funciona como una constante, una vez declarado ya no se podrá sobrecargar.

* Herencia (Clase hija ConsolaPortatil):

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    // La clase consola portatil heredará atributos y métodos de consola:
    public class ConsolaPortatil extends Consola{
        // atributos de esta clase:
        private String TipoBaterias;
        
        // el constructor lleva la palabra super para usar los atributos del padre:
        public ConsolaPortatil(String marca, String modelo, int lanzamiento, String TipoBaterias){
            // pasamos los atributos correspondientes al padre:
            super(marca, modelo, lanzamiento);
            
            // cargamos los atributos del hijo:
            this.TipoBaterias = TipoBaterias;
        }
        
        // creamos sus getter y setters:
        public String getTipoBaterias(){
            return this.TipoBaterias;
        }
        
        public void setTipoBaterias(String TipoBaterias){
            this.TipoBaterias = TipoBaterias;
        }
        
        // y también podemos crear métodos propios además de usar los del padre:
        public void bateria(){
            System.out.println("El tipo de batería que usa " + this.getMarca() + " " + this.modelo + " es de tipo: " + this.TipoBaterias);
        }
        
        // También se sobreescriben los métodos del padre si es necesario:
        @Override
        public void info(){
            System.out.println("La consola " + this.getMarca() + " " + this.modelo + " fue lanzada en " + this.lanzamiento + " y su tipo de bateria es: " + this.TipoBaterias);
        }
    }

* Herencia (Objeto):

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;


    public class HolaMundo {
        
        public static void main(String args[]){
            // el objeto se crea tal y como el original:
            ConsolaPortatil nsw = new ConsolaPortatil("Nintendo", "Switch", 2017, "Batería Lipo");
            
            // se pueden usar los métodos del hijo:
            nsw.bateria();
            
            // y los del padre:
            System.out.println(nsw.nombre());
            
            // y también vemos como reacciona al usar un método sobrecargado del padre:
            nsw.info();
        }
    }

* Saber a que clase apunta el objeto (instanceof):

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import com.mycompany.videoconsolas.Consola;

    public class HolaMundo {

        public static void main(String[] args) {
            // crear objeto:
            Consola nsw = new Consola("Nintendo", "Switch", 2017);
            
            // averiguar si el objeto es parte de la clase correspondiente:
            if(nsw instanceof Consola){
                System.out.println("nsw es objeto de la clase Consola");
            }
        }
    
    }


Paquetes
########

Crear paquetes
**************

1. Se puede crear un paquete en NetBeans haciendo click derecho en Source Packages y en New.. Java Package.
2. A continuación lo llamamos con el nombre de un dominio pero inverso: **com.mysitio.nombrepaquete** en este caso lo llamaremos: **com.mycompany.videoconsolas**
3. En este paquete podemos crear clases como **Consola** y **ConsolaPortatil**


Importar paquetes
*****************

En cualquier archivo Java podemos importar una clase de un paquete como **videoconsolas**:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;
    // se importa la clase del paquete que queremos usar:
    import com.mycompany.videoconsolas.Consola; // si escribimos com.mycompany.videoconsolas.* va a cargar todos los nombres de clases si existe mas de uno.


    public class HolaMundo {
        
        public static void main(String args[]){
            Consola nsw = new Consola("Nintendo", "Switch", 2017);
            
            nsw.info();
            
        }
    }


Enumeradores o enums 
####################

Los enumeradores se utilizan para listar una serie de elementos constantes como los días de la semana.

Enumerador básico
*****************

Los enumeradores más básicos utilizan atributos como constantes y se suelen utilizar para validar elementos con estructuras switch.
Se crea una nueva clase java y se escribe lo siguiente:

.. code-block:: java
    :linenos:

    package com.mycompany.holamundo;

    // crear el enum:
    public enum Generaciones {
        PRIMERA,
        SEGUNDA,
        TERCERA,
        CUARTA,
        QUINTA,
        SEXTA,
        SEPTIMA,
        OCTAVA,
        NOVENA
    }
    
* Si se imprime alguno de los valores estos mostrarán el nombre de la constante:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            System.out.println(Generaciones.PRIMERA);
        }
        
    }

Enumeradores avanzados 
**********************
Estos enumeradores contienen atributos más complejos como objetos y métodos para manejar dichos atributos:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    // crear el enum:
    public enum Generaciones {
        PRIMERA("Magnavox Oddysey"),
        SEGUNDA("Atari 2600"),
        TERCERA("NES"),
        CUARTA("Sega Megadrive"),
        QUINTA("PlayStation"),
        SEXTA("Sega Dreamcast"),
        SEPTIMA("Nintendo Wii"),
        OCTAVA("Nintendo Switch"),
        NOVENA("PS5");
        
        // se genera un atributo para agregar elementos a cada atributo constante:
        private final String consolas; // este atributo será constante.
        
        // se llama al constructor y se inicializa las consolas:
        private Generaciones(String consolas){
            this.consolas = consolas;
        }
        
        // se carga un método para poder acceder a los elementos de cada objeto constante.
        public String getConsolas(){
            return this.consolas;
        }
    }


* Ejemplos de uso de enumeradores:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    public class HolaMundo {
        
        public static void main(String args[]){
            // Acceder a un elemento de un enumerador:
            System.out.println(Generaciones.QUINTA.getConsolas());
            
            // recorrer los elementos de cada enumerador utilizando el metodo values:
            for(Generaciones g: Generaciones.values()){
                System.out.println(g + " GENERACIÓN: " + g.getConsolas());
            }
        }
        
    }

* Clase abstracta: 

.. code-block:: java 
    :linenos:

    package com.mycompany.videoconsolas;

    // para crear una clase abstracta se añade el manejador abstract:
    public abstract class Sistema { // no se pueden crear objetos de esta clase
        // atributos que heredarán los hijos:
        protected String marca;
        protected String modelo;
        protected int lanzamiento;
        
        // constructor por defecto para heredar:
        protected Sistema(String marca, String modelo, int lanzamiento){
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
        }
        
        // métodos abstractos disponibles (no tendrán nada definido):
        public abstract void info();
    }

* Clase que hereda de clase abstracta:

.. code-block:: java 
    :linenos:

    package com.mycompany.videoconsolas;

    public class Consola extends Sistema{
        
        // se define el constructor:
        public Consola(String marca, String modelo, int lanzamiento){
            // se invoca al constructor abstracto y se le pasan los valores:
            super(marca, modelo, lanzamiento);
            
            System.out.println("Se ha creado el objeto consola, ejemplo de datos:");
            System.out.println("Marca: " + this.marca);
            System.out.println("Modelo: " + this.modelo);
            System.out.println("Lanzamiento: " + this.lanzamiento);
        }
        
        // se añade el contenido del método abstracto:
        public void info(){
            System.out.println("La consola " + this.marca + " " + this.modelo + " fue lanzada en " + this.lanzamiento);
        } 
        
    }


* Objeto que se crea:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import com.mycompany.videoconsolas.Consola;

    public class HolaMundo {

        public static void main(String[] args) {
        Consola nsw = new Consola("Nintendo", "Switch", 2017);
        
        nsw.info();
        }
    
    }


Bloques de código 
#################

Los bloques de códigos son bloques anónimos que se ejecutan antes que cualquier otro elemento en una clase. 
Además los bloques **static anonimos** se ejecutan incluso antes que los bloques anónimos.

.. code-block:: java 
    :linenos:

    package com.mycompany.videoconsolas;

    public class Consola {
        public String marca;
        public String modelo;
        // en un bloque estatico solo pueden cargarse elementos estaticos:
        public static int lanzamiento;
        
        // bloque de inicialización de código:
        {
            marca = "Desconocida";
            modelo = "Desconocido";
        }
        
        // bloque de inicialización de código estatico:
        static{
            // valor inicial de lanzamiento:
            lanzamiento = 1970;
        }
        
        private Consola(){
            System.out.println("Se ha creado el objeto consola, ejemplo de datos:");
            // en el constructor podemos mostrar los atributos inicializados:
            System.out.println("Marca: " + this.marca);
            System.out.println("Modelo: " + this.modelo);
            System.out.println("Lanzamiento: " + this.lanzamiento);
        }
        
        public Consola(String marca, String modelo, int lanzamiento){
            this();
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
            // Probamos ahora con el constructor hijo a ver los datos:
            System.out.println("Datos añadidos al objeto:");
            System.out.println("Marca: " + this.marca);
            System.out.println("Modelo: " + this.modelo);
            System.out.println("Lanzamiento: " + this.lanzamiento);
        }
        
        public void info(){
            System.out.println("La consola " + marca + " " + modelo + " fue lanzada en " + lanzamiento);
        } 

        public String nombre(){
            return marca + " " + modelo;
        }

        public String propietario(String nombre){
            return "La consola " + marca + " " + modelo + " es de " + nombre;
        }
        
    }

Interfaces
##########

Las interfaces son similares a las clases abstractas, se usan para implementar contenido adicional a diferentes clases.
También son muy útiles para hacer herencia múltiple.

* Crear una interfaz en netbeans haciendo clic derecho en Source Packages, luego en new y luego elegimos Java Interface:

.. code-block:: java 
    :linenos:

    package com.mycompany.videoconsolas;

    // la interfaz es similar a la clase:
    public interface Soporte {
        // Los atributos en interfaces deben ser constantes y estáticos:
        public static final String SOPORTE = "ROM";
        
        // Los métodos de una interface son siempre públicos y abstractos:
        public abstract void verSoporte();
    }

* Implementar en clase:

.. code-block:: java 
    :linenos:

    package com.mycompany.videoconsolas;

    // se implementa la interfaz, no importa si la clase es padre o hija:
    public class Consola extends Sistema implements Soporte{
        
        public Consola(String marca, String modelo, int lanzamiento){
            super(marca, modelo, lanzamiento);
            
            System.out.println("Se ha creado el objeto consola, ejemplo de datos:");
            System.out.println("Marca: " + this.marca);
            System.out.println("Modelo: " + this.modelo);
            System.out.println("Lanzamiento: " + this.lanzamiento);
        }
        
        public void info(){
            System.out.println("La consola " + this.marca + " " + this.modelo + " fue lanzada en " + this.lanzamiento);
        } 

        @Override
        public void verSoporte() {
            System.out.println("El formato de los archivos es " + SOPORTE);
        }
        
    }

* Crear objeto:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import com.mycompany.videoconsolas.Consola;

    public class HolaMundo {

        public static void main(String[] args) {
        Consola nsw = new Consola("Nintendo", "Switch", 2017);
        
        nsw.info();
        
        nsw.verSoporte();
        // se pueden usar también las constantes de la interfaz desde el objeto:
        System.out.println(nsw.SOPORTE);
        }
    
    }


Tipos Genéricos
###############

Los tipos genéricos definen el el tipo de dato que tendrán todos sus atributos que se va a utilizar en un objeto de una clase.

* Clase con genéricos:

.. code-block:: java 
    :linenos:

    package com.mycompany.videoconsolas;

    // Se define el comportamiento que recibirá osea que el objeto tendrá un objeto genérico:
    public class Consola<T>{
        // los atributos tendrán el tipo genérico:
        T marca;
        T modelo;
        T lanzamiento;
        
        // el constructor definirá el tipo que va a recibir:
        public Consola(T marca, T modelo, T lanzamiento){
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
            
            System.out.println("Se ha creado el objeto consola, ejemplo de datos:");
            System.out.println("Marca: " + this.marca);
            System.out.println("Modelo: " + this.modelo);
            System.out.println("Lanzamiento: " + this.lanzamiento);
        }
        
        public void info(){
            System.out.println("La consola " + this.marca + " " + this.modelo + " fue lanzada en " + this.lanzamiento);
        } 
        
    }

* Ahora se crea el objeto:

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import com.mycompany.videoconsolas.Consola;

    public class HolaMundo {
        
        public static void main(String[] args) {
        // al crear el objeto se le pasa el tipo string y ya se encargará de hacer casting si es posible a todos:
            Consola<String> nsw = new Consola("Nintendo", "Switch", 2017);
        }
    
    }

.. attention::
    El tipo generico T no acepta tipos primitivos, es decir que solo acepta tipos object como String o Integer (no int)

.. note::
    Se puede ver este tipo de implementación en colecciones tipo **List**, **Set** y **Map** que son de tipo objetos.


Manejo de archivos 
##################

Crear un archivo 
****************

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    // se importa java.io:
    import java.io.*;

    public class HolaMundo {
        
        public static void main(String[] args) {
        // se define la ruta y el nombre del archivo:
        String nombreArchivo = "c:\\prueba\\prueba.txt";
        
        // se crea un nuevo objeto de tipo file:
        File archivo = new File(nombreArchivo);
        // se usa un try catch para evitar errores en la lectura:
        try{
            // se crea un objeto para imprimir el archivo:
                PrintWriter salida = new PrintWriter(archivo);
                // cerramos la salida:
                salida.close();
                
        }catch(FileNotFoundException error){
            error.printStackTrace(System.out);
        }
            
        }
    }

Escribir en un archivo 
**********************

.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import java.io.*;

    public class HolaMundo {
        
        public static void main(String[] args) {
        String nombreArchivo = "c:\\prueba\\prueba.txt";
        
        File archivo = new File(nombreArchivo);
        try{
                PrintWriter salida = new PrintWriter(archivo);
                // escribir en el archivo:
                String contenido = "Esto es contenido de prueba";
                // enviar el contenido a la salida:
                salida.println(contenido);
                salida.println();
                String fin = "Fin de escritura";
                salida.println(fin);
                // para guardar cambios se debe cerrar el archivo:
                salida.close();
                System.out.println("Se ha escrito el contenido con éxito");
                
        }catch(FileNotFoundException error){
            error.printStackTrace(System.out);
        }
            
        }
    }


Leer información de archivo 
***************************
  
.. code-block:: java 
    :linenos:

    package com.mycompany.holamundo;

    import java.io.*;

    public class HolaMundo {
        
        public static void main(String[] args) {
        String nombreArchivo = "c:\\prueba\\prueba.txt";
        
        // el buffer exige un try catch:
        try{
                // se crea un buffer para leer el archivo y dentro se le pasa un lector de archivo:
                BufferedReader entrada = new BufferedReader(new FileReader(nombreArchivo));
                
                // guardar en string el contenido del archivo (requiere controla su escepción:
                String lectura = entrada.readLine();
                // recorrer todas las líneas del archivo hasta que sea el resultado nulo:
                while(lectura != null){
                    // imprimir línea:
                    System.out.println(lectura);
                    // salto de línea:
                    lectura = entrada.readLine();
                }
                // cerrar archivo:
                entrada.close();
        }catch(FileNotFoundException error){
            error.printStackTrace(System.out);
        }catch(IOException error){
            error.printStackTrace(System.out);
        }
            
        }
    }

