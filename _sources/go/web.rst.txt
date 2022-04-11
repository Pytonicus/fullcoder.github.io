Desarrollo Web 
==============

.. image:: /logos/logo-go.png
    :scale: 30%
    :alt: Logo GO
    :align: center

.. |date| date::
.. |time| date:: %H:%M

    
Trabajar con Go para desarrollo de aplicaciones web.
   
.. contents:: Índice

Crear servidor  
##############

Creación y arranque de main
***************************

- Paso 1: Crear carpeta para el proyecto **pruebaweb**
- Paso 2: Crear archivo main.go con el código:

.. code-block:: GO 
    :linenos:

    package main

    import (
        "log"
        "net/http"
    )

    func main() {
        // crear nuevo servidor:
        server := http.ListenAndServe("localhost:8000", nil)

        // analizamos si nos devuelve un error:
        log.Fatal(server)
    }

Paso 3: Acceder a la carpeta raiz **pruebaweb** desde terminal y ejecutar ``go run main.go``

.. attention::
    El servidor se ejecutará pero nos dará error 404, eso es debido a que no tenemos rutas o handlers asignados.


Crear un handle
***************
Los handlers (manejadores) reciben una ruta y retornan un comportamiento a través del navegador web.

.. code-block:: GO
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "net/http"
    )

    // función handle que recibe un parametro para escribir una respuesta y otro para recibir información:
    func Index(rw http.ResponseWriter, r *http.Request) {
        // imprimos al navegador un mensaje:
        fmt.Fprintln(rw, "<h1>Hola desde GO</h1>")
    }

    func main() {
        // crear una ruta con un handle para llamar una función handle:
        http.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", nil)

        log.Fatal(server)
    }

.. note::
    Dicho en otro lenguaje o framework, la función HandleFunc sería un router y la función que recibe con el write y el request sería un controlador.


Métodos Request
***************

.. code-block:: GO 
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "net/http"
    )

    func Index(rw http.ResponseWriter, r *http.Request) {
        fmt.Fprintln(rw, "<h1>Hola desde GO</h1>")
        // el método está guardado en el parámetro r:
        fmt.Fprintln(rw, "<h2>Por defecto se trabaja con "+r.Method+" </h2>")
    }

    func main() {
        http.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", nil)

        log.Fatal(server)
    }

.. note::
    No se ahondará demasiado en los métodos aquí porque más adelante se utilizarán con mux.

Error 404
*********

Según el sitio de desarrollo de Mozilla los código de estado son:
1. Respuestas informativas (100-199)
2. Respuestas satisfactorias (200-299)
3. Redirecciones (300-399)
4. Errores de clientes (400-499)
5. Errores del servidor (500-599)

.. code-block:: GO 
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "net/http"
    )

    func Index(rw http.ResponseWriter, r *http.Request) {
        fmt.Fprintln(rw, "<h1>Hola desde GO</h1>")
        fmt.Fprintln(rw, "<h2>Por defecto se trabaja con "+r.Method+" </h2>")
    }

    // crear un handle para el 404:
    func Error(rw http.ResponseWriter, r *http.Request) {
        // se utiliza la función notfound para lanzar correctamente el 404:
        http.Error(rw, "La página no se encuentra", http.StatusNotFound)
    }

    func main() {
        http.HandleFunc("/", Index)
        // se crea una ruta para el error:
        http.HandleFunc("/error", Error)

        server := http.ListenAndServe("localhost:8000", nil)

        log.Fatal(server)
    }

.. note::
    Se puede encontrar más información de errores en la documentación de la librería http: https://pkg.go.dev/net/http#Error 

Argumentos URL
**************

Suponiendo que tenemos la siguiente ruta: http://localhost:8000/saludar?nombre=Guillermo&apellidos=Granados%20G%C3%B3mez

.. code-block:: GO
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "net/http"
    )

    func Index(rw http.ResponseWriter, r *http.Request) {
        fmt.Fprintln(rw, "<h1>Hola desde GO</h1>")
        fmt.Fprintln(rw, "<h2>Por defecto se trabaja con "+r.Method+" </h2>")
    }

    func Saludar(rw http.ResponseWriter, r *http.Request) {
        // recuperar url (/saludar en este caso):
        fmt.Fprintln(rw, r.URL)
        // separar y mapear argumentos en un array:
        fmt.Fprintln(rw, r.URL.Query())

        // recuperar individualmente los parámetros:
        nombre := r.URL.Query().Get("nombre")
        apellidos := r.URL.Query().Get("apellidos")
        fmt.Fprintln(rw, "Hola", nombre, apellidos)

    }

    func main() {
        http.HandleFunc("/", Index)
        http.HandleFunc("/saludar", Saludar)

        server := http.ListenAndServe("localhost:8000", nil)

        log.Fatal(server)
    }

 
Gorilla Mux
###########

Mux es una librería que se utiliza para gestionar rutas en GO:
- Paso 1:

...

Server Hot Reload
#################
 
Para realizar hot reload y no tener que estar compilando cada cambio y lanzando el servidor existe 
la librería **fresh**:

- Paso 1: ejecutar en la terminal ``go mod init nombre_proyecto`` 
- Paso 2: ejecutar en la terminal ``go get github.com/pilu/fresh``
- Paso 3: ejecutar el proyecto escribiendo en terminal ``fresh``

Templates
#########


