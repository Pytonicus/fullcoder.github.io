Framework: Django
=================

.. image:: /logos/logo-django.png
    :scale: 50%
    :alt: Logo Django
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica para trabajar con Django 3

.. contents:: Índice
 
Configuraciones
###############  
 
Creación del proyecto
*********************

Crear entorno virtual y seguir estos pasos:

* Instalar Django: ``pip install django``
* crear un nuevo proyecto: ``django-admin startproject nombre_proyecto``
* Arrancar servidor: ``python manage.py runserver``
* En el navegador: ``localhost:8000`` para ver si arrancó la aplicación.

Configuración del proyecto (settings.py)
****************************************

Acceder desde la raiz del proyecto a la carpeta con el mismo nombre de este. Editar: ``settings.py``:

* debug: ``True`` por defecto, mostrará errores en el navegador. ``False`` para evitar mostrarlos en producción.
* ALLOWED_HOSTS: Un listado en blanco en el cual podemos escribir los dominios permitidos con los que mostrar la app.
* INSTALLED_APPS: Listado donde se añaden las apps que se irán creando.
* DATABASES: Diccionario con las bases de datos que se van a usar, por defecto una SQLite.
* LANGUAGE_CODE: cambiar valor por ``es`` para tener el proyecto en español.
* TIME_ZONE: Para zona horaria España, cambiar a ``Europe/Madrid``
* STATIC_URL: Url donde se guardarán los archivos estáticos.
* MEDIA_URL: Url donde se guardan los archivos multimedia (no existe por defecto).

Arrancar la base de datos
*************************

Trabajar con SQLite
+++++++++++++++++++

* Viene preparada por defecto:

.. code-block:: python 
    :linenos:

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': BASE_DIR / 'db.sqlite3',
        }
    }

* Crear el CRUD inicial de Usuarios: ``python manage.py migrate``

Trabajar con MySQL
++++++++++++++++++

* La configuración sería la siguiente:

.. code-block:: python
    :linenos:

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'nombre_database',
            'USER': 'usuario_database',
            'PASSWORD': 'clave_database',
            'HOST': 'localhost',
            'PORT': '3306',
        }
    }

* Del mismo modo se ejecuta la primera migración: ``python manage.py migrate``

Crear un Administrador
**********************

* Una vez ejecutada la primera migración se genera un usuario ejecutando en terminal: ``python manage.py createsuperuser``

Crear una aplicación
********************

Django es un Framework modular, lo que quiere decir que iremos creando aplicaciones en el para gestionar distintas páginas y así poder reutilizar código.
* Crear app: ``python manage.py startapp nombre_de_tu_app``, esto nos genera una carpeta con los archivos esenciales para una app (views.py, models.py...) 
* Añadir a la lista de apps en ``settings.py``:

.. code-block:: python
    :linenos: 

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'nombre_de_tu_app' # Declaramos nuestra app en esta lista
    ]

Rutas
#####

Rutas principales (prueba/urls.py)
**********************************
El archivo de rutas principal de Django se encuentra en la carpeta cuyo nombre es el del proyecto y se llama ``urls.py``.

urls.py principal:

.. code-block:: python
    :linenos: 

    # las dos primeras líneas importan el panel de administración y la librería path para agregar rutas
    from django.contrib import admin
    from django.urls import path
    from nombre_de_tu_app import views # Este es el archivo de vista que importamos de la app creada anteriormente

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('home/', views.home, name = 'home'), # Definimos que '' (ruta raiz) apunte a la vista **home** y tenga el name 'home' para luego usar un template tag de rutas.
    ]

.. note::
    Si en lugar de home/ definimos un string vacio esta vista se establecerá como la vista principal en cada aplicación

.. note::
    La primera ruta que se observa lleva hacia el panel de administración que viene ya creado de serie en Django 
    
.. attention::
    En los casos que se arranca el servidor y este da un fallo suele ser por dos razones,
    la primera que no se haya importado la vista correspondiente y la segunda que no se haga 
    creado la función de vista en su archivo ``views.py``

Rutas en App (nombre_app/urls.py)
*********************************
Es posible generar otros archivos de rutas ``urls.py`` dentro de cada aplicación para gestionar sus rutas internas.

* En el archivo de rutas principal (prueba/urls.py):

.. code-block:: python
    :linenos:

    from django.contrib import admin
    from django.urls import path, include # Cargamos la librería include

    urlpatterns = [
        path('admin/', admin.site.urls),
        # importamos el archivo urls de nuestra app:
        path('', include('nombre_de_tu_app.urls'))    
    ]

* Se crea el archivo en la ruta de la app correspondiente: (nombre_de_tu_app/urls.py):

.. code-block:: python
    :linenos:

    from django.urls import path
    from . import views as nombre_de_tu_app

    urlpatterns = [
        path('', nombre_de_tu_app.home, name='home'),
        path('sobremi/', nombre_de_tu_app.about, name='sobremi'),
    ]

En este archivo se gestionarán las rutas hacia las vistas de esta app en concreto.

rutas con parámetros 
********************

* Las rutas con parámetros:

.. code-block:: python
    :linenos:

    from django.urls import path
    from . import views as nombre_de_tu_app

    urlpatterns = [
        path('', nombre_de_tu_app.home, name='home'),
        # despues del slash pasamos entre símbolos menor y mayor que el tipo de variable y el parámetro. si no lleva nada lo reconoce como cadena
        path('sobremi/<int:id_entrada>', nombre_de_tu_app.about, name='sobremi'),
    ]

* La ruta que recibe parámetros por ejemplo sería: http://localhost:5000/sobremi/19

* Procesar parámetros desde la vista:

.. code-block:: python
    :linenos:

    from django.shortcuts import render
    from .models import Prueba

    # la función recibe por parámetros la id de la entrada:
    def about(request, id_entrada):
        # este parámetro lo podemos usar por ejemplo para encontrar una entrada ya que django por defecto les asigna un id
        entrada = Prueba.objects.find(id=id_entrada)
        return render(request, 'nombre_de_tu_app/about.html', {'entrada':entrada})


Rutas de CBV
************
Si trabajamos con **Vistas Basadas en Clases (CBV)** las rutas son distintas:

.. code-block:: python
    :linenos:

    from django.urls import path
    # Importamos las vistas:
    from .views import HomePageView

    urlpatterns = [
        # Devolvemos las urls con el metodo as_view para que las muestre como tal:
        path('', HomePageView.as_view(), name="home"),
    ]

Vistas
######

Existen dos formas de crear vistas en Django, las **FBV** (Function-based Views) y las **CBV** (Class-based Views).

FBV (Function-Based Views)
**************************

Vistas basadas en funciones:

* Devolver respuesta HTML con **HttpResponse**:

.. code-block:: python
    :linenos:

    from django.shortcuts import HttpResponse # el modulo HttpResponse carga una respuesta HTML directamente sin plantillas.

    # Creamos la función que gestionará la vista home definida como raiz en urls.py:
    def home(request):
        return HttpResponse("<h1>Título de prueba</h1><h2>Subtítulo</h2>") # esta va a retornar una respuesta html

Si nos vamos al navegador y ejecutamos la raiz veremos que el mensaje de bienvenida cambió por este último.

* Devolver una plantilla HTML con **Render**:

.. code-block:: python
    :linenos:

    # importamos render que suele venir importado por defecto:
    from django.shortcuts import render 

    # creamos una función para gestionar los datos de vista:
    def home(request):
        # dentro de esta vista retornamos render y le pasamos por el segundo parámetro la plantilla que vamos a usar:
        return render(request, 'nombre_de_tu_app/home.html')

.. attention::
    Es probable tener un error Template does not exist, se debe a que se ha creado aun el template, 
    o que no se ha añadido la app a INSTALLED_APPS o simplemente requiere reiniciar el servidor 
    para que funcione.

CBV (Class-Based Views)
***********************

Vistas basadas en Clases, existen varias:

TemplateView
++++++++++++

Clase de vista estandar, se utiliza comunmente para renderizar templates:

.. code-block:: python
    :linenos:

    from django.shortcuts import render
    # Importamos la librería templateview:
    from django.views.generic.base import TemplateView

    # Utilizamos las de tipo templateview para devolver un template:
    class HomePageView(TemplateView):
        template_name = 'nombre_de_tu_app/home.html'

ListView
++++++++

Con ListView podemos devolver una tabla de la base de datos de forma sencilla:

.. code-block:: python
    :linenos: 

    from django.shortcuts import render
    # Importamos el listview y la base de datos:
    from django.views.generic.list import ListView
    from .models import Page

    # Ahora creamos la clase de tipo ListView:
    class PageListView(ListView):
        model = Page # Gestionará el modelo page
        paginate_by = 3 # así de sencillo se paginan resultados.

De esta forma tenemos un listado en el template listo para recorrer usando el bucle sobre el valor object_list ``{% for pagina in object_list %}``

.. attention::
    Para que funcione esta vista y encuentre su template por defecto sería **page_list.html** y la colocamos dentro de la carpeta ``templates/nombre_de_tu_app/``

DetailView
++++++++++

Con la vista detalle recuperamos un elemento de la base de datos para visualizarlo, veamos views.py:

.. code-block:: python
    :linenos:

    # Importamos el detailview:
    from django.views.generic.detail import DetailView
    from .models import Page


    # Ahora vamos a integrar la clase de pagina simple con el detailview:
    class PageDetailView(DetailView):
        model = Page # cargamos el modelo Page

En la ruta deberemos asignar el parámetro ``<int:pk>`` para poder recibir el id del elemento.

.. attention::
    Debemos crear el template dentro de templates/nombre_de_tu_app/ con el nombre page_detail.html, ahora solo falta imprimir los datos usando el template tag {{page}}

CreateView
++++++++++

Como su nombre indica, es la vista para crear elementos, vamos a probarla en views.py:

.. code-block:: python
    :linenos:

    # Importamos CreateView:
    from django.views.generic.edit import CreateView
    # e importamos la librería para hacer redirecciones:
    from django.urls import reverse_lazy

    from .models import Page

    # Y creamos la vista con CreateView para crear registros:
    class PageCreate(CreateView):
        model = Page # Cargamos el modelo.
        fields = ['title', 'content', 'order'] # Y ahora añadimos los campos que vamos a permitir que se puedan crear
        # Opcionalmente hacemos un reverse_lazy que retorna a la página que le indicamos:
        success_url = reverse_lazy('pages:pages')

Con esto solo nos falta el template llamado page_create.html y utilizar un formulario que suba dichos campos.

UpdateView
++++++++++

Esta vista sirve para actualizar registros, hay que pasarle un pk para poder editar la página correcta.

* Editamos views.py:

.. code-block:: python
    :linenos:

    # Importamos el update:
    from django.views.generic.edit import UpdateView
    from django.urls import reverse_lazy
    from .models import Page

    # Ahora creamos la vista update:
    class PageUpdate(UpdateView):
        model = Page
        fields = ['title', 'content', 'order']
        # Ahora le pasamos el sufijo que tendrá la página (page_update_form.html):
        template_name_suffix = '_update_form'
    
        # Ahora vamos a retornar al formulario una vez terminada la edición esta vez necesariamente con un método específico de django:
        def get_success_url(self): # Le pasamos por argumenoto la id:
        return reverse_lazy('pages:update', args = [self.object.id]) + '?ok' # Le pasamos por parámetros un valor ok para verificarlo en el template

De este modo solo nos falta el archivo page_update.html y en la ruta pasarle un parámetro con el nombre <int:pk>, en el template ponemos un formulario tal cual como en CreateView.

DeleteView
++++++++++

Sirve para borrar entradas, funciona de un modo similar a UpdateView, veamos views.py:

.. code-block:: python
    :linenos:

    from django.views.generic.edit import DeleteView
    from django.urls import reverse_lazy
    from django.shortcuts import render

    from .models import Page

    # Creamos la vista delete:
    class PageDelete(DeleteView):
        model = Page
        success_url = reverse_lazy('pages:pages')

Con esto le pasamos a la ruta un parámetro tipo <int:pk> y crear el template DeleteView.as_view()


Pasarle un formulario a una CBV
+++++++++++++++++++++++++++++++

Para pasarle un formulario a un CBV hacemos lo siguiente en views.py:

.. code-block:: python
    :linenos:

    from django.views.generic.edit import CreateView
    from django.urls import reverse_lazy

    from django.shortcuts import render
    from .models import Page
    # Importamos el formulario de forms:
    from .forms import PageForm

    class PageCreate(CreateView):
        model = Page 
        form_class = PageForm # Asignamos el formulario que vamos a utilizar
        success_url = reverse_lazy('pages:pages')

Crear un nuevo contexto
+++++++++++++++++++++++

Este concepto se resume en la manera de exportar datos desde las vistas CBV al Template y este sería el modo:

.. code-block:: python
    :linenos: 

    from django.shortcuts import render
    from django.views.generic.base import TemplateView

    class HomePageView(TemplateView):
        template_name = 'core/home.html'
        # Podemos pasarle valores a la vista a través de un diccionario de contexto con un método específico:
        def get_context_data(self, **kwargs):
            # Cargamos del padre la estructura del diccionario:
            context = super().get_context_data(**kwargs)
            # Y ahora podemos grabar por ejemplo un título:
            context['title'] = 'Título de mi web'
            # La devolvemos al Template para que pueda usarlo:
            return context

Imagina ahora que queremos usar ese contexto en un título del template, pues escribimos ``<h1>{{titulo}}</h1>`` y listo.

Recuperar datos de POST o GET 
+++++++++++++++++++++++++++++

Para recuperar datos desde GET o POST utilizamos la función con su nombre que viene ya preparada en la clase superior:

.. code-block:: python
    :linenos: 

    from .models import Prueba
    from django.views.generic import TemplateView
    from .forms import ContactoForm 

    class RegistroView(TemplateView):
        template_name = 'nombre_de_tu_app/index.html'
        
        # Se utiliza la función predefinida llamada post o get con los parámetros que vemos:
        def post(self, request, *args, **kwargs):
            # guardamos el formulario en una variable con los datos rellenos:
            form = self.form_class(request.POST)
            # comprobamos que sea válido:
            if form.is_valid():
                # preparamos los datos para guardar:
                registro = form.save(commit=False)
                # podemos editar algun dato por el camino:
                registro.fecha_creacion(datetime.now)
                # y guardamos el registro en el modelo:
                registro.save()

                # regresamos a la página de vuelta:
                return redirect(reverse('home'))
            else:
                form = ContactoForm()

De este modo una vez recibe datos los almacena en el modelo.

Decoradores
***********

Los decoradores sirven para hacer modificaciones en las vistas, como por ejemplo definir si una url la puede ver solo usuarios registrados o si es del staff:

* Decoradores en CBV:

.. code-block:: python
    :linenos: 

    # Se le pasa el decorador a la clase directamente:
    @method_decorator(login_required, name='dispatch')
    class ProfileUpdate(TemplateView):
        template_name = 'registration/profile_form.html'

    # podemos definir si es un usuario registrado o si solo puede acceder el staff
    @method_decorator(staff_member_required, name='dispatch') # Para que el decorador de metodos sepa cual es el que tiene que decorar lo asignamos con un parámetro name
    class PageCreate(CreateView): 
        model = Page 
        form_class = PageForm 
        success_url = reverse_lazy('pages:pages')


* Añadimos lo siguiente al final de settings.py para definir hacia donde irá para inciar sesión:

.. code-block:: python
    :linenos: 

    # Este es el path al que queremos que redireccione:
    LOGIN_REDIRECT_URL = 'pages:pages'
    LOGOUT_REDIRECT_URL = 'home'


Middleware en Django  
####################

Los Middlewares se utilizan para controlar como se procesa la información, estos middlewares se ejecutan de forma global antes o despues de cada petición.
Por defecto django cuenta con al menos cuatro middlewares: SecurityMiddleware, SessionMiddleware, CommonMiddleware y AuthenticationMiddleware.
Los middlewares se declaran en **settings.py** en la constante **MIDDLEWARE**

* SecurityMiddleware: Intenta garantizar la seguridad en la aplicación evitanto ataques XSS.
* SessionMiddleware: Accede a la cookie de sesión y define donde se guardan las sesiones.
* CommomMiddleware: Se encarga de normalizar las direcciones añadiendo www o / al final.
* CsrfViewMiddleware: Sirve para garantizar que se cumple el CSRF_TOKEN.
* AuthenticationMiddleware: Sirve para conseguir el usuario de la petición y añadirlo al request.
* MessageMiddleware: Especialmente usado para mensajes flash, aunque ya se delegan sobre todo al Frontend.
* XFrameOptionMiddleware: Evita errores de X-Content o Iframes y ataques click-jacking


Crear Custom Middleware
***********************

1. Dentro de una App se crea un archivo **middleware.py** (cada app tiene su propio archivo o también se puede sacar en la raiz):
2. Este sería el comportamiento base de un middleware:
   
.. code-block:: python 
    :linenos:

    # Se importa el modulo que llama a las peticiones:
    from typing import Callable

    # Se crea una clase para el middleware:
    class NombreMiddleware:
        # en el constructor recibirá la respuesta con Callable:
        def __init__(self, get_response: Callable):
            # guardamos en el atributo de clase la petición:
            self.get_response = get_response


        # se genera el metodo de llamada:
        def __call__(self, request):
            # guardamos la respuesta de la petición:
            response = self.get_response(request)


            return response 

3. Activar middleware en **settings.py**:
   
.. code-block:: python 
    :linenos:

    MIDDLEWARE = [
        'django.middleware.security.SecurityMiddleware',
        'django.contrib.sessions.middleware.SessionMiddleware',
        'django.middleware.common.CommonMiddleware',
        'django.middleware.csrf.CsrfViewMiddleware',
        'django.contrib.auth.middleware.AuthenticationMiddleware',
        'django.contrib.messages.middleware.MessageMiddleware',
        'django.middleware.clickjacking.XFrameOptionsMiddleware',
        'core.middleware.NombreMiddleware' # añadir el nuevo middleware creado
    ]

4. Ahora se va a crear un custom middleware que filtre direcciones IP:

.. code-block:: python 
    :linenos:

    # instalamos para el ejemplo django-ipware:
    from ipware import get_client_ip
    from django.http import HttpResponse

    # se asigna el nombre del middleware:
    class IpValidMiddleware:
        def __init__(self, get_response):
            self.get_response = get_response
            # Creamos la lista negra de ips:
            self.black_list = ['127.0.0.1']


        def __call__(self, request):
            response = self.get_response(request)

            # recuperamos la ip de la request en dos variables (obligatorio aunque se use solo una):
            ip, is_routable = get_client_ip(request)

            # comprobamos si esta en lista negra y cambiamos la response en caso de que sea así:
            if ip in self.black_list:
                # tiramos de error 404:
                response = HttpResponse('Bad request', status=404)

            return response 

Templates
#########

Las plantillas son las que muestran el sitio web mediante etiquetas HTML y también imprimen resultados que gestiona el servidor con **Template Tags**.

* Para comenzar a utilizar templates creamos una carpeta llamada **templates** en el interior de la carpeta de nuestra app y dentro de templates otro directorio con el nombre de la app. (nombre_de_tu_app/templates/nombre_de_tu_app)
* Ahora creamos un archivo html por ejemplo home.html que cargará la página de inicio:

.. code:: html

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Página de prueba</title>
    </head>
    <body>
        <h1>Bienvenido a mi página de prueba</h1>
        <h2>Aquí haremos pruebas varias</h2>
    </body>
    </html>

.. attention::
    Para que funcione debemos tener listo el render que devuelve este archivo html y al abrir el navegador se mostrará correctamente.

Template Tags
*************

Los Template Tags son un tipo de etiquetas especiales en Django que se utilizan en las plantillas para ejecutar respuestas backend.

Estas etiquetas suelen tener dos tipos de estructuras: ``{% instrucción %}`` o ``{{ datos }}`` según el tipo de tarea que vayamos a ejecutar.

Template tag base
+++++++++++++++++

Una buena práctica para no repetir código en plantillas es coger todo el contenido común y almacenarlo en una plantilla base:

* Entramos en la carpeta ``nombre_de_tu_app/templates/nombre_de_tu_app`` y creamos un archivo llamado base.html donde copiaremos el contenido común:
* Ahora vamos a quitar el código de home.html y lo pegamos en base.html:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Página de prueba</title>
    </head>
    <body>
        <h1>Bienvenido a mi página de prueba</h1>
        <h2>Aquí haremos pruebas varias</h2>

        <!-- Justo aquí enmedio utilizaremos el template tag base para extender una parte de otra plantilla  -->
        {% block cuerpo %}{% endblock %}

        <footer>Piptocode, hecho con cariño y para amantes de la programación</footer>
    </body>
    </html>

* Finalmente vamos a usar home.html como una plantilla de extensión con su propio código:

.. code-block:: html
    :linenos:


    <!-- llamamos el template tag con extends: -->
    {% extends 'nombre_de_tu_app/base.html' %}

    <!-- Utilizamos el block content para definir donde irá el contenido de la pagina home respecto a la plantilla base -->
    {% block cuerpo %}
        <h2>Portada</h2>
        <p>Esta es la página principal del sitio y utiliza una plantilla base para el contenido estático</p>
    {% endblock %}

Siguiendo este patrón podemos reutilizar el código base de la web en nuevas páginas o incluso nuevas apps de Django.

.. note::
    En relación a extends podemos cargar cualquier plantilla a modo de fragmento, por ejemplo para ordenar css inline, un sidebar u otros elementos dinámicos que
    hagan falta en el día a día. El objetivo es reducir el número de lineas HTML aumentando la cantidad de plantillas identificables y reutilizables.

Template tag url
++++++++++++++++

Con este template tag podemos establecer vínculos a otras páginas enlazando los names del archivo de rutas.

¿recuerdas las líneas que escribimos dentro de urls.py? ``path('', views.home, name = 'home'),``, el path recibe tres valores, la ruta del navegador, la ubicación de la vista y por último el nombre de la ruta,
este tercer valor es el que utilizamos con el template tag **url**

* vamos a editar el archivo base.html para añadir un menú de navegación:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Página de prueba</title>
    </head>
    <body>
        <h1>Bienvenido a mi página de prueba</h1>
        <h2>Aquí haremos pruebas varias</h2>

        <nav>
            <!-- el template tag url lo usamos dentro del atribut href de un hipervínculo: -->
            <a href="{% url 'home' %}">Índice</a> <!-- lleva entre comillas simples el nombre de la ruta que vamos a vincular -->
            <a href="">Sobre mí</a>
            <a href="">Contacto</a>
        </nav>

        {% block cuerpo %}{% endblock %}

        <footer>Piptocode, hecho con cariño y para amantes de la programación</footer>
    </body>
    </html>

.. attention::
    Si añadimos un name que no existe en el archivo de rutas Django lanzará una pantalla de error en lugar de la plantilla.

Template tag static
+++++++++++++++++++

Con este template tag vamos a cargar archivos estáticos de nuestra web, entre ellos están las imágenes, videos, hojas de estilo y javascript.

* Siguiendo una práctica convencional creamos una carpeta llamada **static** dentro del directorio de la app y dentro de static una carpeta con el nombre de la app: ``nombre_de_tu_app/static/nombre_de_tu_app``.
* Dentro de la última carpeta podemos ir añadiendo carpetas básica como css, js e img para ir añadiendo los archivos correspondientes.
* Ahora podemos utilizar archivos estáticos dentro de dichas rutas:

.. code-block:: html
    :linenos:

    <!-- cargamos el template tag static -->
    {% load static %}

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Página de prueba</title>
        <!-- ahora si queremos cargar un archivo estatico como una hoja de estilo lo hacemos así: -->
        <link rel="stylesheet" href="{% static 'nombre_de_tu_app/css/estilos.css' %}">
    </head>
    <body>
        <h1>Bienvenido a mi página de prueba</h1>
        <h2>Aquí haremos pruebas varias</h2>

        <nav>
            <a href="{% url 'home' %}">Índice</a> 
            <a href="">Sobre mí</a>
            <a href="">Contacto</a>
        </nav>

        {% block cuerpo %}{% endblock %}

        <footer>Piptocode, hecho con cariño y para amantes de la programación</footer>
    </body>
    </html>

Template tag de datos 
+++++++++++++++++++++

Los template tags de datos muestran información que enviamos desde la vista al template.

* Si nos vamos a views.py para añadir un dato:

.. code-block:: python
    :linenos:

    from django.shortcuts import render 

    def home(request):
        # creamos una variable:
        nombre = "Guillermo Granados Gómez"        
        return render(request, 'nombre_de_tu_app/home.html', {'nombre':nombre}) # devolvemos la información en un diccionario

* Ahora que tenemos un dato, podemos mostrarlo en cualquier template de nuestra app:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Página de prueba</title>
    </head>
    <body>     <!-- Ahora podemos mostrar el dato usando su clave -->
        <h1>Bienvenido a la web de {{ nombre }}</h1>
        <h2>Aquí haremos pruebas varias</h2>

        <nav>
            <a href="{% url 'home' %}">Índice</a> 
            <a href="">Sobre mí</a>
            <a href="">Contacto</a>
        </nav>

        {% block cuerpo %}{% endblock %}

        <footer>Piptocode, hecho con cariño y para amantes de la programación</footer>
    </body>
    </html>

Template tag for
++++++++++++++++

En los templates de Django para hacer un bucle for lo hacemos del siguiente modo:

* Para empezar necesitamos un diccionario al que acceder desde views.py:

.. code-block:: python
    :linenos: 

    from django.shortcuts import render 

    def home(request):
        # creamos un diccionario:
        personas = [
            {'nombre': 'Pepe', 'edad': 26},
            {'nombre': 'Antonio', 'edad': 38},
            {'nombre': 'María', 'edad': 37}
        ]        
        return render(request, 'pruebauno/home.html', {'personas':personas}) # devolvemos la información en un diccionario

* Y ahora podemos recorrer el diccionario en nuestro template con el template tag for:

.. code-block:: html
    :linenos:

    <h3>Listado de Clientes</h3>
    <ul>
        {% for persona in personas %} <!-- Abrimos el bucle for en el template -->
            <li>Nombre: {{ persona.nombre }}, Edad: {{ persona.edad }}</li> <!-- Creamos el elemento que va a iterar en la lista imprimiendo los valores -->
        {% endfor %} <!-- Y lleva una llave de cierre -->
    </ul>

Template tag if
+++++++++++++++

Con el template tag if podemos establecer condiciones dentro de los templates, retomando el ejemplo de for vamos a pintar de verde uno de los registros:

.. code-block::
    :linenos:

    <h3>Listado de Clientes</h3>
    <ul>
        {% for persona in personas %} 
            <!-- Si en nombre se encuentra Antonio lo pintaremos de verde: -->
            <li {% if 'Antonio' in persona.nombre  %} style="color: green" {% endif %}>
                Nombre: {{ persona.nombre }}, Edad: {{ persona.edad }}
            </li> 
        {% endfor %} 
    </ul>

Crear template tags customizados
********************************
Son muy útiles para cargar etiquetas con contenido específico que se pueda usar en plantillas.

Como preparar el archivo de templatetags:
1. Dentro de una app como **core** crear carpeta llamada **templatetags**.
2. Dentro de **templatetags** se crea un archivo con una colección de tags **components.py**:


Simple tag
++++++++++

Devuelve información pura como números, cadenas, listados, objetos, diccionarios.

.. code-block:: python 
    :linenos:

    # se importa la librería template:
    from django import template 

    # se registra la librería:
    register = template.Library()

    # y se van creando cada una de las tags:
    @register.simple_tag 
    def get_title():
        return 'bienvenidos a mi página'

- Cogemos un template y lo aplicamos:

.. code-block:: html 
    :linenos:

    <!-- Se carga el módulo con los template tags: -->
    {% load components %}
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <!-- hay que crear una variable a partir del simple_tag: -->
        {% get_title as title %}
        <!-- Utilizar la variable: -->
        <h1>{{ title }} </h1>
        <form method="POST">
            {{ form.as_p }}
            {% csrf_token %}
            <button type="submit">Iniciar sesión</button>
        </form>
        <hr />
        <a href="{% url 'register' %}">Crear usuario</a>
    </body>
    </html>

Filter tags
+++++++++++
Los filter tags se utilizan para filtrar datos en otros tags, y pueden ser simples o compuestos:

- Se reutiliza el archivo **components.py** (aunque se puede crear uno nuevo):

.. code-block:: python 
    :linenos:

    # se puede registrar un filtro sencillo:
    @register.filter
    def upper(value):
        return value.upper()

    # o un filtro con hasta dos parámetros:
    @register.filter 
    def change_language(value, arg):
        
        if arg == 'english':
            value = 'Welcome to my site'
        if arg == 'français':
            value = 'bienvenu à mon site'

        return value

- Estos filtros son utilizados en los templates así:

.. code-block:: html 
    :linenos:

    {% load components %}
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        {% get_title as title %}
        <!-- Utilizar un filtro simple: -->
        <h1>{{ title|upper }} </h1>
        <!-- Utilizar filtros compuestos: -->
        <h2>{{ title|change_language:'english' }} </h2>
        <h2>{{ title|change_language:'français' }} </h2>
        <form method="POST">
            {{ form.as_p }}
            {% csrf_token %}
            <button type="submit">Iniciar sesión</button>
        </form>
        <hr />
        <a href="{% url 'register' %}">Crear usuario</a>
    </body>
    </html>
    

Modelos
#######

Los modelos en Django sirven para crear estructuras de bases de datos con las que podremos interactuar gracias a sus QuerySets.

En cada app que creamos tenemos un archivo models.py, vamos a editar uno para ver que campos tiene:

.. code-block:: python
    :linenos:

    # Los modelos se crean usando una clase que hereda de la superclase Model:
    class Prueba(models.Model):
        autor = models.ForeignKey(User, verbose_name = "Autor", on_delete = models.CASCADE) # El primero es una clave foranea para vincular otras tablas como la de usuarios que viene por defecto
        titulo = models.CharField(max_length=200, verbose_name="Título") # CharField es un campo de tipo texto, el primer parámetro que le pasamos define el tamaño máximo y es obligatorio, el segundo es opcional y sirve para todos los campos (verbose_name define como se mostrará la label del panel de administración)
        descripcion = models.TextField(verbose_name="Descripción") # Con TextField tenemos una caja de texto sin límite de rango.
        link = models.URLField(null=True, blank=True, verbose_name="Enlace") # URLField nos permite agregar una url válida. 
        fecha_creacion = models.DateTimeField(auto_now_add = True) # crea un campo de fecha y hora, podemos pasarle la fecha de una publicación de forma automática con auto_now_add.
        fecha_edicion = models.DateField(auto_now = True) # aquí tenemos otra variante, en primer lugar DateField guarda solo la fecha y opcionalmente podemos decir que lo haga cuando editamos la entrada con auto_now.

        
        # opcionalmente podemos usar la clase Meta para editar valores que nos servirán para mostrar los datos en el panel de administración:
        class Meta: 
            verbose_name = "prueba" # Nombre de la tabla en el panel.
            verbose_name_plural = "pruebas" # nombre en plural.
            ordering = ["-fecha_creacion"] # Orden prioritario, en este caso por fecha descenciente.

        # Con esta función podemos retornar en el panel de administración un valor de referencia
        def __str__(self):
            return self.titulo

.. attention::
    Tienes que tener registrada tu app en el apartado INSTALLED_APPS o sino dará error a la hora de migrar la base de datos.

.. hint::
    Los parámetros comunes para prácticamente todos los campos son verbose_name (nombre que muestra), blank (True o False para permitir el campo vacío), null (True o False para permitir campo nulo)

Cargar imágenes en modelos con Pillow
*************************************

Pillow es una librería de Python que se utiliza para el tratamiento de imágenes. En Django la podemos utilizar para gestionar la carga de estas.

* Lo primero que tenemos que hacer es instalar Pillow en nuestro entorno: ``pip install Pillow``
* Ahora vamos a editar nuestra clase de models.py:

.. code-block:: python
    :linenos:

    class Prueba(models.Model):
        autor = models.ForeignKey(User, verbose_name = "Autor", on_delete = models.CASCADE)
        titulo = models.CharField(max_length=200, verbose_name="Título") 
        descripcion = models.TextField(verbose_name="Descripción")
        fecha_creacion = models.DateTimeField(auto_now_add = True)
        fecha_edicion = models.DateField(auto_now = True)
        # con ImageField podemos subir una imagen a un directorio que elijamos:
        imagen = models.ImageField(upload_to="imagenes/")

        class Meta: 
            verbose_name = "prueba"
            verbose_name_plural = "pruebas" 
            ordering = ["-fecha_creacion"]

        def __str__(self):
            return self.titulo

* Para poder subir las imágenes tenemos que añadir en settings.py la siguiente línea:

.. code-block:: python
    :linenos:

    MEDIA_URL = '/media/'
    MEDIA_ROOT = os.path.join(BASE_DIR, 'media')

* Finalmente nos vamos al archivo de rutas principal (el que se encuentra dentro de la carpeta con el nombre de tu proyecto) y añadimos la siguiente configuración para poder visualizar las imágenes desde el panel:

.. code-block:: python
    :linenos: 

    from django.contrib import admin
    from django.urls import path
    from nombre_de_tu_app import views 
    # Importamos la librería settings:
    from django.conf import settings

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', views.home, name = 'home'), 
    ]

    # Cargamos la ruta siempre que este en modo debug:
    if settings.DEBUG:
        from django.conf.urls.static import static
        urlpatterns += static(settings.MEDIA_URL, document_root = settings.MEDIA_ROOT)

De este modo y mientras no estemos en producción podremos visualizar las imágenes desde el panel de administrador para probar que funciona correctamente.

Modelo de muchos a muchos
*************************
En base de datos un modelo de muchos a muchos nos sirve para establecer una relación entre múltiples componentes de ambas tablas, como por ejemplo crear una lista de categorías:
* Sería algo así nuestro modelo:

.. code-block:: python
    :linenos:

    # primero creamos un modelo para guardar las categorías:
    class Category(models.Model):
        name = models.CharField(max_length = 100, verbose_name="Nombre")
        created = models.DateTimeField(auto_now_add=True, verbose_name="Fecha de creación")
        updated = models.DateTimeField(auto_now=True, verbose_name="Fecha de edición")

    class Meta:
        verbose_name = "categoria"
        verbose_name_plural = "categorias"
        ordering = ["-created"]

    def __str__(self):
        return self.name

    class Prueba(models.Model):
        autor = models.ForeignKey(User, verbose_name = "Autor", on_delete = models.CASCADE)
        titulo = models.CharField(max_length=200, verbose_name="Título") 
        descripcion = models.TextField(verbose_name="Descripción")
        fecha_creacion = models.DateTimeField(auto_now_add = True)
        fecha_edicion = models.DateField(auto_now = True)
        imagen = models.ImageField(upload_to="imagenes/")
        # Ahora vamos a recuperar todas las categorías en la tabla que queremos usar:
        categorias = models.ManyToManyField(Category, verbose_name="Categorías")

        class Meta: 
            verbose_name = "prueba"
            verbose_name_plural = "pruebas" 
            ordering = ["-fecha_creacion"]

        def __str__(self):
            return self.titulo

Ahora podemos generar categorías incluso desde la tabla de pruebas cuando ingresamos o editamos un registro.

Generar modelo y migrar la base de datos
****************************************

Cuando creamos un modelo nuevo lo primero que tenemos que hacer es maquetar la estructura que vamos a migrar cada vez que generemos la base de datos:

* Para crear el modelo de las tablas de una app ejecutamos ``python manage.py makemigrations``.
* Si todo va bien, migramos la base de datos con ``python manage.py migrate``
* Para comprobar el estado de las migraciones se ejecuta: ``python manage.py showmigrations``


ORM de Django y sus QuerySets
#############################

Los QuerySets son listas de objetos que se recuperan de la base de datos de forma similar a una consulta SQL. Existen una serie de
sentencias trabajar con estos datos.

* Lo primero que vamos a hacer es ejecutar ``python manage.py shell``, esto abrirá la consola del ORM.
* Una vez arrancada lo primero que tenemos que hacer para las pruebas es importar un modelo ``from nombre_de_tu_app import Prueba``

Ahora vamos a conocer los distintos comandos para realizar QuerySets:

* ``Prueba.objects.all()``: devuelve todos los registros de la tabla Prueba
* ``Prueba.objects.create(titulo="Ejemplo", descripcion="esto es una entrada")``: Genera un nuevo registro en la tabla Prueba, ten en cuenta que esten todos los campos o sino que puedan estar en blanco (blank=True)
* ``Prueba.objects.filter(titulo__contains = 'Ejemplo')``: Permite filtrar las tablas para devolver solo aquellos que contienen la palabra clave, si quitamos __contains solo obtendrá los que tengan exactamente y únicamente esa palabra.
* ``Prueba.objects.filter(titulo__contains = 'Ejemplo').first()``: Añadiendo el metodo first trae solo el primer registro.
* ``Prueba.objects.count()``: Devuelve el número total de registros que hay en la tabla.
* ``Prueba.objects.order_by('fecha_creacion')``: Permite ordenar los registros de la tabla nuevamente cuando se cargan en la vista.
* ``Prueba.objects.delete(titulo="Ejemplo")``: Elimina un valor según el campo que hayamos elegido para buscarlo

Para salir de la consola ORM escribimos ``exit()`` y pulsamos intro

.. hint::
    Podemos encadenar algunos querysets por ejemplo recuperar todos los datos y ordenarlos por fecha: ``Prueba.objects.all().order_by('-fecha_creacion')``

.. hint::
    Para filtrar por campos de una tabla relacionada se usa doble guión bajo en la clave foranea: ``Videojuego.objects.filter(Consola__marca:'Sega')``

 
 
Realizar QuerySets desde vista y pasarlos a template
****************************************************

Es algo muy común, y es que cuando trabajamos con vistas FBV es el método estandar, para trabajar datos del modelo en la vista lo hacemos del siguiente modo, editamos views.py:

.. code-block:: python
    :linenos:

    from django.shortcuts import render
    # Importamos el Modelo:
    from . import Prueba 

    def home(request):
        # creamos una variable:
        cosas = Prueba.objects.all()      
        return render(request, 'nombre_de_tu_app/home.html', {'cosas':cosas}) # pasamos el queryset por una variable y este lo trata en el template como un diccionario.

Formularios
###########

En Django podemos crear formularios individuales y reutilizables.

Crear un formulario básico
**************************

.. code-block:: python
    :linenos: 

    # importamos la librería forms:
    from django import forms
    # Esto se importa opcionalmente si usamos fechas:
    import datetime

    # Creamos un formulario utilizando una clase que hereda de forms:
    class ContactoForm(forms.Form):
        # Cada campo recibe un tipo de dato con un label que es la etiqueta html y si es requerido:
        nombre = forms.CharField(label="Nombre", required=True) # CharField es para campo de texto
        email = forms.EmailField(label="Correo", required=True) # Email para correos 
        url = forms.URLField(initial='https://', label="Web") # Este sirve para insertar una url y le podemos pasar un valor inicial
        fecha_nacimiento = forms.DateField(initial=datetime.date.today) # este sirve para añadir una fecha y podemos pasarle la de hoy si importamos 'datetime'
        contenido = forms.CharField(label="contenido", required=True, widget=forms.Textarea) # con widget le cambiamos el aspecto directamente para que sea un textarea

Crear un formulario usando su modelo
************************************

Este otro método es mas fácil de personalizar a mi parecer, y organiza mejor todo ademas de permitir elegir que campos se mostrarán del modelo de datos, así pues editamos forms.py:

.. code-block:: python
    :linenos: 

    from django import forms
    from .models import Prueba

    class PruebaForm(forms.ModelForm):
        class Meta:
            # elegimos el modelo de datos:
            model = Prueba 
            # Elegimos los campos que se mostrarán de dicho modelo:
            fields = ['titulo', 'email', 'contenido']
            # añadimos widgets para configurar el diseño de los campos del formulario:
            widgets = {                 # podemos pasarle el atributo al input que queramos.
                'titulo': forms.TextInput(attrs={'class':'formulario'}), # Le asignamos la clase formulario
                'contenido': forms.Textarea(attrs={'class':'formulario'}),
                'email': forms.EmailInput(attrs={'class':'formulario'})
            }
            # Así se puede esconder opcionalmente las labels o cambiar su texto:
            labels = {
                'title':'', 'order':'', 'content':''
            }

    De este modo tenemos otra forma de sacar los formularios, lo demás es todo igual.

Crear formulario y aceptar parámetros para su configuración
***********************************************************

Este tercer método permite recibir parámetros al formulario de modo que podamos configurar ciertas características del mismo:

.. code-block:: python
    :linenos: 

    class PublisherForm(forms.ModelForm):

    # tenemos un campo con su uso más avanzado:
    name = forms.CharField(
        label='Nombre',
        max_length=255,
        required=False,
        widget=forms.TextInput(
            attrs={'class': 'form-control'}
        )
    )

    # En el meta rescatamos el Modelo y los campos:
    class Meta:
        model = Publisher
        fields = ('name', )

    # Y ahora se define un init que recibirá los args y kwargs, estos segundos los usaremos para comprobar que se recibe:
    def __init__(self, *args, **kwargs):
        # se crean las variables con los argumentos posibles:
        self.required = kwargs.pop('required', None)
        self.readonly = kwargs.pop('readonly', None)
        self.disabled = kwargs.pop('disabled', None)
        super().__init__(*args, **kwargs)

        # se comprueba si se reciben y se genera el comportamiento de cada uno:
        if self.required:
            if self.required == 'all':
                for x in self.fields:
                    self.fields[x].widget.attrs['required'] = True
            else:
                for field in self.required:
                    self.fields[field].widget.attrs['required'] = True

        if self.readonly:
            if self.readonly == 'all':
                for x in self.fields:
                    self.fields[x].widget.attrs['readonly'] = True
            else:
                for field in self.readonly:
                    self.fields[field].widget.attrs['readonly'] = True

        if self.disabled:
            if self.disabled == 'all':
                for x in self.fields:
                    self.fields[x].widget.attrs['disabled'] = True
            else:
                for field in self.disabled:
                    self.fields[field].widget.attrs['disabled'] = True

    De este modo se tiene un control universal de cada campo.

    Si queremos establecer un campo del formulario como requerido:
    * form = PublisherForm(required = ['Nombre'])

Utilizar un formulario
**********************

Si queremos usar un formulario lo importamos a la vista del siguiente modo.

.. code-block:: python
    :linenos:

    from django.shortcuts import render
    # importamos el formulario:
    from .forms import ContactoForm 

    def contacto(request):
        form = ContactoForm() # cargamos el formulario en una variable
        return render(request, 'nombre_de_tu_app/contacto.html', {'form': form}) # finalmente lo pasamos al template.

* Para cargar el formulario en la vista editamos el archivo html y lo añadimos:

.. code:: html

    <form method="POST">
        {% csrf_token %} <!-- le pasamos el token -->
        {{formulario.as_p}} <!-- pasamos el formulario y lo formateamos en parrafos, si usamos as_table se formateará en tabla -->
        <button type="submit">Enviar mensaje</button><!-- no olvides el botón submit -->
    </form>
    <!-- por último podemos depurar lo que envía el formulario con el siguiente tag: -->
    {{request.POST}}

.. note:: 
    Si queremos utilizar los campos sueltos para un mayor control del front se llaman como atributos de un objeto: ``{{ formulario.nombre }}`` 
    Esto carga el input, los label y cualquier otra propiedad relacionada con el campo.

Validar un formulario 
*********************

El formulario se valida una vez enviado a la vista antes de ser guardado o gestionado por la base de datos, veamoslo en views.py:

.. code-block:: python
    :linenos:

    from django.shortcuts import render
    from .forms import ContactoForm 

    def contacto(request):
        form = ContactoForm() 

        # comprobamos que hemos recibido una petición post:
        if request.method == "POST":
            # le pasamos los datos a la plantilla del formulario:
            form = ContactoForm(data=request.POST)

            # validamos el formulario y si es correcto guardamos los datos en cada campo:
            if form.is_valid():
                # preparamos los datos para guardar:
                registro = form.save(commit=False)
                # podemos editar algun dato por el camino:
                registro.fecha_creacion(datetime.now)
                # y guardamos el registro en el modelo:
                registro.save()

                # regresamos a la página de vuelta:
                return redirect(reverse('home'))
            else:
                form = ContactoForm()

        # si no se ha recibido ninguna petición post se carga como tal:
        return render(request, 'nombre_de_tu_app/contacto.html', {'form': form})


Usuarios en Django
##################

Django cuenta con modelos integrados para gestionar usuarios y permisos

Users o usuarios
****************

Cargar librerías
++++++++++++++++

- Los metodos de usuarios se importan desde ``django.contrib.auth`` los metodos ``authenticate``, ``users``, ``login``, ``logout``
- El modelo de usuarios se importa desde ``django.contrib.auth.models`` en donde se encuentran ``User`` y ``Group``
- Los formularios de usuarios se importan desde ``django.contrib.auth.forms`` en donde se encuentran ``UserCreationForm`` y ``AuthenticationForm``


Se pueden llamar desde las vistas o los templates con ``request.user`` para hacer validaciones o simplemente mostrarlo.

También se pueden consultar en la bases de datos con el ORM:
- ``User.objects.create_user(username, password, email)``: Permite crear un nuevo usuario.
- ``User.objects.get(username).set_password('password')``: permite cambiar la contraseña. 

Sistema de autenticación 
++++++++++++++++++++++++
- Preparando la ruta (urls.py):

.. code-block:: python 
    :linenos:

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', views.panel, name='panel'),
        path('register/', views.register, name='register'),
        path('login/', views.start, name='login'),
        path('logout/', views.close, name='logout'),
    ]

- Preparando la vista (views.py):

.. code-block:: python
    :linenos:

    from django.shortcuts import render, redirect, HttpResponse
    # importar los metodos del auth necesarios:
    from django.contrib.auth import authenticate, login, logout
    # se importa el formulario de autenticación:
    from django.contrib.auth.forms import AuthenticationForm, UserCreationForm 


    def panel(request):
        # preparamos la respuesta que por defecto redirige a login: 
        response = redirect('login')

        # comprobamos que se ha iniciado sesión y cambiamos la respuesta de ser así:
        if request.user.is_authenticated:
            response = HttpResponse('<h1>Hola ' + request.user.username + '!</h1><a href="logout/">Cerrar sesión</a>')

        return response


    def register(request):
        # cargamos el formulario de creación de usuarios:
        form = UserCreationForm()
        # cargamos la respuesta:
        response = render(request, 'core/register.html', {'form': form})

        # Se valida y se genera el nuevo usuario:
        if request.method == "POST":
            form = UserCreationForm(data=request.POST)

            if form.is_valid():
                user = form.save()
                # Se puede aprovechar para hacer login automáticamente:
                if user is not None:
                    login(request, user)
                    response = redirect('panel')

        return response


    def start(request):
        # se carga el formulario de autenticación:
        form = AuthenticationForm()
        # preparamos la respuesta:
        response = render(request, "core/login.html", {'form': form})

        # si llega algo se intentará iniciar sesión:
        if request.method == 'POST':
            form = AuthenticationForm(data=request.POST)

            if form.is_valid():
                username = form.cleaned_data['username']
                password = form.cleaned_data['password']

                # se verifica que el usuario existe o no:
                user = authenticate(username=username, password=password)

                # si existe se inicia sesión:
                if user:
                    login(request, user)
                    response = redirect('panel')

        return response
        

    def close(request):
        # realizar logout:
        logout(request)
        return redirect('panel')


- Preparando plantilla para login (login.html):

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
    </head>
    <body>
        <form method="POST">
            {{ form.as_p }}
            {% csrf_token %}
            <button type="submit">Iniciar sesión</button>
        </form>
        <hr />
        <a href="{% url 'register' %}">Crear usuario</a>
    </body>
    </html>

- Preparamos plantilla para el registro (register.html):

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
    </head>
    <body>
        <form method="POST">
            {{ form.as_p }}
            {% csrf_token %}
            <button type="submit">Registrar usuario</button>
        </form>
        <hr />
        <a href="{% url 'login' %}">Iniciar sesión</a>
    </body>
    </html>

Cambiar usuario por email
+++++++++++++++++++++++++
Se puede reemplazar el campo para iniciar sesión por otro valor como un DNI o también el Email:

- Abstaer el formulario para usar email (forms.py):

.. code-block:: python
    :linenos:

    from django import forms
    # se importan los formularios de creación y autenticación para abstraer:
    from django.contrib.auth.forms import UserCreationForm, AuthenticationForm
    # se importa el modelo user:
    from django.contrib.auth.models import User

    # Extender un nuevo formulario a partir del original:
    class CreationWithEmail(UserCreationForm):
        # se recupera el campo username y se cambia su formato:
        username = forms.EmailField(label='Correo electrónico')

        class Meta:
            model = User 
            fields = ['username', 'password1', 'password2']


    # hacemos lo mismo con authentication:
    class AuthenticationEmail(AuthenticationForm):
        username = forms.EmailField(label='Correo electrónico')

        class Meta:
            model = User 
            fields = ['username', 'password1']

- Implementar formularios en las vistas de login y register (views.py):

.. code-block:: python 
    :linenos:
    
    from django.shortcuts import render, redirect, HttpResponse
    from django.contrib.auth import authenticate, login, logout
    # se reemplazan los forms de auth por los recien creados:
    from .forms import CreationWithEmail, AuthenticationEmail


    def register(request):
        # Reemplazamos el formulario:
        form = CreationWithEmail()
        response = render(request, 'core/register.html', {'form': form})

        if request.method == "POST":
            # Reemplazamos el formulario:
            form = CreationWithEmail(data=request.POST)

            if form.is_valid():
                user = form.save()
                
                if user is not None:
                    login(request, user)
                    response = redirect('panel')

        return response


    def start(request):
        # Reemplazamos el formulario:
        form = AuthenticationEmail()
        response = render(request, "core/login.html", {'form': form})

        if request.method == 'POST':
        # Reemplazamos el formulario:
            form = AuthenticationEmail(data=request.POST)

            if form.is_valid():
                username = form.cleaned_data['username']
                password = form.cleaned_data['password']

                user = authenticate(username=username, password=password)

                if user:
                    login(request, user)
                    response = redirect('panel')

        return response

Groups o grupos
***************

Los grupos se usan para agrupar permisos con determinados usuarios.


Panel de administración
#######################

El panel de Administración de Django es un modelo CRUD ya definido por defecto con todo el Scaffold del sistema login preparado por defecto.

Puesta en marcha
****************

Para poner en marcha el panel tenemos que hacer un par de cosas en consola:

* Primero tenemos que crear todo el Scaffold ejecutando ``python manage.py migrate``
* Después ejecutamos ``python manage.py createsuperuser`` para generar un nuevo superusuario.

Ahora ya podemos acceder al panel de administración desde la ruta ``localhost:8000/admin``

Mostrar datos de nuestros modelos
*********************************

El panel de Administración solo dispone por defecto de las tablas de usuarios. Pero si hemos creado un modelo debemos implementarlo,
para ello en la carpeta de nuestra app veremos un archivo admin.py el cual editamos:

.. code-block:: python
    :linenos: 

    from django.contrib import admin

    # Importamos el modelo:
    from .models import Prueba

    # Registramos en el panel el modelo:
    admin.site.register(Prueba)

De este modo podremos leer, editar, borrar y añadir registros a esta tabla de nuestra app.

Personalizar titulos de las Apps 
********************************

En el panel de administración vemos que las tablas se irán dividiendo en apartados según su app, si tenemos varias apps veremos que cada
tabla esta dentro de apartados. Podemos cambiar el título de estos apartados accediendo a nuestra app y editando el archivo app.py:

.. code-block:: python
    :linenos: 

    from django.apps import AppConfig


    class nombre_de_tu_appConfig(AppConfig):
        name = 'nombre_de_tu_app'

        # Podemos asignarle un nombre que veremos en el panel:
        verbose_name = 'App de Prueba'

* Para que esto funcione tenemos que exportar dicha configuración a settings.py:
 
.. code-block:: python
    :linenos: 

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'nombre_de_tu_app.apps.nombre_de_tu_appConfig' # cambiamos el nombre de la app por su clase configuradora.
    ]

Personalizar tablas
*******************

Cuando accedemos a una tabla podemos ver una lista con todos los títulos o el valor que hayamos devuelto en el modelo. Pero podemos modificar su comportamiento
editando el archivo admin.py:

.. code-block:: python
    :linenos:

    from django.contrib import admin
    from .models import Prueba

    # Creamos una clase que se encargará de editar las configuraciones de nuestro panel:
    class PruebaAdmin(admin.ModelAdmin):
        # con esta tupla definimos los campos que serán de solo lectura cuando abramos un registro.
        readonly_fields = ('fecha_creacion', 'fecha_edicion')
        # Con list_display definimos que campos se mostrarán en el listado:
        list_display = ('titulo', 'autor', 'descripcion', 'fecha_creacion')
        # Aquí también podemos establecer el orden de lista:
        ordering = ('fecha_creacion', 'titulo')

        # Opcionalmente podemos cambiar la jerarquía de los breadcums para que se muestren por fecha de publicación:
        date_hierarchy = 'fecha_publicacion'

        # Filtrar también los datos que se muestran en la barra lateral derecha:
        list_filter = ('autor__username', 'fecha_creacion')

    admin.site.register(Prueba, PruebaAdmin)


Cambiar título al panel
***********************

Para cambiar el título que se muestra en el panel es tan sencillo como irnos a urls.py principal y al final del archivo añadir:

.. code-block:: python
    :linenos: 

    # Cambiar el título:
    admin.site.site_header = 'Mi Sitio web'
    
    # Cambiar el subtítulo: 
    admin.site.index_title = 'Panel de Administración'
    
    # cambiar texto de la pestaña de navegación:
    admin.site.site_title = 'Mi sitio web dedicado a Django!!!'

Enviar Emails
#############

libreria send_email() send_mass_email() en HTML también 

...

https://docs.djangoproject.com/en/4.0/topics/email/