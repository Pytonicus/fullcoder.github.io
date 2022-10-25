Librería Estandar
=================
 
.. image:: /logos/logo-go.png
    :scale: 30%
    :alt: Logo GO
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M

   
Paquetes más usados en GO
 
.. contents:: Índice
 
Manipulación del Sistema
########################

Averiguar el Sistema operativo (runtime)
****************************************

.. code-block:: GO 
    :linenos:

    package main

    // cargamos la librería runtime:
    import (
        "fmt"
        "runtime"
    )

    func main() {
        // se averigua usando la variable runtime:
        fmt.Println("Sistema operativo: ", runtime.GOOS)
    }


Averiguar la arquitectura
*************************

.. code-block:: GO
    :linenos:

    package main

    // cargamos la librería runtime:
    import (
        "fmt"
        "runtime"
    )

    func main() {
        // se averigua usando la variable runtime:
        fmt.Println("Arquitectura: ", runtime.GOARCH)
    }


Entrada y salida
################

Impresión y recibir datos por consola
*************************************

.. code-block:: GO
    :linenos:

    package main

    import (
        "fmt" // importar fmt
    )

    func main() {
        // imprimir con fmt:
        fmt.Print("Hola persona.")
        // imprimir con fmt y salto de línea:
        fmt.Println("Hola persona y salto de línea.")

        nombre := "Guillermo"
        edad := 34

        // Formatear información al imprimir:
        fmt.Printf("Hola %s, tienes %v años.	\n", nombre, edad) // con s se imprime variable string, con v se imprime algo que no sabemos su formato.

        // Averiguar el tipo de dato de una variable:
        fmt.Printf("%T	\n", edad)

        // recibir un dato:
        fmt.Print("¿Cuál es tu nombre? >>> ")
        fmt.Scanln(&nombre)

        fmt.Println("Te llamas:", nombre)
    }

.. note::
    Al igual que print scan tiene las alternativas Scanln y Scanf que funcionan igual.

Cálculos y números
##################

Números aleatorios (math/rand)
******************************

.. code-block:: GO
    :linenos:

    package main

    // importar la librería rand:
    import (
        "fmt"
        "math/rand"
    )

    func main() {
        // se establece el rango en la variable:
        aleatorio := rand.Int()

        fmt.Println("El número aleatorio es: ", aleatorio)
    }

Manipulación de datos 
#####################

Trabajar con strings (strings)
******************************

.. code-block::
    :linenos:

    package main

    import (
        "fmt"
        "strings" // importar librería strings
    )

    // cargar la librería strings:

    func main() {
        nombre := "Guillermo"

        // conversión a mayúsculas:
        fmt.Println(strings.ToUpper(nombre))

        // conversión a minúsculas:
        fmt.Println(strings.ToLower(nombre))

        // reemplazar 1 o varios caracteres que encuentre:
        nombre = strings.Replace(nombre, "ll", "y", 1)
        fmt.Println(nombre)

        // reemplazar todos los caracteres:
        frase := "Mi-nombre-es-Guillermo"
        frase = strings.ReplaceAll(frase, "-", " ")
        fmt.Println(frase)

        nombres := "Antonio, Luis, Alfredo, Pepa"

        // Convertir a array, se crea una nueva variable para que cambie el tipo de dato a array:
        listado := strings.Split(nombres, ", ")
        fmt.Println(listado)

        // Unir array en una cadena:
        lista_cadena := strings.Join(listado, ", ")
        fmt.Println(lista_cadena)

    }

Trabajar con Números (strconv)
******************************

.. code-block::
    :linenos:

    package main

    import (
        "fmt"
        "strconv" // importar librería strings
    )

    func main() {
        a := "20"
        b := "30"
        // convertir a entero sin variable de error:
        a2, _ := strconv.Atoi(a)

        // convertir con variable de error:
        b2, err := strconv.Atoi(b)
        // en este caso manejamos el error:
        if err != nil {
            fmt.Println(err)
            fmt.Println("No se puede convertir el valor")
        }

        total := a2 + b2

        fmt.Println(total)

        // Otros tipos de conversión (manual de GO):
        booleano, _ := strconv.ParseBool("true")
        float, _ := strconv.ParseFloat("3.1415", 64)
        integer, _ := strconv.ParseInt("-42", 10, 64)
        uinteger, _ := strconv.ParseUint("42", 10, 64)

        fmt.Println(booleano, float, integer, uinteger)

    }
.. note::
    Se puede convertir de entero a cadena usando la función **Itoa()** en lugar de **Atoi()**

Trabajar con errores (errors)
*****************************

.. code-block:: GO 
    :linenos:

    package main

    import (
        "errors" // cargamos librería de errores
        "fmt"
    )

    // la función retornará dos valores, un entero y un error:
    func calcular(num1, num2 int) (int, error) {
        if num1 < num2 {
            // es posible generar errores:
            return 0, errors.New("No se aceptan valores negativos")
        } else {
            // hay que retornar dos cosas, si no ya error retornamos nil:
            return num1 - num2, nil
        }
    }

    func main() {
        // recuperamos el resultado de la función en dos variables:
        total, err := calcular(8, 16)

        if err == nil {
            fmt.Println("Total:", total)
        } else {
            fmt.Println(err)
        }
    }

Manipulación de archivos  
########################

Leer archivo (os)
*****************

.. code-block:: GO 
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "os"
    )

    func main() {
        // abrir un archivo nuevo:
        file, err := os.ReadFile("archivo.txt")

        // comprobar si existen errores:
        if err != nil {
            log.Fatal(err, "no es posible abrir el archivo")
        }

        // imprimir convirtiendo el contenido a string:
        fmt.Println(string(file))
    }


Gestión del Tiempo
##################

Librería (time):

.. code-block:: GO
    :linenos:
 
    package main

    import (
        "fmt"
        "time"
    )

    func main() {
        // recuperar el momento actual:
        inicio := time.Now()

        for i := 0; i < 1000; i++ {
            // mostrar tiempo pasado:
            pasado := time.Since(inicio)
            fmt.Println("Tiempo pasado:", pasado)
        }

    }