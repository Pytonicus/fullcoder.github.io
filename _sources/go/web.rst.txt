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

Uso de Mux:

1. Instalar Gorilla mux: ``go get -u github.com/gorilla/mux``
2. Implementar su uso:

.. code-block:: go
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "net/http"

        "github.com/gorilla/mux" // se carga la libreria mux
    )

    func main() {
        // creamos el enrutador:
        router := mux.NewRouter().StrictSlash(true) // con la función strictslash hacemos rutas amigables

        // crear manejadores para rutas:
        router.HandleFunc("/", Index)

        fmt.Println("Servidor ejecutandose en http://localhost:8000")
        server := http.ListenAndServe(":8000", router) // cargamos el router donde antes estaba nil

        log.Fatal(server)

    }

    func Index(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Ejecutando ruta raiz desde Mux")
    }



attention::
    Recuerda inicializar el proyecto con el comando ``go mod init nombre_proyecto``


Parametros url
**************

.. code-block:: go 
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "net/http"

        "github.com/gorilla/mux"
    )

    func main() {
        router := mux.NewRouter().StrictSlash(true)

        router.HandleFunc("/", Index)
        // se crea una nueva ruta con un parametro:
        router.HandleFunc("/saludar/{nombre}", Saludar)

        fmt.Println("Servidor ejecutandose en http://localhost:8000")
        server := http.ListenAndServe(":8000", router)

        log.Fatal(server)

    }

    func Index(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Ejecutando ruta raiz desde Mux")
    }

    // se crea la función que manejará la respuesta:
    func Saludar(w http.ResponseWriter, r *http.Request) {
        // recuperar parametros url:
        params := mux.Vars(r)
        // asignar el nombre recuperado a una variable:
        nombre := params["nombre"]

        fmt.Fprintf(w, "Hola %s", nombre)
    }


Server Hot Reload
#################
 
Para realizar hot reload y no tener que estar compilando cada cambio y lanzando el servidor existe 
la librería **fresh**:

- Paso 1: ejecutar en la terminal ``go get github.com/pilu/fresh``
- Paso 2: ejecutar el proyecto escribiendo en terminal ``fresh``

attention::
    Recuerda inicializar el proyecto con el comando ``go mod init nombre_proyecto``


Templates
#########

Configuración del proyecto
**************************

Para trabajar con templates tenemos paquetes oficiales como **Text/template** o **HTML/template**

Estas librerías ya vienen instaladas con GO.

Cargar plantilla en ruta 
************************

- En la carpeta del proyecto se crea el archivo **main.go**:

.. code-block:: go 
    :linenos:

    package main

    import (
        "fmt"
        "html/template" // cargamos la librería template
        "log"
        "net/http"
    )

    func Index(rw http.ResponseWriter, r *http.Request) {
        // utilizamos la librería template para cargar el archivo index.html:
        template, err := template.ParseFiles("index.html")

        if err != nil {
            panic(err)
        }
        // ejecutamos el template al que pasamos responsewrite, la data (nil en este caso)
        template.Execute(rw, nil)
    }

    func main() {
        mux := http.NewServeMux()

        mux.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", mux)

        fmt.Println("Servidor corriendo en puerto 8000")
        log.Fatal(server)
    }

- Ahora se crea un archivo **index.html** en la raiz:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Go Main</title>
    </head>
    <body>
        <h1>Bienvenido al Game Room</h1>
    </body>
    </html>


Comunicarse con el template
***************************

Para pasar datos al template lo hacemos cargando en el lugar donde pusimos nil:

.. code-block:: go 
    :linenos:

    package main

    package main

    import (
        "fmt"
        "html/template"
        "log"
        "net/http"
    )

    // se crea una estructura (siempre mayúsculas):
    type Consolas struct {
        Marca  string
        Modelo string
        Lanzamiento int
    }

    func Index(rw http.ResponseWriter, r *http.Request) {
        template, err := template.ParseFiles("index.html")

        // crear un valor consola:
        megadrive := Consolas{"Sega", "Mega Drive", 1989}

        if err != nil {
            panic(err)
        }

        // se carga en el lugar del nil:
        template.Execute(rw, megadrive)
    }

    func main() {
        mux := http.NewServeMux()

        mux.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", mux)

        fmt.Println("Servidor corriendo en puerto 8000")
        log.Fatal(server)
    }

- Ahora el template **index.html** puede trabajar con los datos:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Go Main</title>
    </head>
    <body>
        <h1>Bienvenido al Game Room</h1>
        <!-- Se carga con llaves dobles el valor como un objeto: -->
        <h2>Esta disponible la consola: {{ .Marca }} {{ .Modelo }}</h2>
    </body>
    </html>


Crear variables en plantillas 
*****************************

Para crear variables en templates se usa la palabra reservada with:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Go Main</title>
    </head>
    <body>
        <h1>Bienvenido al Game Room</h1>
        <h2>Esta disponible la consola: {{ .Marca }} {{ .Modelo }}</h2>

        <!-- Crear variables: -->
        {{ with $cosa := "algo" }}
        <!-- Ejecutar variable algo: -->
        {{ $cosa }}


        <!-- Definir donde acaba la variable (bloque fijo) -->
        {{ end }}
    </body>
    </html>


Condicional if-else
*******************

Las condicionales en los templates se aprovechan de una serie de operadores lógicos y condicionales modificados.


Operadores Lógicos 
++++++++++++++++++

- **&&** es sustituido por **and** 
- **||** es sustituido por **or**
- **!** es sustituido por **not** 


Operadores Condicionales 
++++++++++++++++++++++++

- **==** es sustituido por **eq**
- **!=** es sustituido por **ne**
- **<** es sustituido por **lt**
- **<=** es sustituido por **le**
- **>** es sustituido por **gt**
- **>=** es sustituido por **ge**


Uso de condicional
++++++++++++++++++

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Go Main</title>
    </head>
    <body>
        <h1>Bienvenido al Game Room</h1>
        <h2>Esta disponible la consola: {{ .Marca }} {{ .Modelo }}</h2>
        
        <!-- La condición se pone antes del dato a comparar -->
        {{ if le .Lanzamiento 1990}}
            <h3>La consola es de los 80</h3>
        {{ else }}
            <h3>La consola es de {{ .Lanzamiento }}</h3>
        {{ end }}
    </body>
    </html>


Bucles
******

En primer lugar se va a añadir un nuevo campo al struct de Consolas con un mapa de juegos:

.. code-block:: go 
    :linenos:

    package main

    import (
        "fmt"
        "html/template"
        "log"
        "net/http"
    )

    // se añade un array con juegos:
    type Consolas struct {
        Marca       string
        Modelo      string
        Lanzamiento int
        Juegos      []Juego
    }

    // crear la estructura del array:
    type Juego struct {
        Titulo string
    }

    func Index(rw http.ResponseWriter, r *http.Request) {
        template, err := template.ParseFiles("index.html")

        // crear juegos:
        j1 := Juego{"Sonic the Hedgehog"}
        j2 := Juego{"Alex Kidd"}
        j3 := Juego{"Virtua Fighter"}

        // crear lista de juegos:
        juegos := []Juego{j1, j2, j3}

        // actualizar el objeto megadrive:
        megadrive := Consolas{"Sega", "Mega Drive", 1989, juegos}

        if err != nil {
            panic(err)
        }else {
            template.Execute(rw, nil)
        }
    }

    func main() {
        mux := http.NewServeMux()

        mux.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", mux)

        fmt.Println("Servidor corriendo en puerto 8000")
        log.Fatal(server)
    }

Ahora se va a recorrer el listado en el template:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Go Main</title>
    </head>
    <body>
        <h1>Bienvenido al Game Room</h1>
        <h2>Esta disponible la consola: {{ .Marca }} {{ .Modelo }}</h2>
        
        <!-- recorrer y añadir a la lista los juegos: -->
        <ul>
            {{ range .Juegos}}
                <li>{{ .Titulo }}</li>
            {{ end }}
        </ul>
    </body>
    </html>


Funciones en plantillas 
***********************

- En main.go se crea una función que saluda:

.. code-block:: go 
    :linenos:

    package main

    import (
        "fmt"
        "html/template"
        "log"
        "net/http"
    )

    // crear funciones:
    func Saludar(nombre string) string {
        return "Bienvenid@ " + nombre + " al game room"
    }

    func Index(rw http.ResponseWriter, r *http.Request) {
        // se crea un mapa de funciones para templates:
        funciones := template.FuncMap{
            "saludar": Saludar,
        }

        // cambiamos el cargador de template por new y le pasamos la función:
        template, err := template.New("index.html").Funcs(funciones).ParseFiles("index.html")

        if err != nil {
            panic(err)
        }else {
            template.Execute(rw, nil)
        }
    }

    func main() {
        mux := http.NewServeMux()

        mux.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", mux)

        fmt.Println("Servidor corriendo en puerto 8000")
        log.Fatal(server)
    }


- Ahora a probar el template:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Go Main</title>
    </head>
    <body>
        <!-- se carga tal cual el nombre de la key del mapa y si lleva parametros se pone su valor entre comillas: -->
        {{ saludar "Guillermo" }}
    </body>
    </html>


Herencia de plantillas 
**********************

Como en otros sistemas de plantillas, las plantillas pueden heredar de otras:

- Se crea una nueva plantilla llamada por ejemplo **base.html**:

.. code-block:: html 
    :linenos:

    {{ define "head" }}
    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Go Main</title>
    </head>
    <body>
    {{ ende }}

    {{define "footer"}}
    </body>
    </html>
    {{ ende }}


- Se añade en **main.go** la carga de la plantilla:

.. code-block:: go 
    :linenos:

    package main

    import (
        "fmt"
        "html/template"
        "log"
        "net/http"
    )

    func Saludar(nombre string) string {
        return "Bienvenid@ " + nombre + " al game room"
    }

    func Index(rw http.ResponseWriter, r *http.Request) {
        funciones := template.FuncMap{
            "saludar": Saludar,
        }

        // hay que pasar por parsefiles el base.html:
        template, err := template.New("index.html").Funcs(funciones).ParseFiles("index.html", "base.html")

        if err != nil {
            panic(err)
        }else {
            template.Execute(rw, nil)
        }
    }

    func main() {
        mux := http.NewServeMux()

        mux.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", mux)

        fmt.Println("Servidor corriendo en puerto 8000")
        log.Fatal(server)
    }


- Y por último implementamos en el **index.html**:

.. code-block:: html 
    :linenos:

    {{ template "head" }}
    <!-- se carga tal cual el nombre de la key del mapa: -->
    <h1>{{ saludar "Guillermo" }}</h1>
    {{ template "footer"}}


Manejo de errores 
*****************

Lo ideal cuando falla algo en web es manejar el error con mensajes y códigos de error web:

.. code-block:: go 
    :linenos:

    package main

    import (
        "fmt"
        "html/template"
        "log"
        "net/http"
    )

    func Index(rw http.ResponseWriter, r *http.Request) {
        // vamos a buscar un template que no funciona:
        template, err := template.ParseFiles("fake.html")

        if err != nil {
            // para evitar que rompa la funcionalidad controlamos el error con http.error:
            http.Error(rw, "No es posible cargar la página", http.StatusInternalServerError)
        } else {
            template.Execute(rw, nil)
        }
    }

    func main() {
        mux := http.NewServeMux()

        mux.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", mux)

        fmt.Println("Servidor corriendo en puerto 8000")
        log.Fatal(server)
    }


Rutas web 
*********

Los enlaces funcionan con rutas relativas que apuntan al handler de Mux:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <h1>Hola</h1>
        <ul>
            <li><a href="/">Inicio</a></li>
            <li><a href="/otra-web">Inicio</a></li>
        </ul>
    </body>
    </html>

Cargar archivos estáticos
*************************

- En la raiz del proyecto se crea una carpeta llamada **static**
- En **main.go** preparamos la ruta a la carpeta **static**:

.. code-block:: go 
    :linenos:

    package main

    import (
        "fmt"
        "html/template"
        "log"
        "net/http"
    )

    func Index(rw http.ResponseWriter, r *http.Request) {

        template, err := template.ParseFiles("index.html")

        if err != nil {
            http.Error(rw, "No es posible cargar la página", http.StatusInternalServerError)
        } else {
            template.Execute(rw, nil)
        }
    }

    func main() {
        
        // Creamos la ruta a la carpeta de estáticos:
        staticFile := http.FileServer(http.Dir("static"))

        mux := http.NewServeMux()

        // creamos un handler para la ruta:
        mux.Handle("/static/", http.StripPrefix("/static/", staticFile))

        mux.HandleFunc("/", Index)

        server := http.ListenAndServe("localhost:8000", mux)

        fmt.Println("Servidor corriendo en puerto 8000")
        log.Fatal(server)
    }

- Ahora se crea dentro de la carpeta **static** la carpeta **css** y dentro un archivo **main.css**:

.. code-block:: css 
    :linenos:

    body{
        width:100%;
        background-color: red;
    }

- Por último vamos a **index.html** y en la cabezera se carga la hoja:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- se utiliza la ruta relativa para recuperar el css: -->
        <link rel="stylesheet" href="/static/css/main.css">
        <title>Document</title>
    </head>
    <body>
        <h1>Hola</h1>
        <ul>
            <li><a href="/">Inicio</a></li>
            <li><a href="/otra-web">Inicio</a></li>
        </ul>
    </body>
    </html>


Modelos y CRUD
##############

Para comenzar a trabajar con modelos hacemos lo siguiente:

Paso 1. En la raiz crear la carpeta **models**
Paso 2. Crear un fichero **consola.go** que tendrá el modelo de consolas:

.. code-block:: go 
    :linenos:

    // asignamos el nombre del paquete (directorio)
    package models

    // se define un struct para el modelo:
    type Consola struct { // con la sentencia json va a imprimir el nombre que asignemos evitando mayúsculas:
        Id          int    `json:"id"`
        Modelo      string `json:"modelo"`
        Marca       string `json:"marca"`
        Lanzamiento int    `json:"lanzamiento"`
    }

    // se define también la colección de Consolas:
    type Consolas []Consola


Crear controlador
*****************
 
Procedemos a crear un directorio en raiz llamado **controllers** y creamos el primer controlador **consola.go**:

Listar Elementos
****************

Paso 1. Editar **controllers/consola.go**:

.. code-block:: go 
    :linenos:

    package controllers

    // se importan las librerías necesarias:
    import (
        "encoding/json"
        "go_api/models"
        "net/http"
    )

    // ahora se crean las funciones que controlarán la respuesta:
    func ConsolaList(w http.ResponseWriter, r *http.Request) {
        // se crea el listado de juegos:
        consolas := models.Consolas{
            // se crea cada uno de los juegos con su modelo:
            models.Consola{1, "Mega Drive", "Sega", 1989},
            models.Consola{2, "Playstation", "Sony", 1995},
            models.Consola{3, "GameBoy", "Nintendo", 1988},
        }

        // retornamos en JSON la lista:
        json.NewEncoder(w).Encode(consolas)
    }

Paso 2. Crear ruta en **main.go**:

.. code-block:: go 
    :linenos:

    package main

    import (
        "fmt"
        "go_api/controllers" // se importan los controladores
        "log"
        "net/http"

        "github.com/gorilla/mux"
    )

    func main() {
        router := mux.NewRouter().StrictSlash(true)

        router.HandleFunc("/", Index)
        router.HandleFunc("/saludar/{nombre}", Saludar)
        // creamos una ruta pora listar peliculas y otra para pelicula por id:
        router.HandleFunc("/consolas", controllers.ConsolaList)

        fmt.Println("Servidor ejecutandose en http://localhost:8000")
        server := http.ListenAndServe(":8000", router)

        log.Fatal(server)

    }

    func Index(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Ejecutando ruta raiz desde Mux")
    }

    func Saludar(w http.ResponseWriter, r *http.Request) {
        params := mux.Vars(r)
        nombre := params["nombre"]

        fmt.Fprintf(w, "Hola %s", nombre)
    }
