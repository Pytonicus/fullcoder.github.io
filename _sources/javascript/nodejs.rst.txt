Entornos: Node.JS 
=================

.. image:: /logos/logo-node.png
    :scale: 50%
    :alt: Logo Angular
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica de NodeJS 

.. contents:: Índice
 
Configuraciones
###############  

Instalar NodeJS
***************

...

NodeJS CLI 
**********

* Inicializar un proyecto: ``npm init``
* Instalar un paquete: ``npm install paquete``
* Instalar dependencias: ``npm install``
* Instalar paquete y grabar dependencias: ``npm install express --save``
* Instalar un paquete y grabar dependencia de desarrollo: ``npm install paquete --save-dev``

Crear comandos
**************

Se pueden añadir nuevos comandos al package.json como sería el caso de la línea 8:

.. code-block:: javascript
    :linenos:

    {
        "name": "server",
        "version": "1.0.0",
        "description": "",
        "main": "index.js",
        "scripts": {
            "test": "echo \"Error: no test specified\" && exit 1",
            "start": "nodemon index"
        },
        "author": "",
        "license": "ISC",
        "devDependencies": {
            "nodemon": "^2.0.15"
        }
    }

Para ejecutar el nuevo comando llamado **start** escribimos ``npm start``.

Archivo principal 
*****************

* Se crea una caperta para el proyecto y se accede a ella desde linea de comandos. 
* Ejecutar ``npm init`` para inicializar el proyecto.
* Siguiendo los pasos se crea el archivo **package.json** con los metadatos del proyecto, unos scripts y las dependencias del proyecto.
* Crear el archivo de entrada principal de la aplicación **index.js** (o el nombre que hayamos elegido en el manifiesto):

.. code-block:: javascript
    :linenos:

    // cargar libreria http:
    const http = require('http');
    // definir puerto:
    const port = 3000;

    // Crear servidor que tendrá una función lambda con la request y la response:
    http.createServer((req, res)=>{
        // Escribimos la cabecera HEAD de la respuesta con el status y el content-type:
        res.writeHead(200, {'Content-Type': 'text/plain'});
        // escribimos el cuerpo del mensaje http BODY:
        res.write('Muestra en navegador del servidor');
        // cerramos la respuesta:
        res.end();
    }).listen(port, () =>{ // se concatena un listen con el puerto y un mensaje para confirmar que el servidor esta operativo
        console.log('Servidor ejecutandose en localhost:3000');
    });


Enrutamiento 
############

Este es un ejemplo de enrutamiento básico en Nodejs:

.. code-block:: javascript 
    :linenos:

    const http = require('http');
    const port = 3000;

    http.createServer((req, res)=>{
        // cargamos un switch y ponemos en valor la request:
        switch(req.url){
            // cada opción será una ruta:
            case '/':
                res.writeHead(200, {'Content-Type': 'text/plain'});
                res.write('Muestra en navegador del servidor');
                break;
            case '/about':
                res.writeHead(200, {'Content-Type': 'text/plain'});
                res.write('Pagina About');
                break;
            default:
                res.writeHead(404, {'Content-Type': 'text/plain'});
                res.write('Pagina no existe');
        }

        res.end();
    }).listen(port, () =>{ 
        console.log('Servidor ejecutandose en localhost:3000');
    });


Cargar datos en JSON
********************
El uso más común en Node.js es servir contenido json. Este es un ejemplo de uso:

.. code-block:: javascript 
    :linenos:

    const http = require('http');
    const port = 3000;

    // establecemos una coleccion de datos hardcodeada:
    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ]

    http.createServer((req, res)=>{
        switch(req.url){
            case '/':
                res.writeHead(200, {'Content-Type': 'text/plain'});
                res.write('Muestra en navegador del servidor');
                break;
            case '/about':
                res.writeHead(200, {'Content-Type': 'text/plain'});
                res.write('Pagina About');
                break;
            case '/consolas': // en esta ruta enviaremos los datos en formato json:
                res.writeHead(200, {'Content-Type':'application/json'});
                res.write(JSON.stringify(consolas)); // parseamos a json la colección
                break;
            default:
                res.writeHead(404, {'Content-Type': 'text/plain'});
                res.write('Pagina no existe');
        }

        res.end();
    }).listen(port, () =>{ 
        console.log('Servidor ejecutandose en localhost:3000');
    });


Paquetes Interesantes
#####################

Nodemon 
*******
Es un comando que ejecuta el servidor node.js en modo live refresh. De forma que al realizar cambios en el código estos se refrescan.

* Instalar nodemon: ``npm install nodemon``
* Añadir comando nodemon a **package.json**:

.. code-block:: javascript
    :linenos:

    {
        "name": "server",
        "version": "1.0.0",
        "description": "",
        "main": "index.js",
        "scripts": {
            "test": "echo \"Error: no test specified\" && exit 1",
            "start": "nodemon index"
        },
        "author": "",
        "license": "ISC",
        "devDependencies": {
            "nodemon": "^2.0.15"
        }
    }

* Ejecutar nodemon: ``npm start``.

