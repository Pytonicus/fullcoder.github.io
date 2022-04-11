Comunicación Cliente / Servidor
===============================

.. image:: /logos/logo-php.png
    :scale: 15%
    :alt: Logo PHP
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Variables superglobales para manejo y procesamiento de peticiones en PHP 7.4

.. contents:: Índice

GET
###
    
En el caso de recibir los siguientes parámetros: http://localhost:8000/?marca=Sega&modelo=Dreamcast&lanzamiento=1999

* Su procesamiento sería:

.. code-block:: php
    :linenos:

    <?php
        // print_r para ver los valores del array:
        echo "<pre>";
        print_r($_GET);
        echo "</pre>";

        // Recuperar los valores del array $_GET:
        echo "<p>Marca: " . $_GET["marca"] . "</p>";
        echo "<p>Modelo: " . $_GET["modelo"] . "</p>";
        echo "<p>Lanzamiento: " . $_GET["lanzamiento"] . "</p>";
    ?>

POST 
####

.. code-block:: php
    :linenos:

    <?php
        echo "<pre>";
        print_r($_POST);
        echo "</pre>";

        // procesando POST:
        $marca = isset($_POST['marca']) ? $_POST['marca'] : "";
        $modelo = isset($_POST['modelo']) ? $_POST['modelo'] : "";
        $lanzamiento = isset($_POST['lanzamiento']) ? $_POST['lanzamiento'] : "";

    ?>

    <form method="POST">
        <input type="text" name="marca" placeholder="Introduce una marca">
        <br><br>
        <input type="text" name="modelo" placeholder="Introduce un modelo">
        <br><br>
        <input type="date" name="lanzamiento">
        <br><br>
        <input type="submit" value="Generar Consola">
        <br><br>
        <hr>
        <p>Marca: <?php echo $marca ?></p>
        <p>Modelo: <?php echo $modelo ?></p>
        <p>Lanzamiento: <?php echo $lanzamiento ?></p>
    </form>

FILES
#####

.. code-block:: php
    :linenos:

    <?php
        echo "<pre>";
        print_r($_FILES);
        echo "</pre>";
        

        if($_FILES){
            // Ruta almacenamiento:
            $ruta = "imagenes/" . $_FILES['archivo']['name'];

            // Cargar contenido de archivo temporal:
            $archivo = file_get_contents($_FILES['archivo']['tmp_name']);

            // Cargar validador de formato:
            $finfo = new finfo(FILEINFO_MIME_TYPE);

            // validar formato de archivo desde el buffer:
            $mimeType = $finfo->buffer($archivo);

            // ver resultado:
            echo $mimeType;

            // comprobar que el mime coincide con formato .jpg:
            if($mimeType == 'image/jpeg'){
                // subir archivo y comprobar que se ha realizado correctamente:
                if(move_uploaded_file($_FILES['archivo']['tmp_name'], $ruta)){
                    echo "Se ha guardado la imagen";
                }else{
                    echo "Ha habido un error al procesar la imagen";
                }
            }else{
                echo "Formato de archivo no reconocido";
            }
        }
    ?>

    <!-- Uso del Enctype para cargar archivos al servidor: -->
    <form method="POST" enctype="multipart/form-data">
        <input type="file" name="archivo">
        <input type="submit" value="Guardar imagen">
    </form>

Guardar Cookies en cliente
##########################

.. code-block:: php
    :linenos:

    <?php
        // Asignar cookie que caduca en un minuto:
        setcookie("secreto", "Probando cookies con FullCoder", time()+60);

        echo "<pre>";
        print_r($_COOKIE);
        echo "</pre>";
    ?>

Comprobar peticiones al servidor 
################################

.. code-block:: php
    :linenos:

    <?php
        // Recupera las peticiones actuales:
        echo "<pre>";
        print_r($_REQUEST);
        echo "</pre>";

        // Muestra todos los metodos disponibles:
        echo "<pre>";
        print_r($GLOBALS);
        echo "</pre>";
    ?>

Recuperar información del cliente
#################################

.. code-block:: php
    :linenos:

    <?php
        // Asignar cookie que caduca en un minuto:
        setcookie("secreto", "Probando cookies con FullCoder", time()+60);

        echo "<pre>";
        print_r($_SERVER);
        echo "</pre>";
    ?>

Trabajando con sesiones
#######################

.. code-block:: php
    :linenos:

    <?php
        // iniciar la sesión recupera los archivos guardados en $_SESSION:
        session_start();

        echo "<pre>";
        print_r($_SESSION);
        echo "</pre>";
        // guardar datos de la sesión que se mantendrán hasta que esta se destruya:
        if(isset($_POST['usuario'])){
            $_SESSION['usuario'] = $_POST['usuario'];
            $_SESSION['clave'] = $_POST['clave'];
        }

        if($_SESSION['usuario'] == "guillermo" && $_SESSION['clave'] == "clave"){
            echo "<p>Bienvenido: " . $_SESSION['usuario'] . "</p>";
        }else{
            echo "<p>Debe iniciar sesión.</p>";
        }

        // cerrar o destruir la sesión:
        if(isset($_POST['cerrar'])){
            session_destroy();
        }
    ?> 
 
    <form method="POST">
        <input type="text" name="usuario" placeholder="ingresa un usuario">
        <input type="password" name="clave" placeholder="ingresa una clave">
        <input type="submit" value="iniciar sesión">
    </form>

    <form method="POST">
        <input type="hidden" name="cerrar">
        <input type="submit" value="cerrar sesión">
    </form>
 

