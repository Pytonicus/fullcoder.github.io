=================
Programación Bash
=================

.. image:: /logos/programacion-bash-logo.png
    :scale: 20%
    :alt: Logo Programación Bash 
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Última edición el día |date| a las |time|. 

Esta es la documentación que he recopilado para programar en bash.
 
.. contents:: Índice
 
Elementos básicos del lenguaje 
##############################

En linux existen varios tipos de Shells:

- Bourne shell (sh)
- C shell (csh)
- Korn shell (ksh)
- TC Shell (tcsh)
- Bourne Again Shell (bash)

La mas popular es bash y es la que usaremos para estos comandos.

Crear un script
***************

- Creamos un archivo nuevo ``nano prueba-bash.sh`` y añadimos lo siguiente:

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    echo "Prueba de bash ejecutada"

- Añadimos permisos de ejecución al archivo: ``chmod +x prueba-bash.sh``.
- Ejecutamos el script: ``./prueba-bash.sh``

.. attention::
    La primera línea es obligatoria e indica el tipo de shell va a interpretar el script.

.. note::
    Los scripts bash aceptan comandos linux.

Entrada y salida
****************

- La salida de datos la ejecutamos con ``echo`` y para la entrada hacemos lo siguiente:

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    # añadiendo el parámetro n podemos recibir un dato:
    echo -n "Escribe tu nombre: "
    # dicho dato lo guardamos en una variable con read:
    read nombre
    # Ya podemos utilizar el dato recibido:
    echo "Te llamas $nombre"

    # alternativamente podemos usar el read directamente para recibir el parámetro con p:
    read -p "Escribe tus apellidos: " apellidos

    echo "$nombre $apellidos"

.. note::
    podemos limitar el número de caracteres de entrada añadiendo un número al parametro **-n** ej: ``echo -n8 "Introduce una contraseña de 8 caracteres máximos: "``

.. note:: 
    añadiendo al echo el parametro **-t5** u otro número tardará dicho tiempo en cerrar el programa si no se introduce un valor.

.. note::
    si usamos en read el parámetro **-s** ej: ``read -s password`` podemos escribir sin que se muestre la información en el prompt.

Pausar ejecución por tiempo 
***************************

- Se puede añadir una pausa con **sleep** añadiendo un valor numérico que serán los segundos que debe pausarse.

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    echo "creando materia oscura..."
    sleep 1
    echo "preparando atomos de carga..."
    sleep 1
    echo "cargando mundo..."
    sleep 2
    echo "LISTO PARA DESPEGAR!"

Ejecución de comandos 
*********************

Variables y tipos de datos 
##########################

Variables
*********

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    # Esto es un comentario

    # Declarar una variable:
    nombre="Guillermo"

    # Imprimir variables, para usar variables hay que añadir $ al principio:
    echo "Me llamo $nombre" # la concatenación es automática

.. attention::
    El casting de variables no es un problema, ya que las variables son mutables. Por buena practica es importante que cuando se asigne un tipo de dato a una variable no se cambie.

.. note::
    La concatenación con comillas dobles permite añadir las variables en cualquier de la cadena de texto.


Variables de entorno 
********************

Las variables de entorno se establecen en el sistema y para utilizarlas se usa el comando ``env``.

Las variables de entornos mas destacadas son:

- ``echo $HOME``: Muestra la ruta del directorio home del usuario.
- ``echo $PATH``: Muestra una lista de directorios separados por : .
- ``echo $LOGNAME``: Muestra el usuario logeado.
- ``echo $HOSTNAME``: Muestra el nombre del equipo.
- ``echo $MACHTYPE``: Tipo de sistema que estamos utilizando.
- ``echo $UID``: Muestra el id del usuario activo.

Las variables de entorno se definen en **/etc/profile**, **/etc/profile.d** y **~/.bash_profile**.

Operadores 
##########

Operadores aritméticos 
**********************

.. code-block:: bash 
    :linenos:
                                                                                                    prueba.sh                                                                                                                
    #!/bin/bash

    # PARA OPERACIONES ARITMÉTICAS USAMOS LA ASIGNACIÓN DE VARIABLE CON LET
    let suma=5+5
    echo "Suma: $suma"

    let resta=10-2
    echo "Resta: $resta"

    let multiplicacion=2*8
    echo "Multiplicación: $multiplicacion"

    let division=10/2
    echo "División: $division"

    let potencia=2**3
    echo "Potencia: $potencia"

    let modulo=17%2
    echo "Módulo o resíduo: $modulo"

.. attention::
    Recuerda que la asignación de datos en BASH no debe tener espacios entre el símbolo =

Operadores relacionales
***********************

Validación entre dos números.

- ``-eq`` : Igual que.
- ``-ge`` : Mayor o igual que. 
- ``-le`` : Menor o igual que.
- ``-ne`` : Diferente que.
- ``-gt`` : Mayoer que. 
- ``-lt`` : Menor que.

Operadores lógicos 
******************

Expresiones de operaciones lógicas.

- ``=`` : Igual que.
- ``!=`` : Diferente que.
- ``-n`` : Valida si la cadena es superior a 0.
- ``-z`` : Valida si la cadena es igual a 0.

Comparacion de archivos 
***********************

Expresiones para comparar archivos.

Cuando recuperamos un path mediante una cadena:

- ``-d``: Comprueba si es un directorio.
- ``-f``: Comprueba si es un archivo. 
- ``-s``: Comprueba si es un link simbólico.
- ``-e``: Comprueba si el fichero existe.
- ``-s``: Comprueba si tiene un tamaño mayor a 0.
- ``-r``: Comprueba si tiene permiso de lectura.
- ``-w``: Comprueba si tiene permiso de escritura.
- ``-x``: Comprueba si tiene permiso de ejecución.

Estructuras de control
######################

Condicional if 
**************

- If sencillo:

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    echo -s "Contraseña: "
    read clave

    if [ "$clave"="contraseña" ];
    then
            echo "Correcto"
    fi


- If/else:

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    echo -n "Introduce tu edad: "
    read edad

    if [ "$edad" -ge 18 ];
    then
            echo "Tienes $edad años, eres mayor de edad."
    else
            echo "Con $edad, eres menor de edad."
    fi

- Else-if:

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    echo -n "Introduce tu edad: "
    read edad

    if [ "$edad" -ge 65 ];
    then
            echo "Con $edad ya eres un ancian@."
    elif [ "$edad" -ge 18 ];
    then
            echo "Tienes $edad años, eres mayor de edad."
    else
            echo "Con $edad, eres menor de edad."
    fi

- Comprobar archivos:

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    echo -n "Introduce una ruta: "
    read path

    # validando si es directorio, archivo o enlace simbólico:
    if [ -d $path ]; then
            echo "$path es un directorio"
            file="directorio"
    elif [ -f $path ]; then
            echo "$path es un archivo"
            file="archivo"
    else
            echo "$path no existe"
    fi

    # validando que permisos tiene:
    if [ -r $path ]; then 
            echo "  - el $file tiene permisos de lectura"
    fi

    if [ -w $path ]; then
            echo "  - el $file tiene permisos de escritura"
    fi

    if [ -x $path ]; then
            echo "  - el $file tiene permisos de ejecución"
    fi


Bucle for básico 
****************

.. code-block:: bash 
    :linenos:

    #!/bin/bash

    # hacemos el bucle con unos números por defecto:
    for num in {1..10}
    do
            echo $num
    done


Bucle While
***********

.. code-block:: bash 
    :linenos:
                   
    #!/bin/bash

    echo -n "Introduce la contraseña: "
    read password

    while [ $password != "bash"  ]; do
            echo -n "Contraseña erronea, vuelve a intentarlo: "
            read password
    done

    echo "Bienvenid@ al sistema"


Until
*****

- Funciona exactamente igual que **while** salvo porque se ejecuta hasta que la condición sea false:

.. code-block:: bash 
    :linenos:
                   
    #!/bin/bash

    echo -n "Introduce la contraseña: "
    read password

    until [ $password = "bash"  ]; do
            echo -n "Contraseña erronea, vuelve a intentarlo: "
            read password
    done

    echo "Bienvenid@ al sistema"

Tipos de datos avanzados
########################

Arrays
******

.. code-block:: bash 
    :linenos:
                                            
    #!/bin/bash

    # Asignación individual de valores:
    consolas[0]="Nintendo Gamecube"
    consolas[1]="Sony Playstation"
    consolas[2]="Sega Megadrive"
    consolas[3]="Nintendo Switch"

    # Asignación conjunta:
    videojuegos=("The last of Us" "Sonic the Hedgehog" "Crash Bandicoot")

    # recorrer elementos por índice:
    for c in {0..3}
    do
            echo ${consolas[$c]}
    done

    # podemos contar todos los valores que tiene un array usando # y luego *:
    echo "Hay ${#videojuegos[*]} videojuegos:"

    # BUCLE TIPO C:
    # guardamos la cantidad de valores:
    let total_juegos=${#videojuegos[*]}

    # Creamos un bucle for tipo c:
    for(( i=0; $i<$total_juegos; i=$i+1))
    do
            echo "  - ${videojuegos[$i]}"
            # vamos a hacer una pausa de 1 segundo:
            sleep 1
    done

.. important::
    Los arrays en Bash tienen un máximo de 1024 elementos.

Programación modular 
####################

Funciones
*********

.. code-block:: bash 
    :linenos:
                   
    #!/bin/bash

    # crear una función:
    function saludar() {
            echo "Hola $nombre"
            # return (para retornar valores)
    }

    # utilizar función saludar:
    echo -n "Introduce tu nombre: "
    read nombre

    saludar $nombre

Importar y exportar 
###################

Exportar variables 
******************

Se puede exportar una variable cuando sea necesario utilizar fuera de su ámbito, por ejemplo en otro interpretre dentro del archivo:

.. code-block:: bash 
    :linenos:
               
    #!/bin/bash

    # variables normales y exportadas:
    var_basica="Variable normal"
    export var_exportada="Variable exportada"

    # si ejecutamos un nuevo interpretre y llamamos a ambas solo mostrará el resultado de la exportada:
    bash -c '
    echo "valor de var_basica: $var_basica"
    echo "valor de var_exportada: $var_exportada"
'

