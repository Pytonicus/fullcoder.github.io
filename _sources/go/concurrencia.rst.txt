Concurrencia
============
 
.. image:: /logos/logo-go.png
    :scale: 30%
    :alt: Logo GO
    :align: center

.. |date| date::
.. |time| date:: %H:%M

    
Concurrencia en GO o como trabajar en multihilo.
   
.. contents:: Índice



Creación de goRoutines y Channels
#################################

Las goRoutines se utilizan para ejecutar funciones en distintos hilos de manera que pueda ejecutarse el código 
de forma paralela y no tener que esperar a que acabe una rutina para comenzar otra.

Ejecución sin concurrencia 
**************************

.. code-block:: GO 
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "net/http"
    )

    func revisar(servidor string) {
        _, err := http.Get(servidor)

        if err != nil {
            log.Fatal(err)
        }

        fmt.Println(servidor, "en ejecución")
    }

    func main() {
        servidores := []string{
            "https://altiplaconsulting.com",
            "https://youtube.com",
            "https://google.com",
            "https://piptonita.com",
        }

        for _, servidor := range servidores {
            revisar(servidor)
        }

    }

Ejecución con concurrencia
**************************

.. code-block:: GO 
    :linenos:

    package main

    import (
        "fmt"
        "log"
        "net/http"
    )

    // la función recibirá el canal que se ha creado:
    func revisar(servidor string, canal chan string) {
        _, err := http.Get(servidor)

        if err != nil {
            log.Fatal(err)
        }

        // como ya no va a imprimir el mensaje se ejecuta del siguiente modo:
        canal <- servidor + " en ejecución"
    }
 
    func main() {
        // para leer los resultados se crea un canal:
        canal := make(chan string)

        servidores := []string{
            "https://altiplaconsulting.com",
            "https://youtube.com",
            "https://google.com",
            "https://piptonita.com",
        }

        for _, servidor := range servidores {
            // para activar la concurrencia añadimos go para que analice todos los servidores a la vez:
            go revisar(servidor, canal) // le pasamos también el canal
        }

        // ahora se crea otro bucle for para retornar lo que está devolviendo los canales:
        for i := 0; i < len(servidores); i++ {
            // se imprime el canal:
            fmt.Println(<-canal)
        }

    }

.. note::
    Se puede comprobar en el resultado de cada código que con la concurrencia ha devuelto 
    las páginas en distinto orden ya que las mostró nada más terminar de ejecutarlas.