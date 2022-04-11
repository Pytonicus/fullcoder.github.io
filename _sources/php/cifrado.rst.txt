Codificación y Hash
===================

.. image:: /logos/logo-php.png
    :scale: 15%
    :alt: Logo PHP
    :align: center

.. |date| date::
.. |time| date:: %H:%M

  
Cifrado de datos con funciones específicas de PHP 7.4

.. contents:: Índice
  
Codificación
############

.. code-block:: php 
    :linenos:
 
    <?php

        define('METODO','AES-256-CBC'); //En esta constante guardamos el método de encriptación
        define('CLAVE_SECRETA','$BE@ppp80'); //Aquí se guardará la clave secreta.
        define('SUBCLAVE_SECRETA','99326425'); //Y aquí una clave adicional.

        function encriptar($cadena){

            $salida = ""; 
            $prefijo = hash('sha256', CLAVE_SECRETA); //vamos a encriptar el prefijo de la clave con sha256.
            $sufijo = substr(hash('sha256', SUBCLAVE_SECRETA), 0, 16); //y ahora vamos a hacer lo mismo con el sufijo añadiendole el método substr().

            $salida = openssl_encrypt($cadena, METODO, $prefijo, 0, $sufijo); // Ahora vamos a escribir en la variable de salida el resultado encriptado de la cadena entrante combinada con el metodo de encriptación, el prefijo, valor 0 y el sufijo.
            $salida = base64_encode($salida); //finalmente añadimos el metodo de encriptado en base64 para asegurarla más.

            return $salida; //devolvemos el valor de salida.

        }

        $plain_txt = "clave";
        echo "clave sin encriptar: " . $plain_txt;
        echo "<br>";
        echo "clave ya encriptada: " . encriptar($plain_txt); //Ahora aquí vamos a utilizar nuestra función de encriptado con la variable que contiene la clave.

    ?>

* Método para descodificar:

.. code-block:: php
    :linenos:

    <?php

        define('METODO','AES-256-CBC'); //En esta constante guardamos el método de encriptación
        define('CLAVE_SECRETA','$BE@ppp80'); //Aquí se guardará la clave secreta.
        define('SUBCLAVE_SECRETA','99326425'); //Y aquí una clave adicional.

        function decrypt($cadena){

            $prefijo = hash('sha256', CLAVE_SECRETA);
            $sufijo = substr(hash('sha256', SUBCLAVE_SECRETA), 0, 16);
            //hasta aqui todo igual, ahora cambiamos encrypt por decrypt e introducimos la cadena desencriptandola con base64_decode y le aplicamos las claves necesarias para desencriptarlo todo junto de nuevo y devolver el valor de salida correspondiente.
            $salida = openssl_decrypt(base64_decode($cadena), METODO, $prefijo, 0, $sufijo);
            return $salida;
        }

        $clave = "cDQwMTBZbmkwS3BwZm9lR1BtYlZJQT09";

        echo "La clave encriptada es: " . $clave;
        echo "<br>";
        echo "La clave desencriptada es: " . decrypt($clave);

    ?>

Generar un Hash con MD5
#######################

.. code-block:: php 
    :linenos:

    <?php

        $clave = isset($_GET['password']) ? $_GET['password'] : '';

        $salt = '$BE@pppp190716LS%';

        echo "su clave es: " . md5($salt . $clave);

    ?>

Ingresamos la url: http://localhost:8000/?password=coca-cola para ver el hash generado.

* Código para descifrar el hash:

.. code-block:: php 
    :linenos:

    <?php
        $clave = isset($_GET['password']) ? $_GET['password'] : '';

        $salt = '$BE@pppp190716LS%';

        if(md5($salt . $clave) == '116103ad09bf77e6e771c08dc3f63967'){
            echo 'Contraseña correcta';
        }
        else{
            echo 'contraseña incorrecta';
        }
    ?>

Ingresamos la url: http://localhost:8000/?password=coca-cola para descifrar el hash.
