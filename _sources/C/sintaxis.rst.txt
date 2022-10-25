Sintaxis C
==========
 
.. image:: /logos/logo-c.png
    :scale: 50%
    :alt: Logo C
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Sintáxis básica de C
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################
    
Instalación
***********

Para poder compilar un programa escrito en C debemos instalar un compilador, yo personalmente utilizo en linux GCC y el comando para instalarlo es: ``sudo apt install build-essential``

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

.. code-block:: c 
    :linenos:

    // acompañamos con un printf esta sentencia que solo lleva el tipo de dato y el enlace a la variable:
    scanf("%d", &edad);

* Salida de datos:

.. code-block:: c 
    :linenos:

    printf("Tu edad es de %d años\n", edad);

Especificación de formato
+++++++++++++++++++++++++

En C existen los especificadores de formato cuya finalidad se da en la entrada o salida de datos para especificar donde va a ir un dato:

+--------------+-----------------------------------------------+
| Tipo de dato | Denominación                                  |
+==============+===============================================+
| %d           | Número Entero (int)                           |
+--------------+-----------------------------------------------+
| %f           | Número con decimales (float, decimal)         |
+--------------+-----------------------------------------------+
| %c           | Caracter o caracteres (char)                  |
+--------------+-----------------------------------------------+
| %s           | Cadenas de texto (string)                     |
+--------------+-----------------------------------------------+


Estructura en c
***************

* Código c puro:

.. code-block:: c
    :linenos:

    // en la primera línea importamos la librería estandar de C:
    #include <stdio.h>
    // creamos la función principal main que no retorna nada (void):
    void main (void){
            printf("Hola mundo!\n"); // con \n hacemos un salto de línea
    }


.. attention::
    Las líneas terminan en ; obligatóriamente.

Extensión
*********

La extensión utilizada por los archivos C es c Una vez se compila su extensión pasa a ser h

Compilación y ejecución
***********************

* El comando para compilar un programa en C con **GCC** es ``gcc -o nombre script.c``
* La compilación nos devolverá un programa llamado hola que ejecutamos en Linux como ``./hola``

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main (void){
        int numero = 27; // enteros
        float decimal = 11.38; // decimales
        double preciso = 3.1415161820; // doble precisión
        char letra[1] = "a"; // carácteres, que es de cantidad fija.
    }

* Constantes:

.. code-block:: c
    :linenos:

    #include <stdio.h>
    // definir constante en el archivo:
    #define PI 3.1415

    void main (void){
        const PI = 3.1415; // constante de función
    }

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main (void){
        sumar = 3 + 6;
        restar = 7 * 9;
        multiplicar = 11 * 6;
        dividir = 13 / 20;
        resto = 54 % 7;
    }

* Incremento y decremento:

.. code-block:: c 
    :linenos:

    i++;
    ++i;
    --i;
    i--;


* Asignar operación:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main (void){
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

Estructuras de control
######################

Condicional if
**************

* if sencillo:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main(void){
        int a = 0;
        if(a == 0){

                printf("a es igual a 0\n");
        }
    }

* if / else:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main(void){
        int a = 0;
        if(a == 0){

                printf("a es igual a 0\n");
        }else{
                printf("a es distinto a 0\n");
        }
    }

* else-if:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main(void){
        int a = 0;

        if(a == 0){
            printf("a es igual a 0\n");
        }else if(a == 1){
            printf("a es igual a 1\n");
        }else{
            printf("a es un numero desconocido\n");
        }
    }

Condicional Switch
******************
Estructura de un switch:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main(void){
        int a = 0;

        switch(a){
            case 0:
                printf("a es igual a 0\n");
                break;
            case 1:
                printf("a es igual a 1\n");
                break;
            default:
                printf("a es desconocido\n");
        }
    }

Bucle for
*********

* for básico:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main(void){
        int a;

        for(a = 0; a < 5; a++){
            printf("a es igual a %d\n", a);
        }
        printf("a es igual a %d y hemos acabado\n", a);
    }

Bucle while
***********

* While sencillo:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main(void){
        int a = 0;

        while(a < 5){
            printf("a es igual a %d\n", a);
            a++;
        }
        printf("a es igual a %d y hemos terminado\n", a);
    }

* do-while:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    void main(void){
        int a = 0;

        do{
            printf("a es igual a %d\n", a);
            a++;
        }while(a == 0);
        printf("a es igual a %d y hemos terminado\n", a);
    }

Detener secuenda de script
**************************

.. code-block:: c
    :linenos:

    #include <stdio.h>

    void main(void){
        int a = 0;

        while(1){
            printf("a es igual a %d\n", a);
            a++;
            if(a == 5){
                break;
            }
        }
        printf("a es igual a %d y hemos acabado/n", a);
    }

Punteros
########
Cuando trabajamos con punteros establecemos un enlace con una variable, de modo que por ejemplo
en el caso de las funciones, al enviar parámetros lo que mandamos es una copia, pero gracias a los punteros
se puede enviar por parámetros la variable original para modificarla.

.. code-block:: C 
    :linenos:

    #include <stdio.h>

    void main(void){
        int a;
        // declarar un puntero:
        int *ptr_a;
        // asignar variable a un puntero:
        ptr_a = &a;

        a = 5;
        printf("El valor de a es %d\n", a);
        // modificar un puntero:
        *ptr_a = 6;

        printf("El valor de a es %d\n", a);

    }

Tipos de datos avanzados
########################

Arrays
******

.. code-block:: c
    :linenos:

    #include <stdio.h>

    void main(void){
        int a[10];
        int count;

        for(count = 0; count <10; count++){
            a[count] = count;
            printf("Repetición número %d\n", a[count]);
        }
    }


Enumeradores
************
Los enumeradores nos sirven para generar un tipo de dato utilizando ``typedef`` y ``enum``, por ejemplo en el ejemplo generamos y usamos un tipo Booleano.

Ejemplo:

.. code-block:: c 
    :linenos:

    #include <stdio.h>
    // creamos el enum y lo llamamos BOOLEAN:
    typedef enum{
        false,
        true,
    } BOOLEAN;

    void main(void){
        // creamos una variable de tipo BOOLEAN
        BOOLEAN b_var;
        // esta variable solo aceptará los valores true o false
        b_var = false;
        if(b_var == true){
            printf("Verdadero\n");
        }else{
            printf("Falso\n");
        }
    }

Estructura de datos
*******************
La estructura de datos se genera también con ``typedef`` junto a ``struct``

.. code-block:: c
    :linenos:

    #include <stdio.h>

    typedef struct{
        int inval1;
        int inval2;
        int outval;
    } MY_DATA;

    void add(MY_DATA *d){
        d->outval = d->inval1 + d->inval2;
    }

    void main(void){
        MY_DATA data;

        data.inval1 = 5;
        data.inval2 = 7;
        add(&data);

        printf("La suma de %d y %d es %d\n", data.inval1, data.inval2, data.outval);
    }

Programación modular
####################

Funciones
*********

* Procedimienos:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    int sum(int a, int b){
        int res;
        res = a + b;
        printf("La suma de 5 y %d es %d\n", y, z);
    }

    void main(void){
        int y = 2;
        sum(5, y);
    }

* funciones:

.. code-block:: c 
    :linenos:

    #include <stdio.h>

    int sum(int a, int b){
        int res;
        res = a + b;
        return res;
    }

    void main(void){
        int y = 2;
        int z = sum(5, y);

        printf("La suma de 5 y %d es %d\n", y, z);
    }

Manejo de Archivos
##################
En C existe la posibilidad de manejar archivos de modo que podemos leer, editar y crear nuevos:

Escritura de archivos
*********************
Para escribir un nuevo archivo desde cero utilizamos el modificador ``wb``:

.. code-block:: c
    :linenos: 

    #include <stdio.h>

    void main(void){
        FILE *fp;
        int value;

        fp = fopen("entrada.txt", "wb");
        if(fp){
            for(value = 48; value < 58; value++){
                fputc(value, fp);
            }
            fclose(fp);
        }
    }

- Añadir un texto formateado con la función ``fprintf()``:

.. code-block:: c
    :linenos:

    #include <stdio.h>

    void main(void){
        FILE *fp;
        int value;

        fp = fopen("entrada.txt", "wb");
        if(fp){
            fprintf(fp, "Esto es un texto.\n");
            fprintf(fp, "Esto es otro texto.\n");
            fclose(fp);
        }
    }

Lectura de archivos
*******************
Si queremos leer un archivo usamos el modificador ``rb``:

.. code-block:: c
    :linenos: 

    #include <stdio.h>

    void main(void){
        FILE *fp;
        int value;

        fp = fopen("entrada.txt", "rb");
        if(fp){
            while(1){
                value = fgetc(fp);
                if(value == EOF) break;
                else printf("%c", value);
            }
            fclose(fp);
        }
    }

Actualización de archivos
*************************
Para actualizar un archivo existente sin destruir la información que ya posee usaremos el modificador ``ab``:

.. code-block:: c
    :linenos: 

    #include <stdio.h>

    void main(void){
        FILE *fp;
        int value;

        fp = fopen("entrada.txt", "ab");
        if(fp){
            fprintf(fp, "Esto es un texto.\n");
            fprintf(fp, "Esto es otro texto.\n");
            fclose(fp);
        }
    }

.. note::
    Si ejecutamos este codigo varias veces veremos como se incluyen nuevas líneas a nuestro script.

Empaquetado y Preprocesamiento
##############################

Crear paquetes
**************
En C podemos dividir el código y llamarlo en la cabecera

1. Tenemos un archivo llamado por ejemplo ``funcion.c`` que contiene una función específica:

.. code-block:: c
    :linenos: 

    int add_valores(int a, int b, int c){
        return a + b + c;
    }

2. Ahora necesitamos un archivo que exporte la función y lo llamamos ``funcion.h``:

.. code-block:: c
    :linenos: 

    extern int add_valores(int a, int b, int c);

3. Y ahora en nuestro archivo principal podemos importar este paquete:

.. code-block:: c
    :linenos:

    #include <stdio.h>
    // llamada del archivo funcion.h:
    #include "function.h"

    void main(void){
        printf("El total es %d\n", add_valores(1,2,3));
    }

.. important::
    Para compilar este programa ejecutamos ``gcc -o miprograma main.c function.c``

El preprocesador
****************
El archivo de intercambio que creamos antes llamado ``funcion.h`` es un archivo de preprocesamiento, podemos saltarnos ese paso y añadir directamente la línea al codigo principal:

.. code-block:: c
    :linenos: 

    #include <stdio.h>
    extern int add_valores(int a, int b, int c);

    void main(void){
        printf("El total es %d\n", add_valores(1,2,3));
    }

.. important::
    Es necesario ejecutar la compilación de ambos al mismo tiempo igualmente 
