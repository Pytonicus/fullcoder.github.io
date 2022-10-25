Sintaxis C
==========
 
.. image:: /logos/logo-cpp.png
    :scale: 20%
    :alt: Logo C++
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Sintáxis básica de C++
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################
    
Instalación
***********

Para poder compilar un programa escrito en C++ debemos instalar un compilador, yo personalmente utilizo en linux GCC y el comando para instalarlo es: ``sudo apt install build-essential``

Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: c
    :linenos:
 
    // Comentario de una sola línea

* Comentarios multilínea:

.. code-block:: c
    :linenos:

    /* Este comentario 
    tiene más de una línea.
    Puede servir para escribir
    un manual u otras cosas.
    */

Entrada y salida estandar
*************************
C utiliza para entrada de datos la función scanf() y para la impresión de estos por consola printf()

* Entrada de datos:

.. code-block:: c++ 
    :linenos:

    cout << "introduce un número: << endl;
    cin >> numero;

* Salida de datos:

.. code-block:: c++ 
    :linenos:

    // salida estandar:
    cout << "Hola amigo" << " así se puede " << " unir cadenas " endl; // endl salto de página o \n.

    // uso de variables:
    cout << "Tu número es " << numero << endl;


Estructura en c
***************

* Código c puro:

.. code-block:: c
    :linenos:

    #include "iostream"

    using namespace std;

    int main(){
        cout << "Hola mundo";

        return 0;
    }

.. attention::
    Las líneas terminan en ; obligatóriamente.

Extensión
*********

La extensión utilizada por los archivos C++ es cpp

Compilación y ejecución
***********************

* El comando para compilar un programa en C++ con **G++** es ``g++ -o hola hola-mundo.cpp``
* La compilación nos devolverá un programa llamado hola que ejecutamos en Linux como ``./hola``

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: c++ 
    :linenos:

    #include <iostream>
    using namespace std;

    int main(){
        // tipo char:
        char x = 'a';

        // tipo entero:
        int entero = 10;

        // tipo flotante:
        float decimal = 3.5;

        // operaciones:
        float resultado = entero + decimal;

        // booleano:
        bool valor = false;

        // impresión de resultado:
        cout << resultado << endl;

        return 0;
    }

* Constantes:

.. code-block:: c++
    :linenos:

    #include <iostream>
    using namespace std;

    // definir constante en la cabezera:
    #define PI 3.1416;

    int main(){
        // o también se declara la constante con const:
        const float PI = 3.1416;

        // imprimir la constante:
        cout << "El valor de PI es: " << PI;

        return 0;
    }

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: c++ 
    :linenos:

    #include <iostream>
    using namespace std;

    int main (){
        sumar = 3 + 6;
        restar = 7 * 9;
        multiplicar = 11 * 6;
        dividir = 13 / 20;
        resto = 54 % 7;
        // impresión con calculo:
        cout << 3 - 2 << endl;
    }

* Incremento y decremento:

.. code-block:: cpp 
    :linenos:

    i++;
    ++i;
    --i;
    i--;


* Asignar operación:

.. code-block:: cpp 
    :linenos:

    #include <iostream>

    int main (){
        // la variable debe tener un valor asignado:
        resultado = 0

        resultado += 12;
        resultado -= 16;
        resultado *= 19;
        resultado /= 6;
        resultado %= 19;
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

.. code-block:: c++ 
    :linenos:

    #include <iostream>
    #include <string>

    using namespace std;


    int main(){
        int resultado = 0;

        cout << "Cuanto es 39+50?" << endl;
        cin >> resultado;

        if(resultado == 39+50){
            cout << "Respuesta Correcta!" << endl;
        }

        return 0;
    }

* if / else:

.. code-block:: c++ 
    :linenos:

    #include <iostream>
    #include <string>

    using namespace std;


    int main(){
        int resultado = 0;

        cout << "Cuanto es 39+50?" << endl;
        cin >> resultado;

        if(resultado == 39+50){
            cout << "Respuesta Correcta!" << endl;
        }else{
            cout << "Respuesta incorrecta, el resultado es: " << 39+50 << endl;
        }

        return 0;
    }

* else-if:

.. code-block:: c++ 
    :linenos:

    #include <iostream>

    using namespace std;


    int main(){
        int edad = 0;

        cout << "¿Qué edad tienes?" << endl;
        cin >> edad;

        if(edad >= 18){
            cout << "Eres mayor de edad!" << endl;
        }else if(edad >=16 && edad < 18){
            cout << "Eres un adolescente " << endl;
        }else{
            cout << "Eres menor de edad" << endl;
        }

        return 0;
    }

Condicional Switch
******************
Estructura de un switch:

.. code-block:: c++ 
    :linenos:

    #include <iostream>

    using namespace std;


    int main(){
        cout << "Elije una opción: ";
        int opcion;
        cin >> opcion;

        switch(opcion){
            case 1:
                cout << "Has seleccionado la primera opción" << endl;
                break;
            case 2:
                cout << "Has seleccionado la segunda opción" << endl;
                break;
            case 3:
                cout << "Has seleccionado la tercera opción" << endl;
                break;
            default:
                cout << "Opción incorrecta" << endl;
        }

        return 0;
    }

Bucle for
*********

* for básico:

.. code-block:: c++ 
    :linenos:

    #include <iostream>

    using namespace std;


    int main(){

        for(int i=10; i > 0; i--){
            cout << "Cuenta atras... "<< i << endl;
        }

        return 0;
    }

* foreach:

.. code-block:: c++
    :linenos:

    #include <iostream>
    using namespace std;

    int main()
    {
        int numeros[] = { 8, 154, 32, 25 };

        for (int num : numeros){
            cout << num << endl;
        }

    }

Bucle while
***********

* While sencillo:

.. code-block:: c++ 
    :linenos:

    #include <iostream>

    using namespace std;


    int main(){

        int numero;
        cout << "Introduce un número" << endl;
        cin >> numero;
        while(numero <= 100){
            cout << "Introduce un número" << endl;
            cin >> numero;
        }

        return 0;
    }

* Bucle infinito:

.. code-block:: c++
    :linenos:

    #include <iostream>

    using namespace std;


    int main(){

        int numero;
        numero = 0;
        while(1){
            numero++;
            cout << numero << endl;
        }

        return 0;
    }

* do-while:

.. code-block:: c++ 
    :linenos:

    #include <iostream>

    using namespace std;


    int main(){

        int numero;
        cout << "Introduce un número" << endl;
        cin >> numero;
        do{
            cout << "Introduce un número" << endl;
            cin >> numero;
        }while(numero <= 100);

        return 0;
    }

Detener secuenda de script
**************************

.. code-block:: c
    :linenos:

    #include <iostream>

    using namespace std;


    int main(){

        int numero;
        numero = 0;
        while(1){
            numero++;
            cout << numero << endl;

            if(numero == 100){
                break;
            }
        }

        return 0;
    }

Punteros
########
Cuando trabajamos con punteros establecemos un enlace con una variable, de modo que por ejemplo
en el caso de las funciones, al enviar parámetros lo que mandamos es una copia, pero gracias a los punteros
se puede enviar por parámetros la variable original para modificarla.

.. code-block:: C++ 
    :linenos:

    #include <stdio.h>

    #include <iostream>

    using namespace std;

    int funcion(int valor){
        valor = valor + 10;
        return valor;
    }

    int funcionPunteros(int* valor){
        *valor = *valor + 10;
        return *valor;
    }

    int main(){
        int numero = 10;

        cout << "Antes de función " << numero << endl;
        funcion(numero);
        cout << "Después de funcion " << numero << endl;

        cout << "Antes de funcionPunteros " << numero << endl;
        funcionPunteros(&numero);
        cout << "Después de funcionPunteros " << numero << endl;

        return 0;
    }

Tipos de datos avanzados
########################

Arrays o vectores
*****************

.. code-block:: c++
    :linenos:

    #include <iostream>

    using namespace std;


    int main(){
        // declaración y asignación de elementos al array:
        int edades[] = {1,2,9,10,16,32,33,22,15};

        // estableciendo el tamaño de la cadena, algo similar a la función length en otros lenguajes:
        int limite = (sizeof(edades)/sizeof(edades[0]));

        // Recorrido e impresión del array:
        for(int i = 0; i < limite; i++){
            cout << edades[i] << endl;
        }

        // cambiando el valor de un elemento de la cadena:
        edades[2] = 27;
        // impresión de un valor específico del array:
        cout << edades[2] << endl;

        return 0;
    }

Matrices
********

Las matrices son básicamente arrays multidimensionales a los que les asignamos una cantidad de casillas y este se puede representar como una tabla a la hora de guardar y acceder a la información:

.. code-block:: c++
    :linenos:

    # include "iostream"

    using namespace std;

    int main(){
        // creamos una matriz de 4x4
        int matriz[4][4] = {
            {1,2,3,4},
            {4,5,6,7},
            {8,9,10,11},
            {12,13,14,15}
        }; // el primer array representa las filas y el segundo las columnas

        // impresión del número 11:
        cout << matriz[2][3] << endl;

        // recorrer matriz con un bucle anidado:
        for(int fila = 0; fila <= 3; fila++){
            cout << "==============" << endl;
            cout << "|";
            for(int columna = 0; columna <= 3; columna++){
                cout << matriz[fila][columna] << "|";
            }
            cout << endl;
        }
    }

Enumeradores
************
Los enumeradores nos sirven para generar un tipo de dato utilizando ``typedef`` y ``enum``, por ejemplo en el ejemplo generamos y usamos un tipo Booleano.

Ejemplo:

.. code-block:: c++ 
    :linenos:

    # include "iostream"
    using namespace std;


    // definir un enum:
    enum Consola {
        Mandos,
        Aparato,
        Soporte
    };

    int main(){
        // definir una variable:
        Consola VideoConsola;
        // asignar un valor disponible (esto establecerá una posición 1 de 0,1 y 2 que hay disponibles):
        VideoConsola = Aparato;

        // se podrá validar con switch los distintos casos:
        switch(VideoConsola){
            case Mandos:
                cout << "La Nintendo 64 tiene 4 puertos de mandos" << endl;
                break;
            case Aparato:
                cout << "La Nintendo 64 es una consola de 64 bits" << endl;
                break;
            case Soporte:
                cout << "La nintendo 64 funciona con cartuchos de juego" << endl;
                break;
        }
        // Al imprimir este valor del enum nos devolverá un número (de ahí su nombre enum-erador)
        cout << VideoConsola << endl;

    }

Estructura de datos
*******************
La estructura de datos se genera también con ``typedef`` junto a ``struct``

.. code-block:: c
    :linenos:

    #include <stdio.h>

    # include "iostream"
    using namespace std;


    // definir una estructura:
    struct CONSOLA {
        // declarar los tipos de datos presentes:
        string marca;
        string modelo;
        int lanzamiento;
    } videoconsola;

    int main(){
        // cargar la estrucutra en una variable:
        struct CONSOLA playstation;
        // asignar valores:
        playstation.marca = "Sony";
        playstation.modelo = "PlayStation";
        playstation.lanzamiento = 1994;

        cout << "La consola " << playstation.marca << " " << playstation.modelo << " fue lanzada en " << playstation.lanzamiento << endl;
    }

Programación modular
####################

Funciones
*********

.. code-block:: cpp
    :linenos:

    #include <iostream>
    #include <string>

    using namespace std;

    int funcion(int num1, int num2){
        return num1 + num2;
    }

    int main(){
        cout << "el total es: " << funcion(10, 15) << endl;

        return 0;
    }

Programación Orientada a objetos
################################

Clases
******

El gran avance de C++ frente a C tradicional es la inclusión del paradigma orientado a objetos.

* Creación de clases con atributos, metodo y creación del objeto:

.. code-block:: cpp
    :linenos:

    #include <iostream>
    using namespace std;

    // creamos la clase:
    class MiClase {
        public: // definimos el tipo de encapsulación si es publica o privada
            // definimos los atributos
            int numero; 
            string cadena; 
            // y esto es un método de ejemplo:
            void miMetodo(){
                cout << "Metodo de prueba" << endl;
            }
            // metodo que recibe parámetros:
            void conParametros(int edad){
                cout << "Tienes " << edad << " años." << endl;
            }
    }; // las clases se cierran con ;

    int main(){
        // creamos un objeto a partir de la clase anterior:
        MiClase miObjeto;

        // podemos acceder directamente a sus atributos
        miObjeto.numero = 20;
        miObjeto.cadena = "Texto de prueba";

        // imprimimos los valores:
        cout << miObjeto.numero << endl;
        cout << miObjeto.cadena << endl;
        // llamar a un método:
        miObjeto.miMetodo();
        // llamar a un metodo y enviar un parámetro:
        miObjeto.conParametros(33);

        return 0;
    }

Clases con constructor
**********************

.. code-block:: cpp
    :linenos:

    #include <iostream>
    using namespace std;

    class MiClase {
        public:
            string nombre;
            int edad;
            
            // el constructor lleva el nombre de la clase y puede recibir parametros:
            MiClase(string n, int e){
                nombre = n;
                edad = e;

                cout << "Objeto creado con éxito" << endl;
            }

            void presentacion(){
                cout << "Te llamas " << nombre << " y tienes " << edad << " años." << endl;
            }
    };

    int main(){
        MiClase miObjeto("Felipe", 37);

        miObjeto.presentacion();
        return 0;
    }

Tipos de encapsulación en C++
*****************************
Existen tres tipos de encapsulación en C++:

* public: los atributos y métodos son publicos y por tanto se puede acceder a ellos una vez creado el objeto.
* private: los atributos y metodos no pueden ser llamados o modificados desde el objeto.
* protected: los atributos y metodos solo pueden ser llamados o modificados desde la clase.

Get y Set 
*********
Para manejar atributos y metodos privados utilizaremos los get y set, estos metodos son una convención en programación:

.. code-block:: cpp
    :linenos:

    #include <iostream>
    using namespace std;

    class MiClase {
        // cada atributo o metodo lo manejaremos en su propia capa de encapsulación.
        private:
            int numA;
        public:
            // Con los setter modificamos el atributo:
            void setNumero(int n){
                numA = n;
            }

            // y con los getter recuperamos el atributo, debemos poner el tipo de devolución como en las funciones:
            int getNumero(){
                return numA;
            }
    };

    int main(){
        MiClase numeros;

        numeros.setNumero(27);
        cout << "El numero establecido es: " << numeros.getNumero() << endl;
    }

Herencia
********
La herencia en C++ se realizaría del siguiente modo:

.. code-block:: cpp
    :linenos: 

    #include <iostream>
    using namespace std;

    // clase padre:
    class Mueble {
        public:
            string mueble = "Mesa";
            void accion(){
                cout << "PONER LA MESA" << endl;
                cout << "=============" << endl;
            }
    };

    // clase hijo que hereda del padre:
    class MesaComedor: public Mueble {
        public:
            string tipo = "Mesa del comedor";
    };

    int main(){
        MesaComedor mesa;

        mesa.accion();
        cout << "Hay que poner la " << mesa.mueble << endl;
        cout << "¿Qué mesa?" << endl;
        cout << "La " << mesa.tipo << endl;
    }

.. important::
    En la herencia de clases existe otro concepto llamado polimorfismo y se basa en reutilizar los metodos de las clases padre para modificarlos en las clases hijo de forma que
    podemos reutilizarlos sin necesidad de crear unos nuevos.

Manejo de errores
#################
El manejo de errores en C++ se realiza con **try** y **catch**:
 
.. code-block:: cpp
    :linenos: 

    #include <iostream>
    using namespace std;

    int main(){
        int numeroA;
        int numeroB = 20;
        int total;

        cout << "introduce un número:" << endl;
        cin >> numeroA;
        total = numeroA + numeroB;

        // con try probaremos a ejecutar una operación:
        try{
            // si el valor es mayor a 20 siginfica que el numeroA no es una letra o un valor igual menor que 0:
            if(total > 20){
                cout << "El resultado de la suma es: " << total << endl; 
            }else{
                // sino provocaremos un error:
                throw(numeroA);
            }
        } // catch caputará el error provocado:
        catch(int numero){
            cout << "El valor introducido no es correcto: " << numero << endl;
        }
    }

Empaquetado y Preprocesamiento
##############################
He estado buscando información en la red y no he dado con mucho así que he comprobado que se puede crear paquetes del mismo modo que C.

* Archivo ``modulo.cpp`` con la función del paquete:

.. code-block:: cpp
    :linenos: 

    int sumar(int num1, int num2){
        return num1 + num2;
    }

* Archivo de intercambio ``intercambio.h``:

.. code-block:: cpp
    :linenos: 

    extern int sumar(int a, int b);

* Archivo ``main.cpp`` con el código principal:

.. code-block:: cpp
    :linenos: 

    #include "iostream"
    #include "intercambio.h"

    using namespace std;

    int main(){
        cout << sumar(20,15) << endl;
    }

Uso del preprocesador
*********************
Este ejemplo de preprocesado sin utilizar el archivo .h es identico al de C.

* Archivo ``modulo.cpp`` con la función del paquete:

.. code-block:: cpp
    :linenos: 

    int sumar(int num1, int num2){
        return num1 + num2;
    }

* Archivo ``main.cpp`` con el código principal:

.. code-block:: cpp
    :linenos: 

    #include "iostream"
    extern int sumar(int a, int b);

    using namespace std;

    int main(){
        cout << sumar(20,15) << endl;
    }