Sintaxis GO
===========

.. image:: /logos/logo-go.png
    :scale: 30%
    :alt: Logo GO
    :align: center

.. |date| date::
.. |time| date:: %H:%M

    
Sintáxis básica de GO
   
.. contents:: Índice
 
Elementos básicos del lenguaje 
##############################

Instalación
***********
* Instalación: ``sudo apt install golang``
* Extensión de archivos: **.go**

Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: GO
    :linenos:
 
    // Esto es un comentario de una línea

* Comentarios multilínea:

.. code-block:: GO
    :linenos:

    /*
    Comentarios de 
    tipo multilínea 
    */

Entrada y salida estandar
*************************
Datos de entrada y salida a través de la consola y/o el navegador.

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        // declarar valor entrada:
        var edad int

        // salida estandar:
        fmt.Print("¿Qué edad tienes?: ")
        
        // entrada estandar:
        fmt.Scan(&edad)

        // impresión con salto de línea:
        fmt.Println("Tienes", edad, "años")

        // Introducir múltiples valores:
        var nombre, apellidoUno, apellidoDos string

        fmt.Print("¿Cómo te llamas?: ")
        fmt.Scanf("%v %v %v", &nombre, &apellidoUno, &apellidoDos)

        fmt.Printf("Te llamas %v %v %v", nombre, apellidoUno, apellidoDos)
    }

Estructura en GO
*****************

* Código GO puro:

.. code-block:: GO
    :linenos:

    package main

    import "fmt"

    // Función principal:
    func main(){
        // imprimir un saludo:
        fmt.Println("Hola a full!")
    }

Concatenación
*************
Concatenación de variables y cadenas se realiza con **+**

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        nombre := "Guillermo"

        // concatenar:
        fmt.Println("Me llamo " + nombre)

        // se puede ir agregando variables y dejará espacios:
	    fmt.Println("Hola", "amigo mío, tienes", 33, "años")

        // impresión usando verbos:
        nombre := "Guillermo"
        apellidos := "Granados Gómez"
        edad := 33

        // cada %v devolverá el valor de una variable según el orden:
        fmt.Printf("Te llamas %v %v y tienes %v años", nombre, apellidos, edad)
    }

GO-CLI - Comandos de GO
***********************

Comandos de GO:

* go version: versión de go instalada.
* go build: se ejecuta en la raiz del proyecto para generar un ejecutable.
* go build archivo.go: genera un ejecutable de un script.
* GOOS=windows GOARCH=386 go build archivo.go: genera un ejecutable para otro sistema.
* go run archivo.go: ejecuta un script de go.
* godoc: Abre un servidor web en la dirección http://localhost:6000
* go get: permite descargar bibliotecas y utilidades de terceros.
* go mod: permite gestionar los proyectos locales. ``go mod init nombre_proyecto``

.. attention::
    Para poder importar paquetes externos con **go get** antes hay que ejecutar el comando **go mod init nombre_proyecto**
 
Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        // declaración, que se puede hacer así o de una vez:
        var otroTexto string
        otroTexto = "Soy otra cadena"
        var numero int = -15
        var numeroSinSimbolo uint = 15
        var decimal float32 = 2.35
        var decimalLargo float64 = 32.23423423
        var booleano bool = true

        // declaración múltiple: 
        var (
            nombre    = "Guillermo"
            apellidos = "Granados Gómez"
            edad      = 34
        )

        fmt.Println("Soy", nombre, apellidos, "y tengo", edad, "años.")

        // declaracion con operador de inicialización:
        texto := "Cadena de texto \n - separada por una línea"

        fmt.Println(otroTexto)
    }

.. attention::
    Las variables declaradas deben usarse o dará error a la hora de compilar. Se recomienda también declarar en la medida de lo posible usando el operador :=

* Constantes:

.. code-block:: GO
    :linenos:

    package main

    import "fmt"

    func main(){
        // definición de constante:
        const PI = 3.1416
        fmt.Println(PI)

        // definir múltiples constantes:
        const (
            nombre = "Guillermo"
            apellidos = "Granados Gómez"
            edad = 33
        )
        fmt.Print(edad)
    }

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        suma := 2 + 2
        resta := 2 - 2
        multiplicacion := 2 * 2
        division := 2 / 2
        resto := 2 % 2
    }

* Incremento y decremento:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        numero := 5

        // incremento y decremento:
        numero++
        ++numero
        numero--
        --numero
    }

* Asignar operación:

.. code-block:: GO 
    :linenos:

        package main

    import "fmt"

    func main(){
        numero := 5

        numero += 10
        numero -= 11
        numero *= 2
        numero /= 7
        numero %= 2
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

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        var edad int

        fmt.Print("¿Qué edad tienes? \n>>> ")
        fmt.Scanln(&edad)

        if edad >= 18 {
            fmt.Println("Eres mayor de edad")
        }
    }


* if / else:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        var edad int

        fmt.Print("¿Qué edad tienes? \n>>> ")
        fmt.Scanln(&edad)

        if edad >= 18 {
            fmt.Println("Eres mayor de edad")
        } else {
            fmt.Println("Todavía eres menor de edad")
        }
    }


* else-if:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        var edad int

        fmt.Print("¿Qué edad tienes? \n>>> ")
        fmt.Scanln(&edad)

        if edad >= 65 {
            fmt.Println("Eres un anciano")
        } else if edad >= 18 {
            fmt.Println("Eres mayor de edad")
        } else {
            fmt.Println("Todavía eres menor de edad")
        }
    }

* if declaración corta:

.. code-block:: GO
    :linenos:

    package main

    import "fmt"

    // crear una función para recibir parámetros:
    func calcula_edad(e int) string {
        // asignar una variable al scope de un if:
        if edad := e; edad >= 18 {
            return "Eres mayor de edad"
        } else {
            return "Eres menor de edad"
        }
    }

    func main() {
        var mi_edad int

        fmt.Println("¿Qué edad Tienes?")
        fmt.Print(">>> ")
        fmt.Scanln(&mi_edad)
        fmt.Println(calcula_edad(mi_edad))
    }


Condicional Switch
******************
Estructura de un switch:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        var operacion string

        fmt.Print("¿Qué quieres saber? \n>>> ")
        fmt.Scanln(&operacion)

        switch operacion {
        case "nombre":
            fmt.Println("Me llamo Guillermo")
        case "apellidos":
            fmt.Println("Mis apellidos son Granados Gómez")
        case "edad":
            fmt.Println("Tengo 33 años")
        default:
            fmt.Println("No reconozco el comando...")
        }
    }

.. attention::
    Se pueden validar más de un valor en case añadiéndolos con comas: **case 'a','e','i','o','u'**

.. Note::
    Los Switch en GO permiten validar condiciones como a > 10 de un modo similar a if.

Bucle for
*********

* for básico:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {

        for i := 0; i <= 10; i++ {
            fmt.Println("Repetición nº", i)
        }
    }

* foreach:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        // existe un slice:
        consolas := []string{"Megadrive", "Playstation", "Gameboy"}

        // y lo podemos recorrer con un for y range:
        for i, v := range consolas {
            fmt.Println(i, v)
        }

        // si no queremos usar el índice:
        for _, v := range consolas {
            fmt.Println(v)
        }
    }

Bucle while
***********
Según la guía de Go el bucle For es el bucle While de go:


.. code-block:: GO 
:linenos:

    package main

    import "fmt"

    func main() {
        var repetir string

        repeticion := 0

        for {
            repeticion++

            fmt.Println("Repetición nº", repeticion)

            fmt.Print("¿Repetir otra vez? (s/n): ")
            fmt.Scan(&repetir)

            if repetir == "n" {
                break
            }
        }
    }

Punteros
########
Cuando trabajamos con punteros establecemos un enlace con una variable, de modo que por ejemplo
en el caso de las funciones, al enviar parámetros lo que mandamos es una copia, pero gracias a los punteros
se puede enviar por parámetros la variable original para modificarla.

.. code-block:: GO 
    :linenos:

    package main

    import (
        "fmt"
    )

    // La función recibe un puntero tipo string:
    func cambiar(nombre *string) {
        *nombre = "Adolfo"
    }

    func main() {
        // se crea una variable con un nombre:
        nombre := "Pedro"
        fmt.Println(nombre)

        // se envía el puntero de la variable original para modificar:
        cambiar(&nombre)

        // al imprimir de nuevo la variable original vemos que el nombre cambió:
        fmt.Println(nombre)

        // podemos ver la referencia de la memoria donde se asignó el puntero:
        fmt.Println(&nombre)
    }

Defer
*****
Defer ejecutará la función seleccionada como la última. Esta sentencia se usa normalmente para cerrar archivos.

- Ejemplo con funciones:

.. code-block:: GO 
    :linenos:

    package main

    import (
        "fmt"
    )

    // funciones a cargar:
    func funcion1() {
        fmt.Println("Hola desde función 1")
    }

    func funcion2() {
        fmt.Println("Hola desde función 2")
    }

    func funcion3() {
        fmt.Println("Hola desde función 3")
    }

    func funcion4() {
        fmt.Println("Hola desde función 4")
    }

    func main() {
        // ahora se ejecutarán las funciones con los mensajes:
        funcion1()
        defer funcion2()
        funcion3()
        funcion4()
    }


Tipos de datos avanzados
########################

Arrays
******

- Declaración tradicional:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        // dclaración de array con tipo definido:
        var array [5]int
        array[2] = 7
        fmt.Println(array[2])

        // asignar valores al array:

        // asignación directa:
        array2 := [3]string{"Paco", "Pepe", "Adolfo"}
        fmt.Println(array2[2])

        // Asignación directa sin establecer longitud:
        array3 := [...]string{"Galletas", "Fresas", "Aceite", "Tomates"}
        fmt.Println(array3[2])

        // recuperar una parte del array:
        fmt.Println(array3[:2])
    }


- Array multidimensional:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        // declarar array multidimensional:
        var arrayMulti [4][4]int

        // asignar un valor a una posición:
        arrayMulti[2][1] = 11

        // utilizar el valor asignado:
        fmt.Println(arrayMulti[2][1])
    }

.. note::
    Como en otros lenguajes de programación clásicos los arrays son de un tamaño 
    definido previamente en su declaración. Para trabajar con tamaños dinámicos existen los Slices

Slices
******

- Declaración tradicional:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        // declaración y asignación directa:
        personas := []string{"Paco", "Pepe", "Adolfo"}
        fmt.Println(personas[2])

        // declarar y asignar una parte de otro slice:
        var dos []string = personas[:2]

        fmt.Println(dos)
    }


- Slice multidimensional:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        // declaración y asignación directa:
        agenda := [][]string{
            []string{"Paco", "22", "Futbolista"},
            []string{"Pedro", "34", "Barrendero"},
        }

        fmt.Println(agenda[0][0], "es un", agenda[0][2], "y tiene", agenda[0][1], "años")
    }

Mapas
*****
Los mapas son colecciones de datos de la misma forma que un diccionario en Python o un objeto literal en JavaScript.

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // se crea un struct:
    type Consola struct {
        marca, modelo string
        lanzamiento   int
    }

    func main() {
        // ahora se crea el mapa y se utiliza el struct de base:
        var consolas = map[int]Consola{
            0: Consola{marca: "Sega", modelo: "Saturn", lanzamiento: 1994},
            1: Consola{marca: "Sony", modelo: "PlayStation", lanzamiento: 1994},
        }

        // añadir un nuevo valor con su clave definida:
        consolas[2] = Consola{marca: "Nintendo", modelo: "64", lanzamiento: 1996}

        fmt.Println(consolas)
    }

.. important::
    Para crear un mapa vacío lo más común es utilizar la función **make()**

Control de errores
##################

El control de errores en GO no funciona del mismo modo que en otros lenguajes de programación. En el caso de GO cuando se realizan ciertas operaciones estas requieren de dos variables,
una de ellas la que se esta trabajando y la segunda un error que si todo va bien devuelve un valor nil. Si no devuelve nil usamos una condición if para devolver un mensaje de error:

.. code-block:: GO
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "strconv"
    )

    func main() {

        num := "40.36"

        num_entero, err := strconv.Atoi(num)

        // en este caso manejamos el error:
        if err != nil {
            log.Fatal(err, "\n El valor introducido no es un entero")
        }

        fmt.Println(num_entero)

    }


.. note:
    En este ejemplo se puede ver también el uso de la librería log

Programación modular
####################

Funciones
*********

* Procedimienos:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // declarar una función:
    func saludar() {
        fmt.Println("Saludo desde función")
    }

    func main() {
        // utilizar una función:
        saludar()
    }


* funciones:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // las funciones retornan un valor que se debe definir:
    func saludar() string {
        return "Saludo desde función"
    }

    func main() {

        // utilizar una función:
        fmt.Println(saludar())
    }


* uso de parámetros:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // los parametros se reciben con un valor definido::
    func saludar(nombre string) string {
        saludo := "Hola " + nombre
        return saludo
    }

    func main() {

        // pasar un parámetro:
        fmt.Println(saludar("Guillermo"))
    }

* Recibir parámetros indefinidos:

.. code-block:: GO 
    :linenos:

    package main

    import (
        "fmt"
    )

    // enviar parámetros de forma dinámica:
    func imprimir(cosas ...string) {
        fmt.Println(cosas)
    }

    func main() {

        imprimir("Consola", "Movil", "Tablet")

    }

* Retorno múltiple:

.. code-block:: GO 
    :linenos:

    package main

    package main

    import "fmt"

    // se define entre parentesis el tipo de devolución de varios valores:
    func nombreCompleto(nombre string, apellidos string) (string, string) {
        // se devuelven dos valores:
        return nombre, apellidos
    }

    func main() {
        // asignamos los valores a las variables:
        n, m := nombreCompleto("Guillermo", "Granados Gómez")

        // asignar un elemento con retorno múltiple:
        soloNombre, _ := nombreCompleto("Guillermo", "Granados Gómez")

        fmt.Println("Me llamo", n, m)
        fmt.Println("Solo mi nombre es:", soloNombre)
    }

* Funciones anónimas:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // se crea la función:
    func sumar(a, b int) int {
        return a + b
    }

    func main() {
        // se crea una variable con las caracteristicas de la función:
        var operacion func(int, int) int

        // y se asigna la función anterior a la declaración anterior:
        operacion = sumar

        fmt.Println(operacion(20, 15))
    }

Programación orientada a objetos
################################

El paradigma orientado a objetos en GO cambia radicalmente frente a otro lenguajes sustituyendo las clases por estructuras.

Structs
*******
Los Structs son estructuras de datos similares a las clases con la diferencia que estos carecen de constructores y métodos de antemano.

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // Crear una estructura:
    type Consola struct {
        marca       string
        modelo      string
        lanzamiento int
    }

    func main() {
        // crear un nuevo objeto del tipo Consola:
        playstation := Consola{marca: "Sony", modelo: "Playstation", lanzamiento: 1994}

        // uso de atributos:
        fmt.Println("La consola", playstation.marca, playstation.modelo, "fue lanzada en", playstation.lanzamiento)
    }

Métodos de structs
******************

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    type Consola struct {
        marca       string
        modelo      string
        lanzamiento int
    }

    // Método de Consola:
    // los métodos reciben primero un puntero a la structura y luego los datos:
    func (c *Consola) imprimir() { // en los paréntesis de imprimir recibe los parámetros requeridos:
        fmt.Println("La consola", c.marca, c.modelo, "fue lanzada en", c.lanzamiento)
    }

    func main() {
        playstation := Consola{marca: "Sony", modelo: "Playstation", lanzamiento: 1994}

        // ejecutar la función:
        playstation.imprimir()
    }


Herencia
********

- uso de clases no instanciables:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    type Consola struct {
        marca       string
        modelo      string
        lanzamiento int
    }

    func (c *Consola) imprimir() {
        fmt.Println("La consola", c.marca, c.modelo, "fue lanzada en", c.lanzamiento)
    }

    // Herencia:
    type Portatil struct {
        // cargar el struct del que se quiere heredar:
        Consola
        alimentacion string // se pueden añadir nuevos atributos
    }

    // también se pueden añadir métodos que utilicen los atributos y métodos del padre:
    func (p *Portatil) imp_portatil() {
        fmt.Println("La consola", p.marca, p.modelo, "fue lanzada en", p.lanzamiento, "y utiliza", p.alimentacion, "para funcionar")
    }

    func main() {
        playstation := Consola{marca: "Sony", modelo: "Playstation", lanzamiento: 1994}

        playstation.imprimir()

        // crear objeto, aqui solo se puede añadir los atributos existentes en el struct:
        gameboy := Portatil{alimentacion: "4 Pilas AAA"}
        // para añadir los atributos del padre se realiza de forma individual:
        gameboy.marca = "Nintendo"
        gameboy.modelo = "Gameboy"
        gameboy.lanzamiento = 1990

        // se puede ver como se aislan los atributos del padre y los del hijo:
        fmt.Println(gameboy)

        gameboy.imprimir()
        gameboy.imp_portatil()
    }


Interfaces
**********

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // se crea un interface y se le asignan los métodos del struct:
    type Printer interface {
        imprimir()
        encender()
    }

    type Consola struct {
        marca       string
        modelo      string
        lanzamiento int
    }

    func (c *Consola) imprimir() {
        fmt.Println("La consola", c.marca, c.modelo, "fue lanzada en", c.lanzamiento)
    }

    func (c *Consola) encender() {
        fmt.Println("Se ha encendido la", c.modelo)
    }

    type Portatil struct {
        consola      Consola
        alimentacion string
    }

    // se crean las funciones que manejará los métodos usando el interface:
    func imprimirConsola(printer Printer) {
        printer.imprimir()
    }

    func encenderConsola(printer Printer) {
        printer.encender()
    }

    func main() {
        playstation := Consola{marca: "Sony", modelo: "Playstation", lanzamiento: 1994}
        // se utiliza el interface en lugar
        imprimirConsola(&playstation)
        encenderConsola(&playstation)
    }


Importar y exportar
###################

Paquetes en GO
**************
GO reconoce cada carpeta como un paquete, de este modo en una aplicación básica existirá un archivo main.go referenciando al paquete main y el resto
de archivos exportarán sus funciones automáticamente si estan son públicas, que en GO las funciones públicas comienzan en **Mayúscula**.

- Paso 1: Crear nuevo directorio y dentro un archivo **main.go**
- Paso 2: Crear archivo go.mod - Abrir terminal en la raiz del proyecto y ejectuar ``go mod init nombre_proyecto``
- Paso 3: Crear un nuevo paquete **consolas** y dentro un archivo al que llamaremos **listar.go**:

.. code-block:: GO 
    :linenos:

    package consolas // cada paquete lleva el nombre de su carpeta correspondiente

    import "fmt"

    // las funciones solo serán públicas si las ponemos en mayúsculas:
    func Listado() {
        fmt.Println("NES, Gameboy, Megadrive, Saturn")
    }

- Paso 4: Importar paquete y ejecutar función en **main.go**:

.. code-block::
    :linenos:

    package consolas // cada paquete lleva el nombre de su carpeta correspondiente

    import "fmt"

    // las funciones solo serán públicas si las ponemos en mayúsculas:
    func Listado() {
        fmt.Println("NES, Gameboy, Megadrive, Saturn")
    }

- Paso 5: Para ejecutar todo el proyecto ir a raiz desde consola y ejecutar ``go run .``

