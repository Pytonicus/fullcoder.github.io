Microframework: Flask 
=====================

.. image:: /logos/logo-flask.png
    :scale: 10%
    :alt: Logo Flask
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica para trabajar con el Microframework Flask

.. contents:: Índice
 
Configuraciones
###############  
  
Creación del proyecto
*********************
 
* Crear un Directorio para el proyecto y acceder al mismo.
* Crear un entorno virtual.
* Instalar flask: ``pip install flask``.
* Dentro del directorio creamos un directorio llamado templates y un archivo llamado main.py

Archivo principal
*****************

El archivo principal básico:

.. code-block:: python
    :linenos:

    # importamos flask y creamos el objeto con flask:
    from flask import Flask
    app = Flask(__name__)

    # Con un decorador definimos la ruta raiz y dentro una función que devuelve un mensaje.
    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # creamos la condición para arrancar la aplicación flask:
    if __name__ == "__main__":
        # le pasamos la ejecución de la app y por parámetros la ruta del host y si esta en modo depuración o no.
        app.run(host='localhost', debug=True)

* Arrancar el servidor: ``python main.py``
* Abrir en navegador: http://localhost:5000

.. note::
    Al tener habilitado el flag debug en la función run nos dará un pin al arrancar el servidor,
    dicho pin se usará para abrir el depurador en el navegador cuando tengamos algún error de manera que 
    se pulsará sobre el icono de la consola en cualquier línea y se introduce el pin.

Rutas
#####

Rutas principales (main.py)
***************************
Las rutas se suelen añadir en el archivo principal del proyecto:

.. code-block:: python
    :linenos: 

    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # despues de la / creamos otra ruta:
    @app.route('/otra_ruta')
    def hola():
        return 'Acceso a otra ruta!'

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

* En el navegador abrir: http://localhost:5000/otra_ruta

rutas con parámetros 
********************

* Las rutas con parámetros:

.. code-block:: python
    :linenos:

    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # con los símbolos mayor-menor podemos capturar un parámetro por defecto tipo cadena:
    @app.route('/nombre/<persona>')
    def nombre(persona):
        return 'Te llamas {}'.format(persona)

    # Podemos definir que sea un entero o coma flotante:
    @app.route('/edad/<int:edad>')
    def edad(edad):
        return 'Tienes: {} años'.format(edad)

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

* La ruta que recibe parámetros por ejemplo sería: http://localhost:5000/nombre/Guillermo


Rutas por uno o más métodos
***************************
Es posible estipular uno o varios métodos permitidos en una ruta:

.. code-block:: python
    :linenos:

    from flask import Flask
    # importamos la librería request que funciona igual que en django:
    from flask import request

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # el decorador recibe una lista de métodos permitidos:
    @app.route('/metodos', methods=['GET', 'POST'])
    def login():
        # preguntamos si el método es GET que nos abra sesion y si no que nos mande de vuelta al formulario:
        if request.method == 'GET':
            return 'Recibido ' + request.method
        else:
            print("Es otro método")

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

.. note::
    aunque en este ejemplo se usa GET para validar el metodo de entrada, es más común y más cómodo validar el método POST, 
    ya que este último podría presentar más iteracciones en el código que el método GET.

Redirecciones
*************

.. code-block:: python
    :linenos:

    # cargar librerías redirect y url_for:
    from flask import Flask, render_template, redirect, url_for


    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        # Redireccionar a otra ruta usando el nombre de su función:
        return redirect(url_for('saludar'))


    @app.route('/saludar', methods=['GET'])
    def saludar(nombre=None): 
        return 'Hola desde otra ruta'


    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

Error 404
+++++++++
Procedimiento común para redirección 404:

* Crear en **templates** archivo **error.html**:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>ERROR 404</title>
    </head>
    <body>
        <h1>ERROR 404</h1>
        <p>La página solicitada no existe</p>
    </body>
    </html>

* Crear error 404 cuando introducimos rutas incorrectas:

.. code-block:: python
    :linenos:

    from flask import Flask, render_template, redirect, url_for

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return redirect(url_for('saludar'))


    @app.route('/saludar', methods=['GET'])
    def saludar(nombre=None): 
        return 'Hola desde otra ruta'

    # cargamos la ruta de error cuando no se encuentre página:
    @app.errorhandler(404)
    def error(error): # este recibe un parámetro 
        return render_template('error.html'), 404

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

Vistas
######

Las vistas en Flask no suelen usarse, en su lugar se visualizan los templates con Jinja

Templates (Jinja2)
##################

Jinja2 es el motor de plantillas que se utiliza de serie en Flask.

* En la carpeta templates se crea un archivo por ejemplo prueba.html:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
    </head>
    <body>
        <h1>Plantillas Jinja2</h1>
        <p>primera toma de contacto con Flask</p>
    </body>
    </html>

* De vuelta a main.py se renderiza el template:
 
.. code-block:: python
    :linenos:
 
    # importamos render_template para gestionar plantillas:
    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    @app.route('/prueba')
    def prueba(nombre=None): 
        # Renderizamos el archivo prueba:
        return render_template('prueba.html') 

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)


Template Tags
*************

Los Template Tags son un tipo de etiquetas especiales en Jinja2 que se utilizan en las plantillas para ejecutar respuestas backend.

Estas etiquetas suelen tener dos tipos de estructuras: ``{% instrucción %}`` o ``{{ datos }}`` según el tipo de tarea que vayamos a ejecutar.

Template tag base
+++++++++++++++++

Una buena práctica para no repetir código en plantillas es coger todo el contenido común y almacenarlo en una plantilla base:

* En **templates** crear un archivo llamado **base.html**:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
    </head>
    <body>
        {% block cuerpo %}{% endblock %}
    </body>
    </html>

* En el resto de archivos html se elimina todo lo que contemple fuera del body del siguiente modo:

.. code-block:: html 
    :linenos: 

    {% extends 'base.html' %}

    {% block cuerpo %}
    <form method="POST" action="/subir" enctype="multipart/form-data">
        <label for="documento">Subir archivo</label>
        <br>
        <input type="file" name="documento">
        <br><br>
        <input type="submit">
    </form>
    {% endblock %}


Template tag static
+++++++++++++++++++

* En la raiz del proyecto crear carpeta llamada static.
* Crear archivo style.css:

.. code-block:: css
    :linenos:

    body{
        background: yellow;
        color: green;
    }

* En el template se vincula:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
        <!-- Para añadir un archivo css utilizamos url for en una etiqueta jinja2 -->
        <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
    </head>
    <body>
        <h1>Plantillas Jinja2</h1>
        <p>primera toma de contacto con Flask</p>
    </body>
    </html>


Template tag de datos
+++++++++++++++++++++

Los template tags de datos muestran información que enviamos desde la vista al template.

* Si nos vamos a views.py para añadir un dato:

.. code-block:: python
    :linenos:

    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola!!!'


    @app.route('/hola')
    def saludar(): 
        nombre = "Guillermo"
        return render_template('hola.html', nombre=nombre)


    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

* Ahora que tenemos un dato, podemos mostrarlo en cualquier template de nuestra app:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <p>Hola {{nombre}}</p>
    </body>
    </html>

Template tag for
++++++++++++++++

* Se crea un listado en **main.py**:

.. code-block:: python
    :linenos: 

    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola!!!'


    @app.route('/hola')
    def saludar(): 
        personas = ["Guillermo", "Antonio", "Josefa", "Adrián"]
        return render_template('hola.html', personas=personas)


    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

* Y ahora podemos recorrer el diccionario en nuestro template con el template tag for:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <ul>
            {% for persona in personas %}
                <li>{{ persona }}</li>
            {% endfor %}
        </ul>
    </body>
    </html>

Template tag if
+++++++++++++++

Con el template tag if podemos establecer condiciones dentro de los templates, retomando el ejemplo de for vamos a pintar de verde uno de los registros:

* Template condicional que recibe un parámetro:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
    </head>
    <body>
        {% if nombre %}
            <h1>Hola {{ nombre }}</h1>
        {% else %}
            <h1>Hola mundo</h1>
        {% endif %}
    </body>
    </html>

* Cargar el template y pasarle parámetro:

.. code-block:: python
    :linenos:

    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'


    @app.route('/saludos/<nombre>')
    def saludos(nombre=None):
        return render_template('saludos.html', nombre=nombre) # le pasamos el template y la variable con la clave nombre

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

Formularios
###########

En Django podemos crear formularios individuales y reutilizables.

Formularios via POST
********************

* Se crea el archivo por ejemplo **form.html**:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <form method="POST">
            <input type="text" name="nombre" placeholder="Tu nombre">
            <input type="text" name="apellidos" placeholder="Tus apellidos">
            <input type="submit" value="Saludar">
        </form>
    </body>
    </html>

* Lo siguiente es registrar las rutas en Flask:

.. code-block:: python
    :linenos: 

    from flask import Flask, render_template, redirect, url_for, request

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return redirect(url_for('saludar'))


    @app.route('/saludar', methods=['GET'])
    def saludar(): 
        return render_template('form.html')

    @app.route('/saludar', methods=['POST'])
    def saludo(): 
        nombre = request.form['nombre']
        apellidos = request.form['apellidos']
        return 'Te llamas ' + nombre + " " + apellidos


    if __name__ == "__main__":
        app.run(host='localhost', debug=True)


Recuperar archivos en Flask
***************************

De este modo se gestionaría la subida de un archivo desde un formulario:

* Crear en la raiz un directorio llamado **subidas**
* Crear en **templates** un archivo llamado **subidas.html**:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
    </head>
    <body>
        <form method="POST" action="/subir" enctype="multipart/form-data">
            <label for="documento">Subir archivo</label>
            <br>
            <input type="file" name="documento">
            <br><br>
            <input type="submit">
        </form>
    </body>
    </html>

* Por último registrar dos rutas en **main.py**:

.. code-block:: python
    :linenos:

    from flask import Flask, render_template, request
    # añadimos también una utilidad para generar nombres seguros de archivos:
    from werkzeug.utils import secure_filename

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # Ruta del form:
    @app.route('/subir', methods=['GET'])
    def hola(nombre=None): 
        return render_template('subidas.html') 

    # Ruta para procesar la petición:
    @app.route('/subir', methods=['POST'])
    def subir():
        if request.method == 'POST':
            # recuperamos el archivo del parametro files:
            f = request.files['documento']
            # ahora guardamos el archivo con un nombre seguro:
            f.save('./subidas/{}'.format(secure_filename(f.filename)))
            return 'Se ha subido correctamente'

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)


Bases de datos con SqlAlchemy
#############################

Instalar librería 
*****************

* Para usar esta librería se instala: ``pip install Flask-Sqlalchemy``

Crear paquete del proyecto 
**************************

Se crea un paquete llamado **application** y dentro un archivo **__init__.py** para inicializarlo, se mueve aquí el archivo principal de la aplicación.


Configurar base de datos 
************************

En el paquete **application** del proyecto se crea un archivo config.py:

.. code-block:: python 
    :linenos:

    import os    

    secret_key = 'CAB7D2CD6CCDC28113C9A3189DEE647BD945B0903EFEC1E160F2ADB5203CE649'
    PWD = os.path.abspath(os.curdir)    

    DEBUG = True # Modo depuración lo pasamos aquí
    # Vinculamos el conector a la base de datos, en este caso sqlite:
    SQLALCHEMY_DATABASE_URI = 'sqlite:///{}/dbase.db'.format(PWD)
    SQLALCHEMY_TRACK_MODIFICATIONS = False # por rendimiento definimos el track en false

ahora editamos el archivo principal para añadir los cambios:

.. code-block:: python 
    :linenos:

    from flask import Flask
    # Se carga el sqlalchemy también aqui:
    from flask_sqlalchemy import SQLAlchemy
    # se carga el archivo de configuración:
    from application import config    

    app = Flask(__name__)

    # se añade una linea para cargar el archivo config en app:
    app.config.from_object(config)
    # y se carga la base de datos:
    db = SQLAlchemy(app)

    @app.route('/')
    def inicio():
        return 'Página principal'    

    if __name__ == "__main__":  # establecemos el debug que tenemos en config:
        app.run(host='localhost', debug=config.DEBUG)


Crear modelo de datos 
*********************

En el paquete **application** del proyecto se creará un archivo llamado models.py:

.. code-block:: python 
    :linenos:

    # Se importan los tipos de datos:
    from sqlalchemy import *
    # se importa el relacionador:
    from sqlalchemy.orm import relationship
    # se importa la configuración de la base de datos:
    from application.app import db 


    # creamos un primer modelo que será relacionable con el segundo:
    class Categories(db.Model):
        """ Categorías """
        # se define nombre interno de tabla y los campos:
        __tablename__ = 'categories'
        id = Column(Integer, primary_key=True)
        name = Column(String(100))
        
        # retornar clase y función:
        def __repr__(self):
            return (u'<{self.__class__.__name__}: {self.id}>'.format(self=self))


    # Crear otro modelo relacionado con el primero:
    class Articles(db.Model):
        """ Artículos """
        __tablename__ = 'articles'
        id = Column(Integer, primary_key=True)
        nombre = Column(String(100),nullable=False)
        precio = Column(Float,default=0)
        iva = Column(Integer,default=21)
        descripcion = Column(String(255))
        image = Column(String(255))
        stock = Column(Integer,default=0)
        CategoriaId=Column(Integer,ForeignKey('categories.id'), nullable=False)
        categoria = relationship("Categories", backref="Articles")    

        def precio_final(self):
            return self.precio*self.iva/100    

        def __repr__(self):
            return (u'<{self.__class__.__name__}: {self.id}>'.format(self=self))


Crear base de datos 
*******************
Para crear la base de datos ejecutamos la línea de comandos python y los siguientes comandos:

* importar configuración base de datos: ``from application.app import db``
* importar modelos de datos a crear: ``from application.models import Categories, Articles``
* Ejecutar creación de tablas: ``db.create_all()``


Migrar datos modificados en el modelo
*************************************

Actualmente Flask no incorpora un modelo de migración de datos como en el caso de Django. Si se añade un nuevo dato hay que ejecutar primero ``db.drop_all()`` y a continuación
``db.create_all()``

CRUD desde consola python
*************************
* importar configuración base de datos: ``from application.app import db``

Crear registro 
++++++++++++++

* asignar valor al modelo que se quiere adherir dato: ``cat=Categories(name="RPG")``
* Cargar en el orm los datos: ``db.session.add(cat)``
* Cargar en el orm varios datos: ``db.session.add_all([cat1, cat2])``
* Comitear los datos en la base de datos: ``db.session.commit()``


Leer registro 
+++++++++++++

* Cargar una lista completa de registros: ``cat=Categories.query.all()`` (se tiene que recorrer con un bucle)
* Cargar primer elemento de la lista: ``cat=Categories.query.first()``
* Cargar un elemento de la lista por dato de referencia: ``cat=Categories.query.get(1)``
* Filtrar registros: ``Categories.query.filter_by(name="RPG").all()``
* Filtrar por múltiples campos: ``Categories.query.filter_by(name="RPG").filter_by(subname="rol").all()``
* Ortdenar registros recuperados: ``Categories.query.order_by("name").all()``

.. note::
    Cada registro recuperado es un objeto, por lo que acceder a cada campo es igual al acceder a un atributo de una clase ej: **cat.name**

.. note::
    Al igual que se filtran registros y se obtienen todos los resultados posibles, podemos obtener con first() el primer resultado posible.


Editar registro
+++++++++++++++
* Cargar un elemento de la lista por dato de referencia: ``cat=Categories.query.get(1)``
* Modificar un campo del elemento: ``cat.name="Rol"``
* Cargar en el orm los datos: ``db.session.add(cat)``
* Comitear los datos en la base de datos: ``db.session.commit()``


Eliminar registro
+++++++++++++++++
* Cargar un elemento de la lista por dato de referencia: ``cat=Categories.query.get(1)``
* Cargar en el orm los datos con delete: ``db.session.delete(cat)``
* Comitear los datos en la base de datos: ``db.session.commit()``


Trabajar con relaciones 
+++++++++++++++++++++++

A partir de un campo foreign key se pueden obtener los datos de la otra tabla relacionada 
como un objeto: 
* Si recuperamos un registro de la tabla articles: ``art1=Articles.query.get(1)``
* Al estar relacionada con categories se puede recuperar la información de la categoría: ``art1.categories.nombre``


Uso del ORM en archivos py
**************************

El uso del orm es similar al visto en la consola, ejecutando las operaciones desde scripts python:

.. code-block:: python 
    :linenos:

    from aplicacion.models import Articles
    @app.route('/')
    def inicio():
        articulos=Articles.query.all()
        return render_template("inicio.html",articulos=articulos)

* Esto en una plantilla se usaría así:

.. code-block:: html 
    :linenos:

    <div class="panel-heading">Videojuegos</div>
        <table class="table">
                {% for art in articulos %}
                    <tr>
                        <td>{{art.nombre}}</td>
                    </tr>
                {% endfor %}
        </table>
    </div>

Sistema de usuarios y sesiones
##############################

Modelo de usuarios
******************

Antes de nada hay que crear un modelo de usuarios en la base de datos:

.. code-block:: python 
    :linenos:

    class Usuarios(db.Model):
    """Usuarios"""
    __tablename__ = 'usuarios'
    id = Column(Integer, primary_key=True)
    username = Column(String(100),nullable=False)
    password_hash = Column(String(128),nullable=False)
    nombre = Column(String(200),nullable=False)
    email = Column(String(200),nullable=False)
    admin = Column(Boolean, default=False)

    def __repr__(self):
        return (u'<{self.__class__.__name__}: {self.id}>'.format(self=self))    

    @property
    def password(self):
        raise AttributeError('password is not a readable attribute')    

    @password.setter
    def password(self, password):
        self.password_hash = generate_password_hash(password)
    def verify_password(self, password):
        return check_password_hash(self.password_hash, password)

.... TODOOOO