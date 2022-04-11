Entornos: Node.JS 
=================

.. image:: /logos/logo-express.png
    :scale: 50%
    :alt: Logo Angular
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica de NodeJS 

.. contents:: Índice
 
Configuraciones
###############  

* Crear una carpeta para el proyecto y dentro ejecutar ``npm init``
* RECOMENDADO Instalar nodemon: ``npm install nodemon`` y agregar al **package.json**
* Instalar ExpressJS: ``npm install express --save``

Archivo Inicial
***************

* Se crea un archivo **index.js** o simil:

.. code-block:: javascript
    :linenos:

    // importamos la librería express:
    const express = require('express');

    // instanciamos express:
    const app = express();
    // definimos el puerto:
    const port = 3000;

    // se preparan los datos hardcodeados:
    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ]

    // Creamos una ruta raiz:
    app.get('/', (req, res)=>{
        // se define la cabezera y el cuerpo:
        res.status(200).send(consolas); // no hay que parsear a json.
    });

    // creamos el servidor:
    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });

Habilitar CORS
##############

Por defecto el proyecto tiene las CORS restringidas, de modo que si vamos a conectarnos desde 
una aplicación externa se bloqueará.

* Para trabajar con cors se instala ``npm install cors --save``

CORS Publicas
*************
Habilitar cors para hacer publica la API: 

.. code-block:: javascript 
    :linenos:

    const express = require('express');

    const app = express();
    const port = 3500;
    // importamos la librería cors:
    const cors = require('cors');

    // decimos a express que defina los cors (por defecto ahora es pública):
    app.use(cors());


Rutas Express
#############

Peticiones Get
**************

Ejemplo de Get con parámetros:

.. code-block:: javascript
    :linenos:

    const express = require('express');

    const app = express();
    const port = 3000;

    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ]

    app.get('/', (req, res)=>{
        res.status(200).send(consolas); 
    });

    // petición get de una ruta con un parámetro:
    app.get('/consola/:modelo', (req, res)=>{
        // recorremos las consolas y recuperamos la consola con el modelo buscado:
        let consola = consolas.find(elem => {
            return elem.modelo === req.params.modelo;
        });
        // si no encuentra nada:
        if(consola === undefined){
            return res.status(404).json({
                message: 'No se encontró ninguna consola'
            })
        }
        res.status(200).send(consola);
    });

    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });

Peticiones POST 
***************

Ejemplo de inserciones post:

.. code-block:: javascript 
    :linenos:

    const express = require('express');

    const express = require('express');

    const app = express();
    const port = 3000;

    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ];

    // ejecutamos el siguiente middleware para parsear código json de todo el body que entra por POST:
    app.use(express.json());
    app.use(express.urlencoded({extended: true}));

    app.get('/', (req, res)=>{
        res.status(200).send(consolas); 
    });

    app.get('/consola/:modelo', (req, res)=>{
        let consola = consolas.find(elem => {
            return elem.modelo === req.params.modelo;
        });

        if(consola === undefined){
            return res.status(404).json({
                message: 'Consola creada correctamente'
            })
        }
        res.status(200).send(consola);
    });

    // petición post:
    app.post('/consola/crear/', (req, res)=>{
        // añadir el nuevo valor al array:
        consolas.push(req.body);
        // devolvemos una respuesta:
        res.status(201).json({
            mensaje: 'Se ha registrado la consola'
        });
    });

    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });

Peticiones PUT  
**************

Ejemplo de actualizaciones put:

.. code-block:: javascript 
    :linenos:

    const express = require('express');

    const app = express();
    const port = 3000;

    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ];

    app.use(express.json());
    app.use(express.urlencoded({extended: true}));

    app.get('/', (req, res)=>{
        res.status(200).send(consolas); 
    });

    app.get('/consola/:modelo', (req, res)=>{
        let consola = consolas.find(elem => {
            return elem.modelo === req.params.modelo;
        });

        if(consola === undefined){
            return res.status(404).json({
                message: 'Consola creada correctamente'
            })
        }
        res.status(200).send(consola);
    });

    app.post('/consola/crear/', (req, res)=>{
        consolas.push(req.body);
        res.status(201).json({
            mensaje: 'Se ha registrado la consola'
        });
    });

    // crear un put que recibirá un parámetro para buscar el registro a actualizar:
    app.put('/consola/actualizar/:modelo', (req, res)=>{
        // localizar la posición en el array:
        let i = consolas.findIndex(elem => {
            return elem.modelo === req.params.modelo;
        });
        console.log();
        // si existe coincidencia se procede a crear:
        if(i > 0){
            consolas[i] = req.body;
            res.status(201).json({
                message: 'Consola actualizada con éxito'
            });
        }
    });

    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });


Peticiones DELETE   
*****************

Ejemplo de actualizaciones put:

.. code-block:: javascript 
    :linenos:

    const express = require('express');

    const app = express();
    const port = 3000;

    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ];

    app.use(express.json());
    app.use(express.urlencoded({extended: true}));

    app.get('/', (req, res)=>{
        res.status(200).send(consolas); 
    });

    app.get('/consola/:modelo', (req, res)=>{
        let consola = consolas.find(elem => {
            return elem.modelo === req.params.modelo;
        });

        if(consola === undefined){
            return res.status(404).json({
                message: 'Consola creada correctamente'
            })
        }
        res.status(200).send(consola);
    });

    app.post('/consola/crear/', (req, res)=>{
        consolas.push(req.body);
        res.status(201).json({
            mensaje: 'Se ha registrado la consola'
        });
    });

    app.put('/consola/actualizar/:modelo', (req, res)=>{
        let i = consolas.findIndex(elem => {
            return elem.modelo === req.params.modelo;
        });
        console.log();
        if(i > 0){
            consolas[i] = req.body;
            res.status(201).json({
                message: 'Consola actualizada con éxito'
            });
        }
    });

    // el delete recibirá también un parámetro para localizar un elemento:
    app.delete('/consola/eliminar/:modelo', (req, res)=>{
        let i = consolas.findIndex(elem => {
            return elem.modelo === req.params.modelo;
        });
        console.log();
        if(i > 0){
            // ejecutar método para borrar y mensaje:
            consolas.splice(i, 1);
            res.status(200).json({
                message: 'Consola eliminada con éxito'
            });
        }
    });

    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });