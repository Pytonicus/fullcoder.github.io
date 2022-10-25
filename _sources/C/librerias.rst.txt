Librerías C 
===========
 
.. image:: /logos/logo-c.png
    :scale: 50%
    :alt: Logo C
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Librerías comunes de C
  
.. contents:: Índice


string.h 
########
En C para hacer trabajar con Strings tenemos que utilizar la librería ``<string.h>``

Unir dos strings
****************

.. code-block:: c
    :linenos:

    #include <stdio.h>
    #include <string.h>

    void main(void){
        // creamos tres cadenas de caracters y rellenamos las dos primeras:
        char str1[10] = "Primera";
        char str2[10] = "Segunda";
        char str3[20];
        // añadimos a la tercera la primera cadena:
        strcpy(str3, str1);
        // concatenamos un espacio en blanco:
        strcat(str3, " ");
        // y concatenamos la segunda cadena con la tercera.
        strcat(str3, str2);

        printf("%s + %s = %s\n", str1, str2, str3);
    }

comparar dos strings
********************

.. code-block:: c
    :linenos:

    #include <stdio.h>
    #include <string.h>

    void main(void){
        char str1[10] = "hola";
        char str2[10] = "saludo";
        if(strcmp(str1, str2) == 0){ // si da 0 son iguales y si es != distinto no.
            printf("Las dos cadenas son idénticas.\n");
        }else{
            printf("Son cadenas diferentes.\n");
        }
    }

entrada de datos tipo string
****************************

.. code-block:: c
    :linenos:

    #include <stdio.h>

    void main(void){
        int val;
        char string[10] = "250";

        sscanf(string, "%d", &val);
        printf("El valor en el string es %d\n", val);
    }

medir la longitud de un string
******************************

.. code-block:: c
    :linenos: 

    #include <stdio.h>
    #include <string.h>

    void main(void){
        char str1[10] = "Primero";

        printf("La longitud de la cadena %s es %ld\n", str1, strlen(str1));
    }