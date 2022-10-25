Testing 
=======

.. image:: /logos/logo-go.png
    :scale: 30%
    :alt: Logo GO
    :align: center

.. |date| date::
.. |time| date:: %H:%M

     
Testing y pruebas en GO 
#######################

Test Unitario
*************
Los test unitarios se pueden realizar a los paquetes que se vayan creando en GO:

- Paso 1: Crear un nuevo paquete en el proyecto llamado **calcular**
- Paso 2: Crear un archivo llamado **sumar.go**:

.. code-block:: GO
    :linenos:

    package calcular

    func Suma(a, b int) int {
        return a + b
    }

- Paso 3: Crear un archivo para los test **sumar_test.go**:

.. code-block:: GO 
    :linenos:

    package calcular

    import "testing"

    // se crea una función que recibe el paquete testing:
    func TestSuma(t *testing.T) {
        // se ejecuta la función a testear:
        total := Suma(5, 5) // así dará error porque espera 15, cambiar un 5 por un 10 dara OK

        // se comprueba si algo no ha salido tal y como se esperaría:
        if total != 15 {
            // se devuelve un error:
            t.Errorf("Suma incorrecta, tiene %d y se esperaba %d", total, 15)
        }
    }

- Paso 4: Ejecutar el test abriendo una terminal en la carpeta **calcular** con el comando ``go test``


.. attention::
    Recuerda ejecutar **go mod init nombre_proyecto** antes de trabajar con paquetes
