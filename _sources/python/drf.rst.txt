Framework: Django Rest Framework
================================
 
.. image:: /logos/logo-django-rest.png
    :scale: 75%
    :alt: Logo HTML5
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Esta es la documentación que he recopilado para trabajar con Django, un framework basado en Python que sirve para desarrollar aplicaciones web.
 
.. contents:: Índice 
 
Primeros Pasos
##############
  
Crear un proyecto Django 
************************

* Lo primero que vamos a hacer es crear un entorno virtual.
* Luego instalamos Django ``pip install django``
* Creamos un projecto en Django ``django-admin startproject prueba_api``
* Ejecutamos el servidor para ver que se ha creado correctamente ``python manage.py runserver``

Instalar y configurar Django Rest Framework
*******************************************

Empezamos instalando las librerías necesarias:

* Instalamos Django Rest Framework ``pip install djangorestframework``
* Instalamos Django-filter ``pip install django-filter``
* Y por último, instalamos Markdown: ``pip install markdown``

Pasamos a configurar el proyecto:

* Lo primero será añadir **rest_framework** a settings.py:

.. code:: python 

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'rest_framework'
    ]

* Ahora como mínimo necesitamos tener una app creada, para ello ejecutamos ``python manage.py startapp API``
* Añadimos la app a settings.py:

.. code:: python 

    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'rest_framework',
        'API'
    ]

* Realizamos la migración de la base de datos ``python manage.py migrate``
* Y creamos un superusuario ``python manage.py createsuperuser``
  
.. note::
    Una forma cómoda de trabajar con aplicaciones mixtas es crear un directorio API dentro de la app y ahí un nuevo views.py y serializers.py 

Serializadores
##############

Los serializadores se encargan de trabajar con los modelos de datos para adaptarlos a la API.

* Para comenzar tenemos que crear un modelo en nuestra API (API/models.py):

.. code:: python 

    from django.db import models

    class Empleados(models.Model):
        nombre = models.CharField(max_length=100, verbose_name="Nombre")
        apellidos = models.CharField(max_length=100, verbose_name="Apellidos")
        observaciones = models.TextField(verbose_name="Observaciones")

        def _str__(self):
            return self.nombre

* Ejecutamos ``python manage.py makemigrations API`` para preparar las migraciones y migramos la tabla ``python manage.py migrate API``
* Vamos a crear un archivo para los serializadores en la ruta (API/serializers.py):

.. code:: python

    # Importamos la librería de serializers:
    from rest_framework import serializers
    # Importamos el modelo de datos a usar:
    from .models import Empleados

    # Creamos el serializador:
    class EmpleadosSerializer(serializers.ModelSerializer):
    class Meta:
        # Elegimos el modelo:
        model = Empleados
        # Podemos elegir los campos a mostrar:
        # fields = ['nombre', 'apellidos', 'observaciones']
        # O mostrar todos los campos:
        fields = '__all__'

Con esto ya hemos preparado el primer serializador.

ViewSets
########

Los viewsets se implementan en las vistas de Django y sirven para mostrar los valores de la API o bien en su frontend o bien como un JSON, 
para crear un ViewSet nos vamos a (API/views.py):

.. code:: python 

    from django.shortcuts import render
    # Importamos la librería de viewsets:
    from rest_framework import viewsets
    # El modelo Empleados:
    from .models import Empleados
    # Y el serializador de Empleados:
    from .serializers import EmpleadosSerializer

    # Creamos un Viewset para mostrar los datos:
    class EmpleadosViewSet(viewsets.ModelViewSet):
        # En el lanzamos un QuerySet al modelo Empleados:
        queryset = Empleados.objects.all()
        # y le decimos que lo serialize con EmpleadosSerializer:
        serializer_class = EmpleadosSerializer

Con esto ya tenemos listo el ViewSet.

Custom Endpoints
****************
Los Custom endpoints se usan para realizar acciones como filtrado en listas o para actualizar algún tipo de dato específico evítando la creación de nuevos viewsets:


* Ejemplo de uso añadiendo una opción para puntuar una serie:
  
.. code-block:: python 
    :linenos:

    class SerieViewSet(viewsets.ModelViewSet):
        queryset = Serie.objects.all()
        serializer_class = SerieSerializer
        permission_classes = [SoloMeOrReadOnly]

        def get_serializer_class(self):
            serializer = self.serializer_class

            if self.action == 'retrieve':
                serializer = DetailSerieSerializer
            # se añade la opción del nuevo serializador:
            if self.action == 'set_score': # y se utiliza un nuevo serializador específico:
                serializer = ScoreSerializer # se utiliza el serializador de Score que llama a su modelo

            return serializer

            # Con action vamos a crear un endpoint que establezca otra funcionalidad: 
            @action(detail=True, method=['PUT'], url_path='set-score', permission_classes=[IsAdminUser]) # el detail si es True nos hará la acción sobre un elemento en lugar del listado.
            # bajo este decorador se define la función (get o set) que recibirá además del request un valor entero para realizar la acción:
            def set_score(self, request, serie_id: int):
                data = {'serie': serie_id, 'user': request.user.pk, 'score': int(request.POST['score'])}
                # se le pasa la información a la función que controla los serializadores:
                serializer = self.get_serializer_class()(data=data)
                # se valida y si todo va bien se guarda la información:
                serializer.is_valid(raise_exception=True)
                serializer.save()

                return Response(status=status.HTTP_200_OK)

Rutas de la API
###############

Para configurar las rutas de la API utilizamos un archivo adicional de rutas o en nuestro caso vamos a usar el archivo principal (prueba_api/urls.py):

.. code:: python 

    from django.contrib import admin
    from django.urls import path, include # importamos include
    # Importamos la librería routers de rest_frameworks
    from rest_framework import routers
    # Importamos las vistas de la API
    from API import views

    # Creamos un enrutador para la API:
    router = routers.DefaultRouter()

    # En el router vamos añadiendo los endpoints a los viewsets:
    router.register('empleados', views.EmpleadosViewSet)

    urlpatterns = [
        path('api/v1/', include(router.urls)), # Aquí añadimos la ruta de la api que irá recibiendo los distintos endpoints arriba.
        path('admin/', admin.site.urls),
    ]

Ahora podemos ejecutar la API en ``http://localhost:8080/api/v1/`` y ver como podemos añadir registros.

.. attention::
    Con el nivel actual de permisos cualquiera puede introducir valores en la API. Para cambiar eso tenemos que ir al apartado de **permisos**

Modelo relacional y como mostrarlo
##################################

En DRF se pueden mostrar las relaciones entre tablas en una vista final entre otras personalizaciones.

Ejemplo de series y episodios:

1. Los serializadores:

.. code-block:: python 
    :linenos:

    from rest_framework import serializers
    from .models import Serie, Episodio


    class SerieSerializer(serializers.ModelSerializer):

        class Meta:
            model = Serie
            fields = ('id', 'title', 'description')


    class EpisodioSerializer(serializers.ModelSerializer):

        class Meta:
            model = Episodio 
            fields = ('id', 'name')

    # Para recuperar los episodios de una serie:
    class DetailSerieSerializer(serializers.ModelSerializer):
        # se crea el campo serializado para recuperar los episodios:
        episodes = EpisodioSerializer(source='episodio_set', many=True)

        class Meta:
            # se añade el modelo serie y los campos de esta añadiendo el nuevo campo episodes:
            model = Serie
            fields = ('id', 'title', 'description', 'episodes')

2. Ahora se modifica el comportamiento del Viewset que queremos:

.. code-block:: python 
    :linenos:

    class SerieViewSet(viewsets.ModelViewSet):
        queryset = Serie.objects.all()
        serializer_class = SerieSerializer
        permission_classes = [IsAuthenticatedOrReadOnly]

        # Ahora hay que relacionar los dos serializadores de Series:
        def get_serializer_class(self):
            # Si estamos listando todas las series que devuelva el primer serializador:
            serializer = self.serializer_class

            # Si invocamos la vista detalle o 'retrieve' que devuelva la serie con sus episodios:
            if self.action == 'retrieve':
                serializer = DetailSerieSerializer

            return serializer

De este modo cuando se listan todas las series se muestran tal cual y cuando accedemos a una nos indica los episodios que contiene.

Permisos 
########

Tenemos varios tipos de permisos para gestionar nusetra API. Para establecer permisos creamos una lista al final de (prueba_api/settings.py):

* Por defecto nuestra API estará disponible para lectura y escritura ante cualquier extraño.

Permisos Globales (settings.py)
*******************************
Se pueden establecer permisos globales en toda la aplicación editando settings.py:

* Establecer permisos a solo lectura:

.. code:: python 

    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [                     
            'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly',
        ],
    }

* Añadir acceso por login para poder editar y ver datos.

.. code:: python 

    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [                     
            'rest_framework.permissions.IsAuthenticated',
        ],
    }

* Login requerido para editar y visualización sin login:

.. code :: python

    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [                     
            'rest_framework.permissions.IsAuthenticatedOrReadOnly',
        ],
    }

Permisos individuales
*********************

En los ViewSets se pueden definir permisos para cada vista usando la variable **permission_classes**:

.. code-block:: Python
    :linenos:

    from rest_framework import viewsets
    from .serializers import SerieSerializer
    # Se importan los permisos que vayamos a establecer como IsAuthenticatedOrReadOnly, IsAuthenticate, o IsAdminUser:
    from rest_framework.permissions import IsAuthenticatedOrReadOnly
    from series.models import Consola

    class ConsolaViewSet(viewsets.ModelViewSet):
        queryset = Consola.objects.all()
        serializer_class = ConsolaSerializer
        # Se establece el permiso para esta vista:
        permission_classes = [IsAuthenticatedOrReadOnly]


Permisos personalizados
***********************
Se puede crear un nuevo permiso y utilizarlo tanto como permiso global como para ViewSets individuales:

* En la aplicación deseada se crea un archivo **permissions.py**:

.. code-block:: python
    :linenos:

    # se creará un permiso para que acepte solo un usuario:
    # se importa el permiso base:
    from rest_framework.permissions import BasePermission

    # se crea la clase del permiso:
    class SoloMeOrReadOnly(BasePermission):

        # tendrá una función que comprueba si soy yo el que inicia sesión o no:
        def has_permission(self, request, view):
            if request.method == 'GET':
                return True 
            else:
                return bool(request.user.is_authenticated and request.user.username == 'guillermo')

        
        # Este segundo método se invoca para establecer los permisos en un objeto (un articulo o elemento simple):
        def has_object_permission(self, request, view, obj):
            if request.method == 'GET':
                return True 
            else:
                return bool(request.user.is_authenticated and request.user.username == 'guillermo')

* En el **ViewSet** se invoca y se aplica como un permiso cualquiera:

.. code-block:: python 
    :linenos:

    # se importa el permiso creado:
    from .permissions import SoloMeOrReadOnly

    class ConsolaViewSet(viewsets.ModelViewSet):
        queryset = Consola.objects.all()
        serializer_class = ConsolaSerializer
        # ahora se asigna como un permiso cualquiera:
        permission_classes = [SoloMeOrReadOnly]

        def get_serializer_class(self):
            serializer = self.serializer_class

            if self.action == 'retrieve':
                serializer = DetailConsolaSerializer

            return serializer

.. note::
    El método **has_object_permission** que se ocupa de los permisos de un elemento en la tabla no es obligatorio si vamos a tener los mismos permisos como en el ejemplo anterior.


Crear documentación automática
##############################

Es muy interesante crear un sistema de documentación automática en nuestra api rest.

Para ello se hace lo siguiente:

1. Instalar coreapi: ``pip install coreapi``
2. Crear la ruta de la documentación en urls.py:

.. code-block:: python
    :linenos:

    # se importa el modulo de documentación:
    from rest_framework.documentation import include_docs_urls

    urlpatterns = [
        # se usa el modulo de documentación para cargar las rutas, podemos definir si es pública o privada con el tercer parámetro:
        path('docs/', include_docs_urls(title='Nombre API', public=False)),

3. Se añade a la constante **REST_FRAMEWORK** el siguiente valor en **settings.py**:

.. code-block:: python 
    :linenos:

    REST_FRAMEWORK = {'DEFAULT_SCHEMA_CLASS': 'rest_framework.schemas.coreapi.AutoSchema' }


Autenticación con JWT
#####################

1. Instalar jwt: ``pip install djangorestframework-simplejwt``
2. Se añade a **INSTALLED_APPS** la aplicación simplejwt: ``'rest_framework_simplejwt'``
3. Se añaden a la constante **REST_FRAMEWORK** los siguientes valores en **settings.py**:

.. code-block:: python 
    :linenos:

    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [
            'rest_framework.permissions.IsAuthenticated',
        ],
        'DEFAULT_AUTHENTICATION_CLASSES': ( # Este apartado define los metodos de autenticación
            'rest_framework_simplejwt.authentication.JWTAuthentication', # este es el método jwt que vamos a usar
            'rest_framework.authentication.SessionAuthentication', # este es el método por sesión 
            'rest_framework.authentication.BasicAuthentication', # y este es el método básico de usuario y contraseña
        ),
        
    }

3. Toca añadir las rutas para obtener el token de autenticación en urls.py:

.. code-block:: python 
    :linenos:

    # Se importan los metodos para obtener y refrescar el token:
    from rest_framework_simplejwt.views import TokenObtainPairView, TokenRefreshView

    
    urlpatterns = [
        path('api/', include(router.urls)),
        path('admin/', admin.site.urls),
        path('docs/', include_docs_urls('API Fetlix', public=False)),
        # Añadimos la ruta para obtener el token y para refrescarlo:
        path('api/token', TokenObtainPairView.as_view(), name='token_obtain_pair'),
        path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh')
    ]

Obtener un Token
****************

Para obtener un Token se hace lo siguiente:
1. Abrir Postman o Insomnia (u otro cliente API).
2. Ejecutar una petición **POST** a la ruta **http://127.0.0.1:8000/api/token** con usuario y contraseña:

.. code-block:: json 
    :linenos:

    	{
            "username":"misterg@gmail.com",
            "password":"maizfrito"
        }

3. Esto nos devolverá un token por ejemplo:

.. code-block:: json 
    :linenos:

    {
        "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY0NjA1MzkxNCwiaWF0IjoxNjQ1OTY3NTE0LCJqdGkiOiJmOGVhOWUzNTdhMGU0ZWU4ODU0Y2NiNWE2NTdjOGY1ZiIsInVzZXJfaWQiOjN9.9DvZVyzfZcmB-v9P_mgETFighXz2KjChPc_EslH5X3M",
        "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjQ1OTY3ODE0LCJpYXQiOjE2NDU5Njc1MTQsImp0aSI6IjBhNmEyNWM2YjVlMDQ4ZjQ5MzQxYzM2MGNlODM2OTdiIiwidXNlcl9pZCI6M30.He7w5XxjCrgeWupFOnGdVH4EusJ5fRZMbY3zkyZetCI"
    }

4. Ahora este token "access" se utilizará para todas las operaciones contra la API que requieran autenticación.

Haciendo una petición contra la API con JWT
*******************************************
Ejemplo de uso con Python.

La petición se podría dividir en dos partes:

1. Solicitud de token:

.. code-block:: python 
    :linenos:

    import requests

    headers = {
        'Content-Type': 'application/json',
        'Accept': '*/*',
    }

    data = '{"username":"misterg@gmail.com", "password":"sabotaje"}'

    r = requests.post('http://127.0.0.1:8000/api/token', headers=headers, data=data)
    print(r.status_code)
    token = r.json()

2. Petición de datos (listado de series):

.. code-block:: python 
    :linenos:

    headers['Authorization'] = 'Bearer ' + token['access']

    r = requests.get('http://127.0.0.1:8000/api/series/', headers=headers)
    print(r.status_code)
    print(r.content)