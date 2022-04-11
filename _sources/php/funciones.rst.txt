Funciones predefinidas
======================

.. image:: /logos/logo-php.png
    :scale: 15%
    :alt: Logo PHP
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M
  

Funciones más usadas en PHP 7.4

.. contents:: Índice
 
Información del servidor 
########################

En un archivo vacío se guarda la siguiente función:
 
.. code-block:: php
    :linenos:

    <?php 
        phpinfo();
    ?>

Manipulación de variables
#########################

Averiguar tipo de dato
**********************

.. code-block:: php
    :linenos:

    <?php
        $cadena = "Soy una cadena de texto";

        echo gettype($cadena);
    ?>

Validación
**********

.. code-block:: php
    :linenos:

    <?php
        // variable definida:
        $gatos = "";

        // guarda el valor 1 (true) si ha sido definida la variable:
        $definida = isset($gatos);
        echo $definida;

        echo "<br>";

        // uso como validador:
        $comprobar = isset($gatos) ? "Existen gatos en el código" : "No existen gatos en el código";
        echo $comprobar;
    ?>

Destrucción
***********

.. code-block:: php
    :linenos:

    <?php
        $gatos = "";

        // destruir la variable gatos:
        unset($gatos);

        $comprobar = isset($gatos) ? "Existen gatos en el código" : "No existen gatos en el código";
        echo $comprobar;
    ?>

Manipulación de Strings
#######################

Longitud de un String 
*********************

.. code-block:: php
    :linenos:

    <?php
        $consola = "Nintendo DS";
        echo strlen($consola);
    ?>

Conversión a String 
*******************

.. code-block:: php
    :linenos:

    <?php
        $lanzamiento = 2005;
        $fechaLanzamiento = "Lanzamiento en " . (String)$lanzamiento;
        echo $fechaLanzamiento
    ?>

Conversión String a Array
*************************

.. code-block:: php
    :linenos:

    <?php
        $string_consolas = "Nintendo DS, Nintendo 64, Super Nintendo";
        $array_consolas = explode(", ", $string_consolas);
        var_dump($array_consolas);
    ?>

Reemplazar palabras
*******************

.. code-block:: php
    :linenos:

    <?php
        $descripcion = "La Nintendo Mega Drive es la mejor consola de Nintendo hasta la fecha";
        echo str_replace("Nintendo", "Sega", $descripcion);
    ?>

Primera letra mayúscula
***********************

.. code-block:: php
    :linenos:

    <?php
        $descripcion = "La Nintendo Mega Drive es la mejor consola de Nintendo hasta la fecha";
        
        // Primera palabra con letra mayúscula:
        echo ucfirst($descripcion);
        echo "<br>";

        // todas las palabras con letra mayúscula:
        echo ucwords($descripcion);
    ?>

Conversión a mayúsculas
***********************

.. code-block:: php
    :linenos:

    <?php
        $descripcion = strtoupper("La Nintendo Mega Drive es la mejor consola de Nintendo hasta la fecha");
        echo $descripcion;
    ?>

Conversión a minúsculas
***********************

.. code-block:: php
    :linenos:

    <?php
        $descripcion = "La Nintendo Mega Drive es la mejor consola de Nintendo hasta la fecha";
        echo strtolower($descripcion);
    ?>

Eliminar espacios en blanco a los lados
***************************************

.. code-block:: php
    :linenos:

    <?php
        $texto = "   soy un texto con espacios   ";
        echo trim($texto);
    ?>

Localizar posición de caracteres en cadena
******************************************

.. code-block:: php
    :linenos:

    <?php 
        $frase = "En esta frase se esconde el nombre Pepe";
        
        if(strpos($frase, "Pepe") == true){
            echo "Hemos encontrado a Pepe!";
        }
    ?>

Manipulación de Números
#######################

Conversión String a Integer
***************************

.. code-block:: php
    :linenos:

    <?php
        $numeroCadena = "173";
        $suma = (int)$numeroCadena + 50;
        echo "el resultado es: " . $suma;
    ?>

Conversión String a Float
*************************

.. code-block:: php
    :linenos:

    <?php
        $numeroCadena = "17.27";
        $suma = (float)$numeroCadena + 50;
        echo "el resultado es: " . $suma;
    ?>

Redondeo de decimales
*********************

.. code-block:: php
    :linenos:

    <?php
        $numeroDecimal = 23.783728;

        // Redondeo a entero:
        echo round($numeroDecimal);

        echo "<br>";

        // Redondeo a decimal:
        echo round($numeroDecimal, 4); // segundo parámetro define cantidad de dígitos a devolver
    ?>

Manipulación de Arrays
######################

Imprimir contenido
******************

.. code-block:: php
    :linenos:

    <?php
        $fabricantes = ["Nintendo", "Sega", "Sony", "Microsoft"];

        // Imprimir contenido de una variable y el formato:
        var_dump($fabricantes);

        // Imprimir con un formato más legible:
        echo "<pre>";
        print_r($fabricantes);
        echo "</pre>";
    ?>
 
Añadir elemento al array
************************
 
.. code-block:: php
    :linenos:

    <?php 
        // tenemos un array:
        $consolasSony = ["PlayStation", "PlayStation 2", "PlayStation 3"];

        print_r($consolasSony);

        // utilizamos la siguiente función en la cual el primer parámetro es el array anterior y los siguientes los elementos que se añaden:
        array_push($consolasSony, "PlayStation 4", "PlayStation 5");

        print_r($consolasSony);
    ?>

Rango de números
****************

.. code-block:: php
    :linenos:

    <?php
        // guardar un rango de números:
        $rango = range(0, 20);
        var_dump($rango);

        // uso en bucles:
        foreach(range(0, 10) as $numero){
            echo $numero . "<br />";
        }
    ?>

Recuperar valor máximo
**********************

.. code-block:: php
    :linenos:

    <?php
        $fechas = [1932, 1930, 1959, 1092, 1209];

        echo "El año mas reciente es: " . max($fechas);
    ?>

Recuperar valor mínimo
**********************

.. code-block:: php
    :linenos:

    <?php
        $fechas = [1932, 1930, 1959, 1092, 1209];

        echo "El año mas antiguo es: " . min($fechas);
    ?>

Suma total de todos los valores
*******************************

.. code-block:: php
    :linenos:

    <?php
        $carro = [20.85, 10.40, 19.94, 12, 9];

        echo "El total de la compra es: " . array_sum($carro) . "€";
    ?>

Manipulación JSON
#################

Convertir Array en JSON 
***********************

.. code-block:: php
    :linenos:

    <?php 
        // Array a convertir:
        $videoconsolas = array(
            "megadrive" => [
                "lanzamiento" => 1988,
                "fabricante" => "Sega"
            ],
            "snes" => [
                "lanzamiento" => 1990,
                "fabricante" => "Nintendo"
            ],
            "playstation" => [
                "lanzamiento" => 1994,
                "fabricante" => "Sony"
            ]  
        );

        // Imprmir array codificado en formato JSON:
        echo json_encode($videoconsolas);
    ?>

Convertir JSON en Array 
***********************

.. code-block:: php
    :linenos:

    <?php 
        // Se realiza una llamada con CURL:
        $curl = curl_init("http://api.plos.org/search?q=title:DNA");
        // La siguiente función prepara el formato de almacenamiento en String:
        curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
        // Se ejecuta la operación y se guarda en una variable::
        $response = curl_exec($curl);
        // Pasamos a la codificación en JSON:
        $data = json_decode($response);
        // Validar la salida desde metadatos:
        $info = curl_getinfo($curl);



        // Se ejecuta la respuesta si el resultado es correcto:
        if($info['http_code'] == 200 ){
            // ver el contenido de la variable:
            echo "<pre>";
            print_r($data);
            echo "</pre>";
        }else{
            echo "Error", curl_error($curl);
        }

    ?>

.. attention::
    Para poder trabajar con curl hay que instalar la dependencia ``sudo apt install php7.4-curl``

Manipulación de fechas 
######################

.. code-block:: php
    :linenos:

    <?php
        // devolver un valor:
        echo "Hoy es día " . date('d') . " de " . date('m') . " de " . date('Y');

        echo "<br>";
        // devolver fecha formateada:
        echo "Son las: " . date('H:m');
    ?>

* Códigos comunes para Fecha: 

+----------------------------------------------+---------+
| Tipo de valor                                | símbolo |
+==============================================+=========+
| Día en notación numeral                      | d       |
+----------------------------------------------+---------+
| Día por inicial                              | D       | 
+----------------------------------------------+---------+
| Día de la semana                             | l       |
+----------------------------------------------+---------+
| Dias transcurridos desde comienzos de año    | z       |
+----------------------------------------------+---------+
| Dias que tiene el mes corriente              | t       |
+----------------------------------------------+---------+
| Semanas transcurridas desde comienzos de año | W       |
+----------------------------------------------+---------+
| Mes actual en notación numeral               | m       |
+----------------------------------------------+---------+
| Mes actual en notación numeral sin cero      | n       |
+----------------------------------------------+---------+
| Iniciales del mes corriente                  | M       |
+----------------------------------------------+---------+
| Año corriente en notación numeral            | Y       |
+----------------------------------------------+---------+
| Año con notación numeral abreviada           | y       |
+----------------------------------------------+---------+
| Año bisiesto (devuelve 1 si es bisiesto)     | L       |
+----------------------------------------------+---------+
| Fecha en formato ISO-8601                    | c       |
+----------------------------------------------+---------+

* Códigos comunes para Hora:

+----------------------------------------------+---------+
| Tipo de valor                                | símbolo |
+==============================================+=========+
| Ver si la hora es AM o PM                    | a       |
+----------------------------------------------+---------+
| Ver si la hora es AM o PM en mayúsculas      | A       | 
+----------------------------------------------+---------+
| Hora en formato 12                           | g       |
+----------------------------------------------+---------+
| Hora en formato 24                           | G       |
+----------------------------------------------+---------+
| Hora en formato 12 con 0 inicial             | h       |
+----------------------------------------------+---------+
| Hora en formato 24 con 0 inicial             | H       |
+----------------------------------------------+---------+
| Minutos                                      | i       |
+----------------------------------------------+---------+
| Segundos                                     | s       |
+----------------------------------------------+---------+
| Microsegundos                                | u       |
+----------------------------------------------+---------+
| Zona Horaria                                 | e       |
+----------------------------------------------+---------+
| Horario de sol reducido                      | I       |
+----------------------------------------------+---------+
| Desfase meridiano de Greenwitch              | O       |
+----------------------------------------------+---------+
| Hora formato Swatch Internet Time            | B       |
+----------------------------------------------+---------+
| Hora formato UNIX                            | U       |
+----------------------------------------------+---------+


.. attention::
    Los valores textualizados de las fechas están en inglés

Tratamiento de archivos
#######################

Recuperar contenido de archivo 
******************************

.. code-block:: php
    :linenos:

    <?php
        $foto = file_get_contents('foto.jpg');
        echo $foto;
    ?>

Manipulación de archivos
************************

* Escritura de archivos:

.. code-block:: php
    :linenos:

    <?php
        $ip = $_SERVER['REMOTE_ADDR'];
        $navegador = $_SERVER['HTTP_USER_AGENT'];
        $contenido = date('U') . " - Fecha: " . date('Y/m/d - H:i:s') . " - Navegador: " . $navegador . " - IP: " . $ip ."\n";

        // establecemos el nombre de archivo que vamos a editar:
        $archivoLogs = 'logs.dat';
        // abrimos con permisos de creación extras:
        $manejador = fopen($archivoLogs, 'w+');
        // escribimos los cambios:
        fwrite($manejador,$contenido);
    ?>

* Lectura de archivos:

.. code-block:: php
    :linenos:

    <?php
        $archivoLogs = 'logs.dat';
        // abrimos el archivo con permisos de lectura:
        $manejador = fopen($archivoLogs, 'r');

        // establecemos la condición con fgetcsv() de manera que los dividirá:
        while($datos = fgetcsv($manejador,1000000, "-")){
            echo "<pre>";
            print_r($datos);
            echo "</pre>";
        }
        fclose($manejador);
    ?>

* Actualización de archivos:

.. code-block:: php
    :linenos:

    <?php
        $ip = $_SERVER['REMOTE_ADDR'];
        $navegador = $_SERVER['HTTP_USER_AGENT'];
        $contenido = date('U') . " - Fecha: " . date('Y/m/d - H:i:s') . " - Navegador: " . $navegador . " - IP: " . $ip ."\n";

        // establecemos el nombre de archivo que vamos a editar:
        $archivoLogs = 'logs.dat';
        // abrimos con permisos de actualizacion extras:
        $manejador = fopen($archivoLogs, 'a+');
        // escribimos los cambios:
        fwrite($manejador,$contenido);
    ?>

Manipulación de cabeceras
#########################

Redirección
***********

.. code-block:: php
    :linenos:

    <?php
        header('Location: https://www.prueba.com');
    ?>

Modificar el comportamiento de un script
****************************************

.. code-block:: php
    :linenos:

    <?php 
        // indica al navegador que el script php es una imagen.
        header('Content-type: image/jpg');

        $foto = file_get_contents('foto.jpg');
        echo $foto;
    ?>

* Lista de MIMES más comunes: https://developer.mozilla.org/es/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types

Descargar un archivo desde un script
************************************

.. code-block:: php
    :linenos:

    <?php 
        header('Content-type: image/jpg');
        // se define la disposición y el nombre que tendrá al ser descargado:
        header('Content-disposition: attachment; filename="descarga.jpg"');

        $foto = file_get_contents('foto.jpg');
    ?>

Tratamiento de CORS
*******************

.. code-block:: php
    :linenos:

    <?php 
        // Origen: *: todos | www.codigo.com: una url | null: bloquea cualquier origen excepto el mismo servidor:
        header('Access-Control-Allow-Origin: *');
        // Cabeceras permitidas separadas por comas:
        header("Access-Control-Allow-Headers: X-API-KEY, Origin, X-Requested-With, Content-Type, Accept, Access-Control-Request-Method");
        // Métodos permitidos separados por comas:
        header("Access-Control-Allow-Methods: GET, POST, OPTIONS, PUT, DELETE");

        echo "<h1>Sitio de prueba</h1>";
    ?>
 


 