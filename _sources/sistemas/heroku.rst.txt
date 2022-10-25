======
Heroku
======

.. image:: /logos/heroku-logo.png
    :scale: 20%
    :alt: Logo Heroku
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Última edición el día |date| a las |time|. 

Despliegue de aplicaciones en Heroku.
 
.. contents:: Índice

Instalar Heroku CLI y desplegar aplicación  
##########################################


Crear proyecto y configurar
****************************

- Paso 1: Descargar e instalar Heroku CLI: https://devcenter.heroku.com/articles/heroku-cli
- Paso 2: Entrar en la página de Heroku y hacer click en **Create new app**
- Paso 3: abrir terminal en pc y ejecutar ``heroku login``

Crear un repositorio GIT
************************

- Paso 1: ejecutar en la raiz del proyecto ``git init``
- Paso 2: ejecutar en la raiz del proyecto: ``heroku git:remote -a taskmanagerpytonicus``

Desplegar aplicación 
********************

- Paso 1: añadir todos los datos: ``git add .``
- Paso 2: comitear los cambios: ``git commit -am "primer commit"``
- Paso 3: Pushear los datos en heroku: ``git push heroku master``

Comprobar que se ha desplegado
******************************

- En la pestaña overview se verá un panel en el que podemos observar a la derecha un mensaje **Build Succeeded**
- Si pinchamos arriba a la derecha en More y luego en Logs podemos ver si hay algún error.


NodeJS en Heroku 
****************

Existen un par de errores comunes en proyectos NodeJS, vamos a resolverlos:

- Error de puertos: editar el archivo **index.js** y cambiar el puerto por lo siguiente:

.. code-block:: javascript 
    :linenos:

    const mongoose = require("mongoose");
    const app = require('./app');
    // cambiar puerto por estas dos opciones:
    const port = process.env.PORT || 3977;

    mongoose.connect("mongodb+srv://guillermo:1234@cluster0.zicnrri.mongodb.net/?retryWrites=true&w=majority", {
        useNewUrlParser: true, 
        useUnifiedTopology: true,
    }, (err, res)=>{
        try{
            if(err){
                throw err;
            }else{
                console.log("Se ha establecido la conexión a la base de datos");
            }
        }catch(error){
            console.error(error);
        }
    });


    app.listen(port, () => {
        console.log(`Servidor funcionando en: http://localhost:${port}`);
    });

- Ausencia de comando start: editar package.json y añadir start en scripts:

.. code-block:: javascript 
    :linenos:

    {
        "name": "curso_node",
        "version": "0.0.1",
        "description": "Rest api node",
        "main": "index.js",
        "scripts": {
            "start": "node index.js", // esta linea no siempre se crea con npm init
            "test": "echo \"Error: no test specified\" && exit 1"
        },
        "author": "Guillermo Granados Gómez",
        "license": "MIT",
        "dependencies": {
            "express": "^4.18.1",
            "mongoose": "^6.5.2"
        }
    }
