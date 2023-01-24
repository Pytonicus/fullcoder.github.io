PostgreSQL
==========

.. image:: /logos/basic64-logo.png
    :scale: 100%
    :alt: Logo PostgreSQL
    :align: center

.. |date| date::
.. |time| date:: %H:%M
 

Funcionamiento de PostgreSQL
  
.. contents:: Índice

Primeros pasos   
##############

Instalación de PostgreSQL 
*************************

- Para instalar PostgreSQL desde cualquier sistema operativo es recomendable seguir los pasos de su web oficial: https://www.postgresql.org/download/
- En Linux tendrás que descargar Pgadmin 4 desde su sitio web: https://www.pgadmin.org/download/
- En un terminal podemos comprobar que se ha instalado ejecutando: ``psql --version``

.. attention::
    Es posible que al instalar PGAdmin4 no este configurada la conexión, es crucial crear una contraseña para configurar la conexión desde la consola **psql** para el usuario **postgres** o sino no podremos configurar la conexión externa.

Conceptos básicos
*****************

- Cluster: Áreas de almacenamiento con una o más bases de datos.
- Bases de datos: Colecciones de datos (igual que MySQL)
- Esquemas: Colecciones de tablas en bases de datos. 
- Tablespaces: Almacenamiento en disco desde punto de vista entre tabla e índices.
- Rol: Entidades que pueden ser dueñas de bases de datos o permisos (Usuarios y Grupos)
- Tabla: Colecciones de datos relacionales.
- Vista: Sentencias SQL que afectan a una o varias tablas.
- Disparador (Trigger): Disparadores de eventos que se activan cuando se actua sobre alguna tabla.

Seguridad 
*********

PostgreSQL cuenta con opciones para limitar el acceso a diferentes tipos de usuario en cada cluster, el tipo de ip permitida, el host si es local o externo, el método, y las direcciones permitidas.


Acceso a Postgres desde terminal
********************************

En linux:

- Abrir terminal y cambiar al usuario postgres: ``sudo -i -u postgres``
- Con el usuario postgres ya se puede ejecutar en terminal: ``psql``
- si queremos listar bases de datos: ``\l``
- Para poder usar pgadmin debemos cambiar la contraseña del usuario **postgres**, en el cli **psql** ejecutamos la sentencia:

.. code-block:: sql 
    :linenos:

    ALTER USER postgres WITH ENCRYPTED password '1234';

Sentencias SQL Crear 
####################

Crear base de datos
*******************

.. code-block:: Postgres
    :linenos:

    CREATE DATABASE coleccion
        WITH
        OWNER = postgres
        ENCODING = 'UTF8'
        CONNECTION LIMIT = -1
        IS_TEMPLATE = False;

.. note::
    el campo CONNECTION LIMIT con -1 está indicando que tiene conexiones ilimitadas.

Crear Schema
************

.. code-block:: Postgres
    :linenos:

    CREATE SCHEMA coleccion;

Crear dominio
*************

los dominios se utilizan para establecer un diseño de entrada para un dato en particular. En este caso los campos id de la base de datos colección:

.. code-block:: postgres
    :linenos:

    CREATE DOMAIN coleccion.id AS CHAR(6) NOT NULL
	    CHECK(VALUE ~ '^[G]{1}[-]{1}\d{4}$'); -- Ejemplo: G-0001

Crear tabla 
***********

- Crear tabla sencilla:

.. code-block:: postgres
    :linenos:

    CREATE TABLE coleccion.consola (
        id coleccion.id, -- el id le asignamos el dominio creado
        marca VARCHAR(50) NOT NULL,
        modelo VARCHAR(50) NOT NULL,
        lanzamiento DATE,
        PRIMARY KEY (id)
    );

- Crear tabla con clave foranea:

.. code-block:: postgres
    :linenos:

    CREATE TABLE coleccion.videojuego (
        id coleccion.id, -- el id le asignamos el dominio creado
        titulo VARCHAR(50) NOT NULL,
        id_sistema coleccion.id, -- y a la clave foranea también
        lanzamiento DATE,
        PRIMARY KEY (id),
        FOREIGN KEY (id_sistema) REFERENCES coleccion.consola (id)
        ON UPDATE CASCADE ON DELETE CASCADE -- actualizar datos en forma de cascada
    );

Sentencias SQL Alterar
######################

Alterar columnas  
****************

.. code-block:: postgres
    :linenos:

    -- añadir columna:
    ALTER TABLE coleccion.videojuego ADD COLUMN formato VARCHAR(50);

    -- eliminar columna:
    ALTER TABLE coleccion.videojuego DROP COLUMN lanzamiento;

    -- cambiar formato de columna:
    ALTER TABLE coleccion.videojuego ALTER COLUMN formato TYPE CHAR(50);

    -- renombrar columna:
    ALTER TABLE coleccion.videojuego RENAME COLUMN formato TO soporte;

Alterar tablas
**************

.. code-block:: postgres
    :linenos:
    
    ALTER TABLE coleccion.videojuego RENAME TO juego;


Sentencia SQL Insertar 
######################

Insertar registro
*****************

.. code-block:: postgres
    :linenos:

    INSERT INTO coleccion.consola VALUES ('G-0001', 'Sony', 'Playstation', '1994-12-03');

Insertar varios registros
*************************

.. code-block:: postgres
    :linenos:

    INSERT INTO coleccion.consola VALUES 
        ('G-0002', 'Sony', 'Playstation 2', '2000-03-04'),
        ('G-0003', 'Sony', 'Playstation 3', '2006-11-11'),
        ('G-0004', 'Sony', 'Playstation 4', '2013-11-15');

Insertar registro con clave foranea
***********************************

.. code-block:: postgres
    :linenos:

                                                                    -- se agrega el id que corresponde al dato relacionado con la otra tabla.
    INSERT INTO coleccion.juego VALUES ('G-0001', 'Final Fantasy VIII','G-0001','1999-02-11');


Sentencias SQL Actualizar
#########################

Actualizar columna completa 
***************************

.. code-block:: postgres
    :linenos:

    -- asi se actualizarán todos los datos de la columna lanzamiento:            
    UPDATE coleccion.juego SET lanzamiento = '2022-10-10';

Actualizar columna de uno o varios registros por condición  
**********************************************************

.. code-block:: postgres
    :linenos:

    UPDATE coleccion.juego SET titulo = 'Final Fantasy 8' WHERE id = 'G-0001';

Actualizar columna de uno o varios registros por varias condiciones   
*******************************************************************

.. code-block:: postgres
    :linenos:

    -- actualizar aquellos registros que cumplan dos o mas condiciones:
    UPDATE coleccion.consola SET lanzamiento = '1990-01-01' WHERE marca = 'Sony' AND modelo = 'Playstation 2';

    -- actualizar aquellos registros que cumplan al menos una de las siguientes condiciones:
    UPDATE coleccion.consola SET lanzamiento = '1990-01-01' WHERE marca = 'Sony' OR modelo = 'Playstation 2'; 

Sentencias SQL Eliminar 
#######################

Eliminar Schema
***************

.. code-block:: Postgres
    :linenos:

    DROP SCHEMA public;

Eliminar Tabla 
**************

.. code-block:: postgres 
    :linenos:

    DROP TABLE coleccion.juego;


Eliminar columna completa 
*************************

.. code-block:: postgres
    :linenos:

    -- asi se Eliminarán todos los datos:            
    DELETE FROM coleccion.juego;

Eliminar columna de uno o varios registros por condición  
********************************************************

.. code-block:: postgres
    :linenos:

    DELETE FROM coleccion.juego WHERE titulo = 'Final Fantasy 8';

Eliminar columna de uno o varios registros por varias condiciones   
*****************************************************************

.. code-block:: postgres
    :linenos:

    -- eliminar aquellos registros que cumplan dos o mas condiciones:
    DELETE FROM coleccion.consola WHERE lanzamiento = '1990-01-01' AND modelo = 'Playstation 2';

    -- eliminar aquellos registros que cumplan al menos una de las siguientes condiciones:
    DELETE FROM coleccion.consola WHERE marca = 'Sony' OR modelo = 'Playstation 2'; 


Condiciones SQL 
###############

Las instrucciones SQL se utilizan para filtrar y organizar las consultas.

Instrucción WHERE 
*****************

.. code-block:: postgres 
    :linenos:

    -- Seleccionar elementos añadiendo una condición where:
    SELECT * FROM coleccion.juego WHERE titulo='Final Fantasy VIII';


Instrucciones AND y OR  
**********************

.. code-block:: postgres 
    :linenos:

    -- Con AND indicamos que se deben cumplir dos o mas campos para los resultados:
    SELECT * FROM coleccion.consola WHERE marca='Sony' AND modelo='Playstation';

    -- Con OR indicamos que se debe cumplir al menos uno de los siguientes campos:
    SELECT * FROM coleccion.consola WHERE marca='Sony' OR modelo='Playstation 2';

    -- Con IN indicamos que se recuperen varios registros que cumplan con una columna:
    SELECT * FROM coleccion.consola WHERE modelo IN ('Playstation', 'Playstation 2');

    -- Con NOT IN indicamos que se recuperen todos los registros que no cumplan con una columna:
    SELECT * FROM coleccion.consola WHERE modelo NOT IN ('Playstation', 'Playstation 2');

    -- Con LIKE indicamos que recupere aquellos valores que contengan parte de un registro:
    SELECT * FROM coleccion.consola WHERE modelo LIKE '%Playstation%';

    -- Con BETWEEN indicamos un rango de valores como fechas o registros inclusivos:
    SELECT * FROM coleccion.consola WHERE id BETWEEN 'G-0002' AND 'G-0003';

    -- Con <, <=, >, >= podemos buscar registros mayores o iguales a fechas o numeros:
    SELECT * FROM coleccion.consola WHERE id >= 'G-0002';

    -- Con <> podemos buscar registros distintos a un valor concreto al igual que NOT IN:
    SELECT * FROM coleccion.consola WHERE id <> 'G-0002';


Instrucción AS  
**************

.. code-block:: sql 
    :linenos:

    -- AS define un alias para la columna:
    SELECT marca AS compañia, modelo AS consola FROM coleccion.consola;


Instrucción COUNT  
*****************

.. code-block:: sql 
    :linenos:

    -- Contar todos registros que hay en la tabla:
    SELECT COUNT(*) AS cantidad_consolas FROM coleccion.consola;

    -- Contar los resultados que cumplan una condición:
    SELECT COUNT(*) AS playstation_3 FROM coleccion.consola WHERE modelo = 'Playstation 3';

Instrucción SUM 
***************

- Primero vamos a crear una nueva columna con valores numéricos:

.. code-block:: sql 
    :linenos:

    -- Añadimos una columnas ventas:
    ALTER TABLE coleccion.consola ADD COLUMN ventas INTEGER;
    -- Poblamos la tabla:
    UPDATE coleccion.consola SET ventas = 1654654 WHERE id='G-0001';
    UPDATE coleccion.consola SET ventas = 1654655 WHERE id='G-0002';
    UPDATE coleccion.consola SET ventas = 1655522 WHERE id='G-0003';
    UPDATE coleccion.consola SET ventas = 16546355 WHERE id='G-0004';

- Ahora hacemos la suma de toda la columna:

.. code-block:: sql 
    :linenos:

    -- sumar ventas totales:
    SELECT SUM(ventas) AS ventas_totales FROM coleccion.consola;

.. note::
    Si el valor numerico a sumar es de tipo varchar podemos cambiarlo a entero o decimal haciendo un CAST: ``SELECT SUM(CAST(ventas AS INT)) AS ventas_totales FROM coleccion.consola;``

Instrucción MAX 
***************

.. code-block:: sql 
    :linenos:

    -- sacar el valor máximo:
    SELECT MAX(ventas) FROM coleccion.consola;

Instrucción MIN 
***************

.. code-block:: sql 
    :linenos:

    -- sacar el valor minimo:
    SELECT MIN(ventas) FROM coleccion.consola;

Instrucción AVG  
***************

.. code-block:: sql 
    :linenos:

    -- sacar el promedio:
    SELECT AVG(ventas) AS promedio FROM coleccion.consola;


Instrucción ORDER BY 
********************

.. code-block:: sql 
    :linenos:

    -- ordenar resultados de forma ascendente (ASC) o descendente (DESC):
    SELECT marca, modelo, ventas FROM coleccion.consola ORDER BY ventas DESC;

Instrucción HAVING 
******************

.. code-block:: sql 
    :linenos:

Instrucción DISTINCT 
********************

.. code-block:: sql 
    :linenos:

    -- DISTINCT muestra resultados no repetidos de una columna:
    SELECT DISTINCT marca FROM coleccion.consola;

Instrucción LIMIT  
*****************

.. code-block:: sql 
    :linenos:

     la cantidad de resultados a mostrar:
    SELECT * FROM coleccion.consola LIMIT 2; -- con order by podemos ordenar los resultados y mostrar otros


Consultas relacionales
######################

- Vamos a añadir unos registros:

.. code-block:: sql 
    :linenos:

    -- insertamos unos registros nuevos con claves foraneas (si no hay valores relacionados entre tablas no se mostrará nada)
    INSERT INTO coleccion.juego VALUES 
        ('G-0100', 'Final Fantasy VIII','G-0001','1999-02-11'),
        ('G-0101', 'Final Fantasy IX','G-0001','1999-02-11'),
        ('G-0102', 'Final Fantasy X','G-0002','1999-02-11');


Instrucción INNER JOIN
**********************

.. code-block:: sql 
    :linenos:

    SELECT * FROM coleccion.juego 
    INNER JOIN coleccion.consola -- seleccionamos la tabla a relacionar
    ON juego.id_sistema = consola.id; -- relacionamos la clave foranea de nuestra tabla con la clave primaria de la otra tabla

.. note::
    se pueden usar instrucciones condicionales como **WHERE** entre otras del anterior apartado.

.. note::
    también se pueden anidar sentencias **INNER JOIN** relacionando tablas con las ya presentes.

Instrucción LEFT JOIN
*********************

TODO: REVISAR LEFT JOIN

.. code-block:: sql 
    :linenos:

    SELECT * FROM coleccion.juego 
    LEFT JOIN coleccion.consola -- MOSTRARÁ los datos de la tabla join aunque tenga algun valor null  
    ON juego.id_sistema = consola.id; 

Instrucción RIGHT JOIN
**********************

.. code-block:: sql 
    :linenos:

    SELECT * FROM coleccion.juego 
    RIGHT JOIN coleccion.consola -- MOSTRARÁ los datos de la tabla seleccionada aunque no tenga relación con la tabla join 
    ON juego.id_sistema = consola.id; 

Vistas 
######

Las vistas sirven para mostrar datos de varias tablas en una especie de tabla virtual.

- Crear vista:

.. code-block:: sql 
    :linenos:

    -- CREAR UNA VISTA:
    CREATE VIEW coleccion.juegos_psone AS 
    SELECT * FROM coleccion.juego WHERE id_sistema = 'G-0001';

- Utilizar vista:

.. code-block:: sql 
    :linenos:

    -- ejecutar consulta:
    SELECT * FROM coleccion.juegos_psone;

- Borrar vista:

.. code-block:: sql 
    :linenos:

    -- eliminar vista:
    DROP VIEW coleccion.juegos_psone;

- Renombrar vista:

.. code-block:: sql 
    :linenos:

    -- renombrar una vista:
    ALTER VIEW coleccion.juegos_psone RENAME TO psone_list;

Subconsultas
############

.. code-block:: sql 
    :linenos:

    SELECT * FROM coleccion.juego 
    WHERE id_sistema IN ( -- hacemos una segunda consulta utilizando el campo que coincide con la relación en este caso id_sistema = id:
        SELECT id FROM coleccion.consola 
        WHERE id BETWEEN 'G-0002' AND 'G-0004'
    );

Funciones
#########

LEFT 
****

.. code-block:: sql 
    :linenos:

    -- Con left recuperamos de izquierda a derecha un numero de elementos:
    SELECT LEFT(modelo, 4) FROM coleccion.consola;


RIGHT  
*****

.. code-block:: sql 
    :linenos:

    -- Con left recuperamos de derecha a izquierda un numero de elementos:
    SELECT RIGHT(modelo, 4) FROM coleccion.consola;


CONCAT   
******

.. code-block:: sql 
    :linenos:

    -- concat une mediante comas cadenas de texto:
    SELECT CONCAT(marca, ' ', modelo) FROM coleccion.consola;

LENGHT   
******

.. code-block:: sql 
    :linenos:

    -- cuenta los caracteres de celda:
    SELECT LENGTH(modelo) FROM coleccion.consola;

REPLACE   
*******

.. code-block:: sql 
    :linenos:

    -- reemplaza caracteres recibiendo la columna, el o los caracteres a reemplazar y el valor nuevo:
    SELECT REPLACE(modelo, 'Playstation', 'ps') FROM coleccion.consola;

CAST    
****

.. code-block:: sql 
    :linenos:

    -- convierte un dato a otro tipo:
    SELECT CAST(CURRENT_TIME AS VARCHAR(50));


NOW    
***

.. code-block:: sql 
    :linenos:

    -- muestra la hora actual:
    SELECT NOW();

- añadir un intervalo de tiempo:


.. code-block:: sql 
    :linenos:

    -- muestra la hora actual:
    SELECT (NOW() + INTERVAL '1 DAY') AS mañana;

.. note::
    los intervalos podemos manejarlos en minutos, horas, días, semanas y años.

CURRENT_TIME    
************

.. code-block:: sql 
    :linenos:

    -- devuelve la hora exacta:
    SELECT CURRENT_TIME;

CURRENT_DATE    
************

.. code-block:: sql 
    :linenos:

    -- devuelve la fecha actual:
    SELECT CURRENT_DATE;

TIMEOFDAY    
*********

.. code-block:: sql 
    :linenos:

     -- Muestra la fecha en formato completo:
    SELECT TIMEOFDAY();

DATE_PART   
*********

.. code-block:: sql 
    :linenos:

    -- CON DATE_PART podemos comparar la diferencia entre dos fechas:
    SELECT DATE_PART('year', '2015-01-06'::date) - DATE_PART('year', '2002-02-05'::date) AS diferencia_año;

.. note::
    también se puede sacar la diferencia entre días, semanas, meses y años.


Transacciones
#############

Para iniciar las transacciones accedemos a la consola de PSQL:

- Seleccionamos la base de datos: ``\c coleccion`` 
- Seleccionamos el esquema para ver todas las tablas y vistas: ``SET SEARCH_PATH TO coleccion;`` 
- Y ahora podemos listar las tablas: ``\d``

Commit   
******

- Comenzar una transacción en SQL: ``BEGIN TRANSACTION``
- Insertar un registro (este se quedará temporalmente guardado para el usuario que esta operando pero no lo verán el resto hasta que se comitee): 

.. code-block:: sql 
    :linenos:
    
    INSERT INTO coleccion.consola VALUES ('G-0051', 'Sony', 'PSP', '1994-12-03');

- confirmar cambios: ``COMMIT;``

Rollback   
********

- Comenzar una transacción en SQL: ``BEGIN TRANSACTION;``
- Insertar un registro (este se quedará temporalmente guardado para el usuario que esta operando pero no lo verán el resto hasta que se comitee): 

.. code-block:: sql 
    :linenos:
    
    INSERT INTO coleccion.consola VALUES ('G-0052', 'Sony', 'PSVITA', '1994-12-03');

- Comprobamos que esta cargado en la tabla: ``SELECT * FROM consola;``
- eliminar cambios: ``ROLLBACK;``
- Confirmamos que el temporal ya se ha eliminado: ``SELECT * FROM consola;``

.. note::
    Este tipo de operación es muy útil cuando guardamos datos en tablas relacionadas y una de las operaciones no ha funcionado correctamente. En ese caso podemos hace rollback y borrar todo lo que ya no sirve.

Roles de usuario 
################

En PostgreSQL se crea por defecto el superusuario postgres. Sin embargo podemos crear diferentes usuarios los cuales acceden y trabajan con la base de datos. 
Por otro lado, los roles agregan a estos usuarios y definene los permisos sobre esquemas y objetos de la estructura.

De modo que los privilegios se asignan a los roles y los roles se asignan a los usuarios.

La jerarquía para los permisos es la seguiente: Primero tener permiso para acceder a la base de datos, luego va el permiso a los esquemas y por último a los objetos de la base de datos.

Luego existen dos tipos de privilegios:

- privilegios del sistema: los superusuarios (por defecto "postgres"). (CREATEDB, CREATEROLE, CREATEUSER, INHERIT, LOGIN)
- privilegios de objeto: los privilegios sobre objetos como la base de datos o los esquemas. (SELECT, INSERT, DELETE, UPDATE, TRUNCATE, USAGE, EXECUTE, CREATE ON)

Crear un rol 
************

- Crear un rol de superusuario:

.. code-block:: sql 
    :linenos:

    -- crear rol de superusuario:
    CREATE ROLE super WITH SUPERUSER;

    -- otorgar permiso de uso a un esquema:
    GRANT USAGE ON SCHEMA coleccion TO super;

    -- otorgar todos los privilegios a todas las tablas:
    GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA coleccion TO super WITH GRANT OPTION;

    -- crear usuario administrador con el rol superusuario:
    CREATE USER admin WITH PASSWORD '1234' IN ROLE super;

- Crear un rol para un usuario limitado:

.. code-block:: sql 
    :linenos:

    -- crear rol de usuario básico:
    CREATE ROLE regular_user WITH SUPERUSER;

    -- otorgar permiso de uso a un esquema:
    GRANT USAGE ON SCHEMA coleccion TO regular_user;

    -- otorgar ciertos privilegios al rol usuario regular:
    GRANT SELECT, INSERT, UPDATE, DELETE ON coleccion.consola, coleccion.juego TO regular_user WITH GRANT OPTION;

    -- crear usuario con el rol nuevo:
    CREATE USER regular WITH PASSWORD '1234' IN ROLE regular_user;

Eliminar rol, usuario y revocar privilegios  
*******************************************

.. code-block:: sql 
    :linenos:

    -- Borrar usuario:
    DROP USER regular;

    -- Revocar permisos:
    REVOKE SELECT, INSERT, DELETE, UPDATE ON coleccion.juego, coleccion.consola FROM regular_user;

    -- Eliminar rol (no pueden existir usuarios o permisos en tablas vinculados a este rol):
    DROP ROLE regular_user;

TODO: REVISAR ESTA PARTE...

PL/SQL 
######

Es un lenguaje de programación similar a python o java el cual puede crear nuevos tipos de datos o calculos complejos.

Funciones 
*********

Declarar una función 
++++++++++++++++++++

.. code-block:: plsql 
    :linenos:

    -- Creamos una función que retornará un tipo de dato y añadimos los símbolos de dolar:
    CREATE FUNCTION coleccion.HolaMundo() RETURNS VARCHAR(50) AS $$
    -- justo después se declaran las variables:
    DECLARE 
        mensaje VARCHAR(50) := 'Hola mundo';
    BEGIN -- aquí comienza el contenido de ejecución de la función
    RETURN mensaje; -- retornamos el mensaje
    END; -- aquí finaliza la ejecución de la función
    $$ LANGUAGE plpgsql; -- definimos el lenguaje que es plpgsql

Ejecutar una función 
++++++++++++++++++++

.. code-block:: plsql 
    :linenos:

    -- usamos select para ejecutar la función:
    SELECT coleccion.HolaMundo();

.. note::
    Si queremos crear una función ya existente usamos ``CREATE OR REPLACE``

Eliminar función 
++++++++++++++++

.. code-block:: plsql 
    :linenos:

    DROP FUNCTION coleccion.holamundo();

.. note::
    En PGAdmin podemos desplegar Schema y si desplegamos functions veremos las funciones declaradas.


Uso de parámetros
*****************

.. code-block:: plsql 
    :linenos:

    CREATE FUNCTION coleccion.Sumar(num1 INT, num2 INT) -- pasamos los datos con su tipo
    RETURNS INT AS $$ -- retornaremos un tipo entero
    BEGIN
        RETURN num1 + num2;
    END;
    $$ LANGUAGE plpgsql;

    -- ejecutamos la función:
    SELECT coleccion.Sumar(20, 58);


Condicionales 
************* 

if / else 
+++++++++

.. code-block:: plsql 
    :linenos:

    CREATE FUNCTION coleccion.ComprobarEdad(edad INT)
    RETURNS VARCHAR(50) AS $$
    BEGIN
        -- comprobamos un numero:
        IF edad > 65 THEN 
            RETURN 'Con ' || edad || ' has llegado a la tercera edad';
        ELSIF edad < 18 THEN
            RETURN 'Con ' || edad || ' eres menor de edad';
        ELSE 
            RETURN 'Con ' || edad || ' eres mayor de edad';
        END IF;
    END;
    $$ LANGUAGE plpgsql;

    SELECT coleccion.ComprobarEdad(14);

CASE 
++++

.. code-block:: plsql 
    :linenos:

    CREATE FUNCTION coleccion.Opciones(opcion INT)
    RETURNS VARCHAR(50) AS $$
    DECLARE 
        mensaje VARCHAR(50) := 'Opción ';
    BEGIN
        -- esta sentencia funciona igual que switch:
        CASE 
            WHEN opcion = 1 THEN 
                RETURN mensaje || opcion || ': Ejecutar limpieza del sistema';
            WHEN opcion = 2 THEN 
                RETURN mensaje || opcion || ': Ejecutar reparación de archivos';
            WHEN opcion = 3 THEN 
                RETURN mensaje || opcion || ': Ejecutar creación de copia de respaldo';
            WHEN opcion = 4 THEN 
                RETURN mensaje || opcion || ': Ejecutar análisis del sistema';
            ELSE 
                RETURN 'No se reconoce la opción';
        END CASE;
    END;
    $$ LANGUAGE plpgsql;

    SELECT coleccion.Opciones(2);

Bucles
******

FOR LOOP 
++++++++

.. code-block:: plsql 
    :linenos:

    CREATE FUNCTION coleccion.Bucle(num INT)
    RETURNS INT AS $$
    DECLARE
        i INT := 1;
    BEGIN
        FOR i IN 1..num LOOP
            RAISE NOTICE 'Incrementando %', i;
        END LOOP;
    END;
    $$ LANGUAGE plpgsql;

    SELECT coleccion.Bucle(100);

.. note::
    Si queremos invertir el bucle de forma descendiente cambiamos el orden de los números: ``FOR i IN num..1 LOOP``

.. note::
    Si queremos dar saltos mayores usamos by: ``FOR i IN 1..num BY 2 LOOP``


WHILE  
+++++

.. code-block:: plsql 
    :linenos:

    CREATE FUNCTION coleccion.Mientras(num INT)
    RETURNS INT AS $$
    DECLARE
        i INT := 0;
    BEGIN
        WHILE i < num LOOP 
            RAISE NOTICE 'Incrementando %', i;
            i = i + 1;
        END LOOP;
    END;
    $$ LANGUAGE plpgsql;

    SELECT coleccion.Mientras(20);

Procedimientos
**************

Crear un procedimiento 
++++++++++++++++++++++

.. code-block:: plsql
    :linenos:

    CREATE PROCEDURE coleccion.InsertarConsola
    (marca VARCHAR(50), modelo VARCHAR(50), lanzamiento DATE, ventas INT)
    LANGUAGE plpgsql AS $$
    DECLARE
        idCode CHAR(6);
        idAux CHAR(6);
    BEGIN
        -- Sacamos el id de la última consola y sumamos uno mas:
        idCode := (SELECT id FROM coleccion.consola ORDER BY id DESC LIMIT 1);
        idAux := (SELECT SUBSTRING(idCode, 3, 6));
        idAux := CAST(idAux AS INT)+1;
        IF idAux < '9' THEN
            idCode = 'G-00' || idAux;
        ELSIF idAux BETWEEN '10' AND '99' THEN 
            idCode = 'G-0' || idAux;
        ELSIF idAux BETWEEN '100' AND '999' THEN 
            idCode = 'G-' || idAux;
        END IF;
        
        -- Ahora creamos la operación de inserción:
        INSERT INTO coleccion.consola VALUES
        (idCode, marca, modelo, lanzamiento, ventas);
        
        RAISE NOTICE 'Se ha añadido el registro % correctamente', idCode;
    END; $$

Ejecutar procedimiento
++++++++++++++++++++++

.. code-block:: plsql 
    :linenos:

    -- Utilizamos call para llamar procedimientos en lugar de select:
    CALL coleccion.InsertarConsola('Sega', 'Dreamcast', '1998-10-10', 93873);

Eliminar procedimiento  
++++++++++++++++++++++

.. code-block:: plsql 
    :linenos:

    DROP PROCEDURE coleccion.InsertarConsola();

.. note::
    En PGAdmin podemos desplegar Schema y si desplegamos procedures veremos los procedimientos declaradas.


Triggers 
********

Los triggers se ejecutan después de una operación. Por ejemplo al insertar un registro podemos ejecutar un select para visualizar datos.

Crear un Trigger 
++++++++++++++++

.. code-block:: psql 
    :linenos:

    -- crear una tabla donde registrar que usuario ejecutó una operación:
    CREATE TABLE coleccion.consola_operaciones(
        id SERIAL PRIMARY KEY, -- CREAMOS UNA PRIMARY KEY AUTOINCREMENTADA CON SERIAL
        accion VARCHAR(50),
        id_consola VARCHAR(50),
        modelo_consola VARCHAR(50),
        nombre_usuario VARCHAR(50),
        fecha TIMESTAMP
    );

    -- Crear la función que dispara el trigger:
    CREATE FUNCTION coleccion.BorradoConsola() RETURNS TRIGGER
    AS $$
    DECLARE
        usuario VARCHAR(20) := (SELECT CURRENT_USER); -- Averiguar que usuario realizo el borrado.
        fecha TIMESTAMP := (SELECT LEFT(CAST (CURRENT_TIMESTAMP AS CHAR(30)), 19));
    BEGIN
        INSERT INTO coleccion.consola_operaciones 
        (accion, id_consola, modelo_consola, nombre_usuario, fecha)
        -- OLD recupera los últimos datos borrado:
        VALUES('Borrado', OLD.id, OLD.modelo, usuario, fecha);

        RETURN NEW;
    END;
    $$ LANGUAGE plpgsql;

    -- crear el trigger que se ejecutará tras el borrado de un registro en consola:
    CREATE TRIGGER BorrarConsola AFTER DELETE ON coleccion.consola
    FOR EACH ROW
    EXECUTE PROCEDURE coleccion.BorradoConsola();


Ejecutar un Trigger 
+++++++++++++++++++

Para ejecutar un Trigger basta con ejecutar una operación sql relacionada, en este caso el borrado de un registro:

.. code-block:: plsql 
    :linenos:

    -- ejecutar operacion:
    DELETE FROM coleccion.consola WHERE id = 'G-0053';
    -- comprobar que se ha registrado:
    SELECT * FROM coleccion.consola_operaciones;

Eliminar un Trigger 
+++++++++++++++++++

.. code-block:: plsql 
    :linenos:

    DROP TRIGGER BorrarConsola ON coleccion.consola;


Administración de base de datos 
###############################

