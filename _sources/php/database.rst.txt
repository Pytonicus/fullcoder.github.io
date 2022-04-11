Manipulación de base de datos
=============================

.. image:: /logos/logo-php.png
    :scale: 15%
    :alt: Logo PHP
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Manipulación de base de datos con PDO en PHP 7.4

.. contents:: Índice
 
Conexión SQLITE 3
#################
 
Pasos iniciales:
 
* Primero tenemos que instalar sqlite3 en nuestro sistema: ``sudo apt install php7.4-sqlite3``
* Luego localizamos el archivo **php.ini** que suele estar en **/etc/php/7.4/ y dentro de las carpetas **apache2** y **cli** encontraremos estos archivos.
* Editamos y buscamos las líneas que ponen ``;extension=pdo_sqlite`` y ``;extension=sqlite`` si tienen un **;** lo quitamos para habilitarlas.

* Conectar a una base de datos SQLite 3:

.. code-block:: php 
    :linenos:
 
    <?php 
        try{
            // realizamos la conexion con el motor sqlite y apuntamos directamente a la base de datos:
            $db = new PDO('sqlite:datos.sqlite');
            $db->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
            $db->setAttribute(PDO::ATTR_DEFAULT_FETCH_MODE, PDO::FETCH_OBJ);

            echo "Conexión realizada con éxito";
        }catch(Exception $e){
            echo "Error de conexión: " . $e->getMessage();
        }
        // para cerrar la conexión:
        $con = null;
    ?>

Conexión MySQL
##############

Pasos iniciales:

* Primero tenemos que instalar sqlite3 en nuestro sistema: ``sudo apt install php7.4-mysql``
* Luego localizamos el archivo **php.ini** que suele estar en **/etc/php/7.4/ y dentro de las carpetas **apache2** y **cli** encontraremos estos archivos.
* Editamos y buscamos las líneas que ponen ``;extension=pdo_mysql`` si tienen un **;** lo quitamos para habilitarlas.

.. code-block:: php 
    :linenos:

    <?php 
        // preparamos los datos del servidor:
        $servidor = "localhost";
        $usuario = "guillermo";
        $clave = "guillermo";
        try{
            // preparamos la conexión eligiendo el motor mysql:
            $conn = new PDO("mysql:host=$servidor;dbname=prueba", $usuario, $clave);
            // realizamos la conexión:
            $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
            echo "Conexión realizada con éxito";
        }catch(Exception $e){
            echo "Error de conexión: " . $e->getMessage();
        }
        // para cerrar la conexión:
        $conn = null;
    ?>  

Conexión SQL SERVER
###################
Para realizar la conexión a SQL SERVER:
* Instalamos el driver ODBC: https://www.microsoft.com/en-us/download/details.aspx?id=36434
* Descargamos el controlador para PHP: https://docs.microsoft.com/en-us/sql/connect/php/download-drivers-php-sql-server?view=sql-server-ver15#download
* Se extraen las librerías .dll en la carpeta ext/ del directorio php/ que tenganmos.
* Se edita php.ini para que reconozca las librerías y se reinicia el servidor:

.. code-block:: 

    extension=php_sqlsrv_74_ts_x64.dll
    extension=php_sqlsrv_74_nts_x64.dll
    extension=php_pdo_sqlsrv_74_nts_x64.dll
    extension=php_pdo_sqlsrv_74_ts_x64.dll

* crear un usuario que pueda hacer login en el servidor DDBB y permitr el acceso desde SQL Server en lugar de Windows Authorization.
* Luego podemos crear el conector:

.. code-block:: php 
    :linenos:

    <?php 
        // preparamos los datos del servidor:
        $servidor = "NOMBREEQUIPO"; // no vale localhost.
        $usuario = "guillermo";
        $clave = "guillermo";
        try{
            // preparamos la conexión eligiendo el motor mysql:
            $conn = new PDO("sqlsrv:server=$servidor;database=prueba", $usuario, $clave);
            // realizamos la conexión:
            $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
            echo "Conexión realizada con éxito";
        }catch(Exception $e){
            echo "Error de conexión: " . $e->getMessage();
        }

        // para cerrar la conexión:
        $conn = null;
    ?>  
 

 
Operaciones CRUD
################

Crear base de datos
*******************

.. code-block:: php 
    :linenos:

    <?php 
        $servidor = "localhost";
        $usuario = "guillermo";
        $clave = "guillermo";
        // ignoramos elegir la base de datos al preparar conexión::
        $conn = new PDO("mysql:host=$servidor", $usuario, $clave);
        // realizamos la conexión:
        $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        // preparamos la consulta:
        $sql = "CREATE DATABASE pruebaSQL";
        // realizamos la consulta:
        $conn->exec($sql);
        
        echo "Base de datos creada con éxito";
        $conn = null;
    ?>


Crear una tabla
***************

.. code-block:: php 
    :linenos:

    <?php 
        $servidor = "localhost";
        $usuario = "guillermo";
        $clave = "guillermo";
        $base = "prueba";

        $conn = new PDO("mysql:host=$servidor;dbname=$base", $usuario, $clave);

        $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $sql = "CREATE TABLE agenda(
            id INT(10) AUTO_INCREMENT PRIMARY KEY,
            nombre VARCHAR(30) NOT NULL,
            edad INT(10) NOT NULL
            )";

        $conn->exec($sql);
        
        echo "Tabla creada con éxito";
        $conn = null;
    ?>  

Insertar registros
******************

.. code-block:: php 
    :linenos:

    <?php 
        $servidor = "localhost";
        $usuario = "guillermo";
        $clave = "guillermo";
        $base = "prueba";

        $conn = new PDO("mysql:host=$servidor;dbname=$base", $usuario, $clave);

        $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);

        $sql = "INSERT INTO agenda (nombre, edad) values ('Alfredo', 30)";

        $conn->exec($sql);
        
        echo "Inserción realizada con éxito";
        $conn = null;
    ?>  

Inserciones y actualizaciones múltiples
***************************************

.. code-block:: php 
    :linenos:

    <?php 
        $servidor = "localhost";
        $usuario = "guillermo";
        $clave = "guillermo";
        $base = "prueba";

        $conn = new PDO("mysql:host=$servidor;dbname=$base", $usuario, $clave);

        $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        // Preparar consulta para separar parametros:
        $sql = $conn->prepare("INSERT INTO agenda (nombre, edad) VALUES (:nombre, :edad)");
        // preparar parametros:
        $sql->bindParam(':nombre', $nombre);
        $sql->bindParam(':edad', $edad);

        // insertar mas de un registro a la vez:
        $nombre = "Antonio";
        $edad = 38;
        $sql->execute();

        $nombre = "Eustaquia";
        $edad = 73;
        $sql->execute();
        
        echo "Inserciones realizadas correctamente";
        $conn = null;
    ?>  

.. attention:: 
    los bindParams se pueden usar en operaciones INSERT y en operaciones UPDATE


Leer registros
**************

.. code-block:: php 
    :linenos:

    <?php 
        $servidor = "localhost";
        $usuario = "guillermo";
        $clave = "guillermo";
        $base = "prueba";

        $conn = new PDO("mysql:host=$servidor;dbname=$base", $usuario, $clave);

        $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        // Preparar consulta:
        $sql = $conn->query("SELECT * FROM agenda");
        // Ejecutar consulta, ,fetch para registros individuales y fetchAll para multiples:
        $sql = $sql->fetchAll(PDO::FETCH_ASSOC); // usar el parametro FETCH_ASSOC imprime de forma limpia.
        // Recorrer todos los datos:        
        foreach($sql as $data){
            echo "- " . $data['nombre'] . "\n";
        }
        
        $conn = null;
    ?>  

Borrar registros
****************

.. code-block:: php 
    :linenos:

    <?php 
        $servidor = "localhost";
        $usuario = "guillermo";
        $clave = "guillermo";
        $base = "prueba";

        $conn = new PDO("mysql:host=$servidor;dbname=$base", $usuario, $clave);

        $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        // Preparar consulta:
        $sql = "DELETE FROM agenda WHERE id=1";
        // ejecutar consulta:
        $conn->exec($sql);

        echo "Registro eliminado";

        $con = null;
    ?>  

Actualizar registros
********************

.. code-block:: php 
    :linenos:

    <?php 
        $servidor = "localhost";
        $usuario = "guillermo";
        $clave = "guillermo";
        $base = "prueba";

        $conn = new PDO("mysql:host=$servidor;dbname=$base", $usuario, $clave);

        $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        // Preparar consulta:
        $sql = "UPDATE agenda SET nombre='Elvira', edad=32 WHERE id=2";
        // preparar estado:
        $stmt = $conn->prepare($sql);    
        // ejecutar consulta:
        $stmt->execute();

        echo "Registro actualizado";

        $con = null;
    ?>  