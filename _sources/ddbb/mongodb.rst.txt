MongoDB
=======

.. image:: /logos/mongodb-logo.png
    :scale: 25%
    :alt: Logo MongoDB
    :align: center

.. |date| date::
.. |time| date:: %H:%M
 

Funcionamiento de MongoDB
  
.. contents:: Índice

Primeros pasos   
##############

Instalación de MongoDB 
**********************

Para instalar MongoDB desde cualquier sistema operativo es recomendable seguir los pasos de su web oficial: https://www.mongodb.com/try/download/community

Herramienta MongoDB Compass 
***************************

Para instalar la herramienta cliente Studio 3T: https://studio3t.com/download-studio3t-free

O si prefieres MongoDB Compass: https://www.mongodb.com/es/products/compass

Tipos de datos 
**************

Tipos simples:

- números
- cadenas de textos 
- fecha
- hora 
- booleanos

Tipos complejos:

- Arrays
- objeto
- binary data 
- objectId (identificador que se crea automáticamente con cada documento)
- Expresiones regulares

Comandos de consola
###################

Si estás usando Studio 3T puedes utilizar su consola para ejecutar comandos.

Comandos de ejecución  
*********************

- Arrancar la consola: ``mongo``
- Listar bases de datos: ``show dbs``
- Eliminar base de datos: ``db.dropDatabase()``
- Seleccionar o Crear base de datos: ``use nombre_db`` (si no existe hasta que no hagas una inserción no la mostrará)
- Listar colecciones base de datos: ``show tables``
- Averiguar en que base de datos estás: ``db``
- Ver la metadata de la base de datos seleccionada: ``db.stats()``
- Mostrar ayuda para bases de datos: ``db.help()``
- Mostrar info del servidor: ``db.hostInfo()``
- Mostrar hora del sistema: ``Date()`` 

Comandos para inserción  
***********************

- Crear un documento en una colección: ``db.consolas.insertOne({marca: "Nintendo", modelo: "Switch"})`` (si no existe la colección la crea)
- Crear varios documentos o colecciones: ``db.consolas.insertMany([{marca: "Nintendo", modelo: "DS"}, {marca: "Sony", modelo: "Playstation"}])``

.. attention:: 
    En el momento que se inserta un registro en una base de datos esta ya aparece y también se crea la colección si no existe.

Comandos para consultas   
***********************

Consultas básicas 
+++++++++++++++++

- Consultar todos los elementos de una colección: ``db.consolas.find().pretty()`` (pretty mejora la lectura salvo en Studio 3T que viene mejorada)
- Consultar elementos de una colección que cumplan la condición: ``db.consolas.find({modelo: "Switch"})`` 
- Contar resultados: ``db.consolas.find().count()`` (se puede filtrar resultados)
- Limitar resultados mostrados en búsqueda a un número determinado: ``db.consolas.find().limit(2)``
- Consultar documentos y ordenarlos por ascendente (1) o descendiente (-1): ``db.consolas.find().sort({modelo: 1})``

Consultas para Arrays 
+++++++++++++++++++++

- Obtener todos los documentos que contengan los valores definidos en el array: ``db.consolas.find({videojuegos: {$all: ["Crash Bandicoot", "Metal gear solid"]}})`` (se pueden establecer uno o varios valores)

.. attention::
    en el primer ejemplo podemos usar también **$in** o **$ni** para que se cumpla la condición si contiene o no al menos uno de los valores.

Consulta para documentos 
++++++++++++++++++++++++

Para consultar en otros documentos embebidos o relacionados:

- Obtener documentos que contengan el valor de un documento embebido: ``db.consolas.find({"videojuegos.titulo": "Super Mario oddysey"})``

.. attention::
    Hay que observar que cuando se realiza este tipo de búsquedas la clave del elemento si lleva comillas.

Comandos para actualizar  
************************

- Actualizar un documento: ``db.consolas.updateOne({modelo: "Switch"}, { $set: {lanzamiento: 2017} })``
- Vaciar valores y añadir nuevos: ``db.consolas.replaceOne({modelo: "Playstation"}, {marca: "Sony"})`` (ahora solo estará el campo marca)
- Actualizar varios documentos: ``db.consolas.updateMany({lanzamiento: {$gt: 2011}}, { $set: {generacion: "Octava"} })`` 

.. note::
    $gt y $set son filtros. En el primer caso $gt indica que se esta buscando un número mayor que el indicado y en el segundo que se va a editar unos campos.

Actualizar Arrays 
+++++++++++++++++

- Añadir elemento al array: ``db.users.updateOne({nickname:"pytonicus"}, {$addToSet: {games: "Metal Gear Solid"}})``
- Añadir varios elementos al array (sin añadir repetidos): ``db.users.updateOne({nickname:"pytonicus"}, {$addToSet: {games: {$each: ["Metal Gear Solid", "Crash Bandicoot"]}}})``
- Añadir varios elementos al array (añadiendo repetidos): ``db.users.updateOne({nickname:"pytonicus"}, {$addToSet: {games: {$push: ["Metal Gear Solid", "Crash Bandicoot"]}}})``
- Eliminar último elemento del array (o primero usando -1): ``db.users.updateOne({nickname:"pytonicus"}, {$pop: {games: 1}})``
- Eliminar un elemento del array: ``db.users.updateOne({nickname:"pytonicus"}, {$pull: {games: "Metal Gear Solid"}})``

Comandos para eliminar   
**********************

El comando para eliminar realiza su trabajo bajo condición. Si más de un documento cumple con el campo elegido se eliminara el primero en el caso **deleteOne()** y varios si usamos **deleteMany()**

- Eliminar un documento: ``db.consolas.deleteOne({modelo: "Playstation"})``
- Eliminar varios documentos: ``db.consolas.deleteMany({marca:"Nintendo"})``
- Vaciar colección: ``db.consolas.deleteMany({})``
- Eliminar colección: ``db.consolas.drop()``


Operadores
**********

Los operadores empiezan con un símbolo $ y se usan para filtrar la información:

- **$set**: añadir o editar campos.
- **$eq**: igual que.
- **$lt**: menor que.
- **$lte**: menor o igual que.
- **$gt**: mayor que.
- **$gte**: mayor o igual que.
- **$ne**: distinto.
- **$in**: dentro de.
- **$nin**: fuera de.
- **$all**: Busca documentos que tengan un array que tengan como mínimo los elementos de la busqueda.


Relaciones en MongoDB 
#####################

Documento embebido
******************

La relación de un documento embebido suele ser un json dentro de otro:

.. code-block:: javascript 
    :linenos:

    {
        "_id" : ObjectId("62fb86771d63eaf8fbcc54c5"),
        "marca" : "Nintendo",
        "modelo" : "Switch",
        "lanzamiento" : 2017.0,
        "generacion" : "Octava",
        "videojuegos" : [
            {
                "titulo" : "Zelda Breath of the wild",
                "lanzamiento" : 2017.0
            },
            {
                "titulo" : "Super Mario Oddysey",
                "lanzamiento" : 2017.0
            }
        ]
    }


Documento relacionado
*********************

El documento relacionado tiene una lista de identificadores que relacionan a un documento con otros documentos:

.. code-block:: javascript 
    :linenos:

    {
        "_id" : ObjectId("62fb86771d63eaf8fbcc54c5"),
        "marca" : "Nintendo",
        "modelo" : "Switch",
        "lanzamiento" : 2017.0,
        "generacion" : "Octava",
        "videojuegos" : [1,2]
    }

Indices en MongoDB 
##################

Los índices son estructuras de datos especiales que gestiona MongoDB almacenando el valor de un campo específico. Por defecto en cada colección se crea el índice **_id**.
Estos índices se utilizan para mejorar el rendimiento en las búsquedas de resultados.


- Listar todos los índices: ``db.consolas.getIndexes()``

Índices simples 
***************

- Crear un índice: ``db.consolas.createIndex({marca: -1})`` (-1 ordena descendente, 1 orden ascendente)
- Eliminar un index (utiliza el name): ``db.consolas.dropIndex("marca_-1")``

.. note::
    Al hacer un find a partir de ahora MongoDB localiza el índice y optimiza las búsquedas.


Índices compuestos
******************

El índice compuesto se aplica sobre dos o más campos:

- Crear un índice compuesto: ``db.consolas.createIndex({marca: 1, lanzamiento: -1})``
- Eliminar un index (utiliza el name): ``db.consolas.dropIndex("marca_1_lanzamiento_-1")``

.. note::
    todas las consultas que impliquen estos dos campos irán mas deprisa y se organizarán por marca ascendente y luego por lanzamiento descendiente.

Índices únicos
**************

Estos índices se crean para aquellos documentos que tengan un campo con un valor único.

- Crear un índice único: ``db.consolas.createIndex({modelo: 1}, {unique: true})``
- Eliminar un index (utiliza el name): ``db.consolas.dropIndex("modelo_1")`` 

.. attention::
    Si se intenta crear un índice tipo único en un campo que contenga valores repetidos o nulos, dará error.

.. attention::
    Al crear este tipo de índice, ya no podrás crear documentos que contenga un valor duplicado en el campo indexado.

