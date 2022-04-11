Sintaxis PHP
============

.. image:: /logos/logo-php.png
    :scale: 15%
    :alt: Logo PHP
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Sintáxis básica de PHP 7.4
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################
    
Instalación
***********
* Instalación: ``sudo apt install php7.4``
* Extensión de archivos: **.php**

Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: php
    :linenos:
 
    // Comentario de una sola línea

* Comentarios multilínea:

.. code-block:: php
    :linenos:

    /* Este comentario 
    tiene más de una línea.
    Puede servir para escribir
    un manual u otras cosas.
    */

Entrada y salida estandar
*************************
Datos de entrada y salida a través de la consola y/o el navegador.

.. code-block:: php 
    :linenos:

    <?php
        // echo:
        echo "hola mundo";

        // print:
        print("Hola mundo");
    ?>

.. attention::
    No existe una entrada estandar como tal, en todo caso sería mediante métodos GET, POST, etc.

Estructura en php
*****************

* Código PHP puro:

.. code-block:: php
    :linenos:

    <?php 
        $variable = 20;

        if($valor == 20){
            echo "el valor es igual";
        }
    ?> 
    
* código php junto a HTML:

.. code-block:: php
    :linenos:

    <?php 
        $titulo = "practicando PHP";
    ?>

    <html>
        <head>
        </head>
        <body>
            <h1><?php echo $titulo; ?></h1>
        </body>
    </html>

* También podemos cargar etiquetas HTML con PHP:

.. code-block:: php
    :linenos:

    <?php 
        echo "<p>Etiqueta incrustada desde php</p>";
    ?>

.. attention::
    Las líneas terminan en ; obligatóriamente.

Concatenación
*************
Concatenación de variables y cadenas se realiza con **.**

.. code-block:: php 
    :linenos:

    <?php
        echo "cadena concatenada a " . "otra cadena";

        echo "resultado en variable: " . $variable;
    ?>

PHP-CLI - Comandos de PHP
*************************

Comandos de PHP:

* php -v: versión usada
* php -m: módulos cargados
* php -i: configuración de php actual
* php -r: enviar código a ejecutar ej: ``echo "hola mundo"``
* php archivo.php: ejecutar un archivo php.
* php -S: ejecutar servidor php ``php -S localhost:8000``
* php -S -t: establecer un directorio inicial de arrance del server: ``php -S localhost:8000 -t inicial/``

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: php 
    :linenos:

    <?php 
        $cadena = "Cadena de texto";
        $entero = 27;
        $decimal = 23.27;
        $booleano = true; // false
        $array = ['datos', 2, 3.2, false];
        $array_asociativo = [
            'nombre' => 'Pepe',
            'telefono' => 753283723
        ];

    ?>

* Constantes:

.. code-block:: php
    :linenos:

    <?php
        // funcion define:
        define("CONSTANTE", "valor de la misma");
        echo CONSTANTE;

        // palabra reservada const:
        const constante = "valor de la constante";
        echo constante;
    ?>

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: php 
    :linenos:

    <?php 
        $sumar = 3 + 6;
        $restar = 7 * 9;
        $multiplicar = 11 * 6;
        $dividir = 13 / 20;
        $resto = 54 % 7;
    ?>

* Incremento y decremento:

.. code-block:: php 
    :linenos:

    <?php 
        $i++;
        ++$i;
        --$i;
        $i--;
    ?>

* Asignar operación:

.. code-block:: php 
    :linenos:

    <?php 
        // la variable debe tener un valor asignado:
        $resultado = 0

        $resultado += 12;
        $resultado -= 16;
        $resultado *= 19;
        $resultado /= 6;
    ?>

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

.. code-block:: php 
    :linenos:

    <?php
        $edad = 18;

        if($edad >= 18){
            echo "Eres mayor de edad";
        }
    ?>

* if / else:

.. code-block:: php 
    :linenos:

    <?php
        $edad = 15;

        if($edad >= 18){
            echo "Eres mayor de edad";
        }else{
            echo "Eres menor de edad";
        }
    ?>

* else-if:

.. code-block:: php 
    :linenos:

    <?php
        $edad = 45;

        if($edad >= 65){
            echo "Eres un anciano";
        }
        else if($edad >= 18){
            echo "Eres mayor de edad";
        }else{
            echo "Eres menor de edad";
        }
    ?>

* if alternativo:

.. code-block:: php 
    :linenos:

    <?php
        $edad = 73;

        if($edad >= 65):
            echo "Eres un anciano";
        else if($edad >= 18):
            echo "Eres mayor de edad";
        else:
            echo "Eres menor de edad";
        endif;
    ?>

.. note::
    Aparte de este if, existe for, foreach y while que comparten la misma forma de operar.

* Operador ternario:

.. code-block:: php 
    :linenos:

    <?php
        $edad = 35;
        $comprobarEdad = $edad >= 18 ? "Eres mayor de edad" : "Eres menor de edad";

        echo $comprobarEdad;
    ?>

Condicional Switch
******************
Estructura de un switch:

.. code-block:: php 
    :linenos:

    <?php
        $color = "verde";

        switch($color){
            case ("rojo"):
                echo "El color es rojo";
                break;
            case ("verde"):
                echo "El color es verde";
                break;
            case ("azul"):
                echo "El color es azul";
                break
            default:
                echo "No se reconoce el color";
        }
    ?>

Bucle for
*********

* for básico:

.. code-block:: php 
    :linenos:

    <?php
        for($i = 0; $i <= 10; $i++){
            echo "Repetición nº " . $i;
        }
    ?>

* foreach:

.. code-block:: php 
    :linenos:

    <?php
        $electrodomesticos = ["lavadora","nevera","microondas"];

        foreach($elecrodomesticos as $aparato){
            echo $aparato . "<br>";
        }
    ?>

* foreach clave / valor:

.. code-block:: php 
    :linenos:

    <?php
        $electrodomesticos = [
            "producto" => "Nevera",
            "modelo" => "FX27",
            "marca" => "Fagor",
            "precio" => 783.23
        ];

        foreach($elecrodomesticos as $key => $value){
            echo $key . ": " . $value . "<br>";
        }
    ?>

Bucle while
***********

* While sencillo:

.. code-block:: php 
    :linenos:

    <?php
        $num = 0;
        
        while($num < 10){
            echo "código de mensaje - " . $num;
            $num++;
        }
    ?>

* do-while:

.. code-block:: php 
    :linenos:

    <?php
        $num = 0;

        do{
            echo "código de mensaje - " . $num;
            $num++;            
        }  
        while($num < 10);
    ?>

Detener secuenda de script
**************************

.. code-block:: php
    :linenos:

    <?php 
        for($i = 0; $i <= 10; $i++){
            if($i == 5){
                echo "Ya has llegado a 5 y no más";
                die;
            }
        }
        echo "Esta frase no se mostrará";
    ?>

Tipos de datos avanzados
########################

Arrays
******

- Declaración tradicional:

.. code-block:: php 
    :linenos:

    <?php 
        $arreglo = ["cadena", 20, 18.27, false, ["otra cadena", 23, 18.77]];
    ?>

- Declaración con función array():

.. code-block:: php 
    :linenos:

    <?php 
        $arreglo = array("cadena", 20, 18.27, false);
    ?>

- Array multidimensional:

.. code-block:: php 
    :linenos:

    <?php 
        $operadores = array(
            ["OPERADOR", "DENOMINACIÓN"],
            ["suma", "+"],
            ["resta", "-"],
            ["multiplicación", "*"],
            ["división", "/"],
            ["resto", "%"]
        );

        // ejemplo recorrido array multidimensional:
        echo "<table border=1>";

        foreach($operadores as $key => $value){
            echo "<tr>";
            foreach($operadores[$key] as $operador){
                echo "<td>" . $operador . "</td>";
            }
            echo "</tr>";
        }

        echo "</table>"; 
    ?>

* Imprimir y asignar valores:

.. code-block:: php 
    :linenos:

    <?php 
        echo $arreglo[2];
        $arreglo[2] = "Veinte"; 
    ?>

Arrays asociativos
******************

- Declaración tradicional:

.. code-block:: php 
    :linenos:

    <?php 
        $asociaciones = [
            "clave" => "valor",
            "nombre" => "Paco",
            "edad" => 27,
            "peso" => 77.32,
            "cuota" => true
        ];
    ?>

- Declaración con función array():

.. code-block:: php 
    :linenos:

    <?php 
        $asociaciones = array(
            "clave" => "valor",
            "nombre" => "Paco",
            "edad" => 27,
            "peso" => 77.32,
            "cuota" => true
        );
    ?>

- Array multidimensional:

.. code-block:: php 
    :linenos:

    <?php 
        $asociaciones = [
            "clave" => "valor",
            "nombre" => "Paco",
            "edad" => 27,
            "peso" => 77.32,
            "cuota" => true,
            "subscripciones" => [
                "netflix" => true,
                "hbo" => false,
                "prime" => true
            ]
        ];

        foreach($asociaciones as $key => $value){
            echo "<ul>";
                if($key != "subscripciones"){
                    echo "<li>" . $key . ": " . $value . "</li>";
                }else{
                    echo "<li>Subscripciones: ";
                    foreach($asociaciones[$key] as $key => $value){
                        echo "<br>";
                        if($value){
                            echo "- " . $key . ": si";
                        }else{
                            echo "- " . $key . ": no";
                        }
                    }
                }
            echo "</ul>";
        }
    ?>

- Imprimir y asignar valores:

.. code-block:: php 
    :linenos:

    <?php 
        echo $asociaciones["nombre"];
        $arreglo["subscripciones"]["netflix"] = "subscrito"; 
    ?>

Control de errores
##################

.. code-block:: php
    :linenos:

    <?php
        try{
            throw new Exception(" No existe archivo de configuracion ");
        }catch(Exception $e){
            echo " Hubo un error" . $e->getMessage();
        }finally{
            echo "Cerrando BD";
        }
    ?>

Programación modular
####################

Funciones
*********

* Procedimienos:

.. code-block:: php 
    :linenos:

    <?php 
        function saludar(){
            echo "Hola persona";
        }

        saludar();
    ?>

* funciones:

.. code-block:: php 
    :linenos:

    <?php 
        function saludar(){
            return "Hola persona";
        }

        echo saludar();
    ?>

* uso de parámetros:

.. code-block:: php 
    :linenos:

    <?php 
        function saludar($nombre){
            return "Hola " . $nombre;
        }

        echo saludar("Pepe");
    ?>

* Funciones anónimas:

.. code-block:: php 
    :linenos:

    <?php
        $tuNombre = function($nombre){
            return "Hola ". $nombre;
        };

        echo $tuNombre("Pepe");
    ?>

* Ámbito global:

.. code-block:: php 
    :linenos:

    <?php
        $nombre = "alberto";

        $saludar = function(){
            global $nombre;
            return "¿Qué tal " . $nombre . "?";
        };

        echo $saludar();
    ?>

Programación orientada a objetos
################################

Los elementos de una clase se definen con ámbito **public**, **private** y **protected**. 
Adicionalmente se puede agregar el modificador **static** para poder acceder a los atributos y métodos sin crear un objeto.

Clases y objetos
****************

* Estructura clase:

.. code-block:: php 
    :linenos:

    <?php
        class Videoconsola {
            // atributos con ámbito obligatorio:
            public $modelo = "Mega Drive";
            public $marca = "Sega";

            // métodos con ambito public por defecto:
            function descripcion(){
                echo "Es una " . $this->marca . " " . $this->modelo;
            }
        }

        // crear objeto:
        $megaDrive = new Videoconsola;

        // recuperar atributo:
        echo $megaDrive->marca . "<br>";

        // recuperar métodos:
        $megaDrive->descripcion();
    ?>


* Constructor:

.. code-block:: php 
    :linenos:

    <?php
        class Videoconsola {
            public $modelo;
            public $marca;

            // constructor:
            function __construct($modelo, $marca){
                $this->modelo = $modelo;
                $this->marca = $marca;

                echo "Se ha creado el objeto";
                echo "<br>";
            }

            function descripcion(){
                echo "Es una " . $this->marca . " " . $this->modelo;
            }
        }

        // crear objeto con parámetros:
        $playStation = new Videoconsola("PlayStation", "Sony");

        $playStation->descripcion();

    ?>

* Get y Set:

.. code-block:: php 
    :linenos:

    <?php
        class Videoconsola {
            // métodos privados:
            private $modelo;
            private $marca;

            function __construct($modelo, $marca){
                $this->modelo = $modelo;
                $this->marca = $marca;

                echo "Se ha creado el objeto";
                echo "<br>";
            }

            // get:
            function getModelo(){
                return $this->modelo;
            }

            function getMarca(){
                return $this->marca;
            }

            // set:
            public function setModelo($valor){
                $this->modelo = $valor;
            }

            public function setMarca($valor){
                $this->marca = $valor;
            }

            function descripcion(){
                echo "Es una " . $this->marca . " " . $this->modelo;
            }
        }

        $playStation = new Videoconsola("PlayStation", "Sony");

        echo $playStation->getMarca() . "<br>";

        $playStation->setModelo("PlayStation 5");
        echo $playStation->getModelo();
    ?>

* Herencia:

.. code-block:: php 
    :linenos:

    <?php
        class Videoconsola {
            public $modelo;
            public $marca;

            function __construct($modelo, $marca){
                $this->modelo = $modelo;
                $this->marca = $marca;

                echo "Se ha creado el objeto";
                echo "<br>";
            }

            function descripcion(){
                echo "Es una " . $this->marca . " " . $this->modelo;
            }
        }

        class SuperNintendo extends Videoconsola{
            function __construct(){
                $this->modelo = "SNES";
                $this->marca = "Nintendo";
            }
        }

        $superNintendo = new SuperNintendo;

        $superNintendo->descripcion();
    ?>

Clases abstractas y resolución de ámbito
****************************************

- uso de clases no instanciables:

.. code-block:: php 
    :linenos:

    <?php
        abstract class Videoconsola {
            public static $modelo = "Super Nintendo";
            public $marca;

            function __construct($modelo, $marca){
                $this->modelo = $modelo;
                $this->marca = $marca;

                echo "Se ha creado el objeto";
                echo "<br>";
            }

            public static function juegos(){
                echo "La consola dispone de alrededor de 700 títulos";
            }

            // las funciones abstractas se deben usar obligatoriamente en la clase hija:
            abstract function precio();
        }

        // clase a partir de clase abstracta:
        class SuperNintendo extends Videoconsola{
            function __construct(){
                $this->modelo = "SNES";
                $this->marca = "Nintendo";
            }

            function precio(){
                echo "La consola cuesta 200 €";
            }
        }

        // uso de clase hija:
        $superNintendo = new SuperNintendo;
        echo $superNintendo->modelo;
        echo "<br>";
        $superNintendo->precio();
        echo "<br>";

        // resolución de ámbito:
        echo Videoconsola::$modelo;
        echo "<br>";
        Videoconsola::juegos();
    ?>

Interfaces
**********

.. code-block:: php 
    :linenos:

    <?php
        interface Videoconsola{
            function descripcion();
            function precio();
        }

        class NeoGeo implements Videoconsola{
            public $modelo;
            public $marca;
            public $precio;

            function __construct($modelo, $marca, $precio){
                $this->modelo = $modelo;
                $this->marca = $marca;
                $this->precio = $precio;
            }

            function descripcion(){
                echo "Es la consola " . $this->modelo . " de " . $this->marca . "<br>";
            }
            function precio(){
                echo "La consola cuesta: " . $this->precio . " €";
            }
        }

        $neoGeo = new NeoGeo("Neo Geo Pocket", "SNK", 149.99);
        $neoGeo->descripcion();
        $neoGeo->precio();
    ?>

Importar y exportar
###################

include y require
*****************

* Importar archivos php:

.. code-block:: php 
    :linenos:

    <?php
        // incluir archivo php:
        include 'ruta/archivo.php';

        // incluir obligatorio:
        require("ruta/archivo.php");

        // incluir y no repetir:
        include_once 'ruta/archivo.php';

        // incluir obligatorio y no repetir:
        require_once("ruta/archivo.php");
    ?>

Namespace
*********

* Exportar (videojuegos.php):

    .. code-block:: php 
        :linenos:

        <?php 

            namespace Videoconsola{

                // las constantes solo se pueden definir con const:
                const generacion = "5ª Generación";

                class Sistema {
                    public $modelo = "Mega Drive";
                    public $marca = "Sega";

                    function descripcion(){
                        echo "Es una " . $this->marca . " " . $this->modelo;
                    }
                }

                function tipo(){
                    echo "Es un sistema de tipo Videoconsola doméstica";
                }
            }

            namespace Arcade{

                // las constantes solo se pueden definir con const:
                const cabina = "Bartop";

                class Sistema {
                    public $modelo = "Naomi";
                    public $marca = "Sega";

                    function descripcion(){
                        echo "Es una placa" . $this->marca . " " . $this->modelo;
                    }
                }
            }
        ?>
    
    * Importar namespace (index.php):

    .. code-block:: php 
        :linenos:

        <?php
            include 'videojuegos.php';

            // cargar cada namespace:
            use const Videoconsola\generacion;
            use Videoconsola\Sistema as Videoconsola;
            use function Videoconsola\tipo as tipo;

            use Arcade\Sistema as Arcade;

            echo generacion . "<br>";
            $megaDrive = new Videoconsola;
            $megaDrive->descripcion();
            echo "<br>";
            tipo();
            echo "<br>";

            $naomi = new Arcade;
            $naomi->descripcion();
        ?>
        
.. note:: 
    Los namespace se pueden declarar sin el uso de llave.