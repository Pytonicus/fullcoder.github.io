Framework: Django Rest Framework
================================
 
.. image:: /logos/logo-django-rest.png
    :scale: 75%
    :alt: Logo HTML5
    :align: center

.. |date| date::
.. |time| date:: %H:%M

 
Esta es la documentación que he recopilado para trabajar con Djang rest framework. Una extensión de django para crear API Rest.
 
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

.. code-block:: python 
    :linenos:

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

.. code-block:: python 
    :linenos:

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

.. code-block:: python 
    :linenos:

    from django.db import models


    class Consola(models.Model):
        """ Modelo de datos para videoconsolas """

        marca = models.CharField(max_length=200)
        modelo = models.CharField(max_length=200)
        lanzamiento = models.IntegerField(blank=True, null=True)

        def __str__(self):
            return self.modelo


    class Videojuego(models.Model):
        """ Modelo de datos para videojuegos """

        titulo = models.CharField(max_length=200)
        consola = models.ForeignKey(Consola, on_delete=models.CASCADE)

        def __str__(self):
            return self.modelo


* Ejecutamos ``python manage.py makemigrations API`` para preparar las migraciones y migramos la tabla ``python manage.py migrate API``

Serializador básico
*******************

* Vamos a crear un archivo para el serializador en la ruta (API/serializers/consolaSerializer.py):

.. code-block:: python 
    :linenos:

    # Importamos la librería de serializers:
    from rest_framework import serializers
    # Importamos el modelo de datos a usar:
    from API.models import Consola

    # Creamos el serializador:
    class ConsolaSerializer(serializers.ModelSerializer):
        # de forma similar a los formularios, es conveniente definir los campos del modelo:
        marca = serializers.CharField(required=True, max_length=200)
        modelo = serializers.CharField(required=True, max_length=200)
        lanzamiento = serializers.IntegerField(required=False)

        class Meta:
            # Elegimos el modelo:
            model = Consola

            # Aquí se definen los campos que va a manejar el serializador:
            fields = [
                'marca', 
                'modelo', 
                'lanzamiento'
            ]

        # el metodo validador recibirá los datos que se van a regsitrar y los comprobará antes de ingresarlos:
        def validate(self, data):
        # podemos crear validaciones específicas:
        if data.get('lanzamiento') and data.get('lanzamiento')  < 1970:
            raise serializers.ValidationError('El año de lanzamiento es demasiado bajo')


Con esto ya hemos preparado el primer serializador.

.. important::
    Recuerda crear un archivo vacío llamado **__init__.py** en cada carpeta que se generes para convertirlo en módulo.

Modificar salida de datos 
*************************

Se puede modificar la salida de datos a mostrar en el JSON:

.. code-block:: python 
    :linenos:

    from rest_framework import serializers
    # importamos el modelo videojuego para listarlos:
    from API.models import Consola, Videojuego

    class ConsolaSerializer(serializers.ModelSerializer):
        marca = serializers.CharField(required=True, max_length=200)
        modelo = serializers.CharField(required=True, max_length=200)
        lanzamiento = serializers.IntegerField(required=False)

        class Meta:
            model = Consola

            # Aquí se definen los campos que va a manejar el serializador:
            fields = [
                'id',
                'marca', 
                'modelo', 
                'lanzamiento'
            ]

        def validate(self, data):
            # podemos crear validaciones específicas:
            if data.get('lanzamiento') and data.get('lanzamiento')  < 1970:
                raise serializers.ValidationError('El año de lanzamiento es demasiado bajo')

            return data

        # Se puede personalizar la salida de datos con este método:
        def to_representation(self, instance):
            # podemos ir llamando cada uno de los títulos disponibles por su consola:
            juegos = Videojuego.objects.filter(consola=instance.id)
            return {
                "id": instance.id,
                "marca": instance.marca,
                "modelo": instance.modelo,
                "lanzamiento": instance.lanzamiento,
                "juegos": [juego.titulo for juego in juegos] # tan solo hay que añadir el titulo de cada elemento del listado que hemos localizado
            }


Modificar creación de datos  
***************************

Se puede modificar la creacíon de datos para ajustar su guardado:

.. code-block:: python 
    :linenos:

    from rest_framework import serializers
    from API.models import Consola, Videojuego

    class ConsolaSerializer(serializers.ModelSerializer):
        marca = serializers.CharField(required=True, max_length=200)
        modelo = serializers.CharField(required=True, max_length=200)
        lanzamiento = serializers.IntegerField(required=False)
        # creamos un campo nuevo opcional para recibir un videojuego y crearlo si no existe:
        videojuego = serializers.CharField(required=False, max_length=200)

        class Meta:
            model = Consola

            fields = [
                'id',
                'marca', 
                'modelo', 
                'lanzamiento',
                'videojuego' # este hay que añadirlo a la lista de campos para que el validador lo verifique
            ]

        def validate(self, data):
            if data.get('lanzamiento') and data.get('lanzamiento')  < 1970:
                raise serializers.ValidationError('El año de lanzamiento es demasiado bajo')

            return data

        def to_representation(self, instance):
            juegos = Videojuego.objects.filter(consola=instance.id)
            return {
                "id": instance.id,
                "marca": instance.marca,
                "modelo": instance.modelo,
                "lanzamiento": instance.lanzamiento,
                "juegos": [juego.titulo for juego in juegos]
            }

        # se usa el método create y en el se localiza si existe la consola y sino se procede a crear:
        def create(self, validated_data):
            # se crea la consola con los datos validados:
            consola = Consola.objects.create(**validated_data)
            # se crea el videojuego:
            if validated_data.get('videojuego'):
                Videojuego.objects.create(titulo=validated_data.get('videojuego'), consola_id=consola.id)

            # se retorna la creación del objeto:
            return consola


.. attention::
    la información que se recibe a continuación ya ha sido validada, por lo tanto no se puede modificar aquello que no pase la validación.

Modificar actualización de datos  
********************************

Se puede modificar la creacíon de datos para ajustar su guardado:

.. code-block:: python 
    :linenos:

    from rest_framework import serializers
    from API.models import Consola, Videojuego

    class ConsolaSerializer(serializers.ModelSerializer):
        marca = serializers.CharField(required=True, max_length=200)
        modelo = serializers.CharField(required=True, max_length=200)
        lanzamiento = serializers.IntegerField(required=False)
        videojuego = serializers.CharField(required=False, max_length=200)

        class Meta:
            model = Consola

            fields = [
                'id',
                'marca', 
                'modelo', 
                'lanzamiento',
                'videojuego' 
            ]

        def validate(self, data):
            if data.get('lanzamiento') and data.get('lanzamiento')  < 1970:
                raise serializers.ValidationError('El año de lanzamiento es demasiado bajo')

            return data

        def to_representation(self, instance):
            juegos = Videojuego.objects.filter(consola=instance.id)
            return {
                "id": instance.id,
                "marca": instance.marca,
                "modelo": instance.modelo,
                "lanzamiento": instance.lanzamiento,
                "juegos": [juego.titulo for juego in juegos]
            }

        def create(self, validated_data):
            consola = Consola.objects.create(**validated_data)
            if validated_data.get('videojuego'):
                Videojuego.objects.create(titulo=validated_data.get('videojuego'), consola_id=consola.id)

            return consola

        
        # se puede modificar el update para editar campos como queramos:
        def update(self, instance, validated_data):

            # se recuperan los campos validados que queremos modificar:
            validated_data["marca"] = instance.marca # recuperamos del registro original la marca y evitamos que sea modificable.
            validated_data["lanzamiento"] = 1990 # se puede establecer un valor fijo que no cambiará aunque enviemos un dato distinto.

            # ahora se recorren los valores de ambos objetos y se combinan:
            for key, value in validated_data.items():
                setattr(instance,key,value)

            # se guarda y retornan los cambios:
            instance.save()
            return instance

* Al intentar actualizar el registro con los siguientes datos no permitirá el cambio de marca y el lanzamiento asignará siempre 1990:

.. code-block:: json 
    :linenos:

    {
        "marca": "Sammy",
        "modelo": "Play Funstation",
        "lanzamiento": 2015
    }


.. attention::
    la información que se recibe a continuación ya ha sido validada, por lo tanto no se puede modificar aquello que no pase la validación.


ViewSets
########

Los viewsets se implementan en las vistas de Django y sirven para mostrar los valores de la API o bien en su frontend o bien como un JSON.

GET (mostrar información)
*************************

Para crear un ViewSet nos vamos a (API/views/consolaViewSet.py):

.. code-block:: python 
    :linenos:

    # importamos el apiview:
    from rest_framework.views import APIView
    # y el response:
    from rest_framework.response import Response 
    # también es necesario traer el modelo:
    from API.models import Consola
    # se carga el serializador creado:
    from API.serializers.consolaSerializer import ConsolaSerializer

    # creamos la vista:
    class ConsolaApiView(APIView):

        # con APIView se va definiendo que tipo de entrada permite la vista(funciona como una vista común en Django en lo referente a parametros):
        def get(self, request):
            # se carga los datos en una variable:
            consolas = Consola.objects.all()
            # se le envía al serializador, definimos si va a ser uno o varios resultados con many:
            serializer = ConsolaSerializer(consolas, many=True)

            # se muestra la respuesta:
            return Response(serializer.data, status=status.HTTP_200_OK)


GET - Paginación y personalizar salida 
++++++++++++++++++++++++++++++++++++++

Se puede retornar un número determinado de elementos por página creando un paginador personalizado:

.. code-block:: python 
    :linenos:

    from rest_framework.views import APIView
    from rest_framework.response import Response 
    from API.models import Consola
    from API.serializers.consolaSerializer import ConsolaSerializer
    # se cargan los siguientes módulos de paginador:
    from django.core.paginator import Paginator, PageNotAnInteger, EmptyPage

    # creamos la vista:
    class ConsolaApiView(APIView):
        # se define un nuevo parámetro para recibir por url con el número de página:
        def get(self, request, consola=None):
            
            # Si queremos un solo resultado, usamos el parámetro consola por url y recuperamos solo un valor:
            consola = Consola.objects.filter(id=consola).first()
            if consola:
                serializer = ConsolaSerializer(consola)
                return Response(serializer.data, status=status.HTTP_200_OK)


            consolas = Consola.objects.all()
            serializer = ConsolaSerializer(consolas, many=True)
            page = request.data.get('page')
            # el paginador recibe la data del serializador y un número de páginas:
            paginator = Paginator(serializer.data, 5)
            # Se controla si se recibe o no página y el número de páginas:
            try:
                consolas_paginated = paginator.page(page)
            except PageNotAnInteger:
                consolas_paginated = paginator.page(1)
            except EmptyPage:
                consolas_paginated = paginator.page(paginator.num_pages)
            # Se puede modificar la respuesta para retornar datos de la paginación:
            return Response({
                "cantidad_paginas": paginator.num_pages,
                "pagina_actual": page,
                "hay_siguiente": consolas_paginated.has_next(),
                "pagina_siguiente": consolas_paginated.next_page_number() if consolas_paginated.has_next() else False,
                "consolas": consolas_paginated.object_list
            }, status=status.HTTP_200_OK)


POST (Crear registro)
*********************

El post se define como un método nuevo para procesar la información:

.. code-block:: python 
    :linenos:

    from email.policy import HTTP
    from rest_framework.views import APIView
    from rest_framework.response import Response 
    from API.models import Consola
    from API.serializers.consolaSerializer import ConsolaSerializer
    from django.core.paginator import Paginator, PageNotAnInteger, EmptyPage
    from rest_framework import status

    class ConsolaApiView(APIView):
        def get(self, request, consola=None):

            consola = Consola.objects.filter(id=consola).first()
            if consola:
                serializer = ConsolaSerializer(consola)
                return Response(serializer.data, status=status.HTTP_200_OK)

            consolas = Consola.objects.all()
            serializer = ConsolaSerializer(consolas, many=True)

            page = request.data.get("page")
            paginator = Paginator(serializer.data, 5)

            try:
                consolas_paginated = paginator.page(page)
            except PageNotAnInteger:
                consolas_paginated = paginator.page(1)
            except EmptyPage:
                consolas_paginated = paginator.page(paginator.num_pages)
            # Se puede modificar la respuesta para retornar datos de la paginación:
            return Response({
                "cantidad_paginas": paginator.num_pages,
                "pagina_actial": page,
                "hay_siguiente": consolas_paginated.has_next(),
                "pagina_siguiente": consolas_paginated.next_page_number() if consolas_paginated.has_next() else False,
                "consolas": consolas_paginated.object_list
            }, status=status.HTTP_200_OK)

        # se define el post en la api view:
        def post(self, request):
            # se carga la información de la petición post en el serializador:
            serializer = ConsolaSerializer(data=request.data)
            # se verifica si ha pasado la validación:
            if serializer.is_valid():
                # se guarda la información y se retorna el resultado:
                serializer.save()
                return Response(serializer.data, status=status.HTTP_201_CREATED)
            # si no ha salido bien se retornan los errores:
            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)



DELETE - Eliminar elemento 
**************************

.. code-block:: python 
    :linenos:

    from email.policy import HTTP
    from rest_framework.views import APIView
    from rest_framework.response import Response 
    from API.models import Consola
    from API.serializers.consolaSerializer import ConsolaSerializer
    from django.core.paginator import Paginator, PageNotAnInteger, EmptyPage
    from rest_framework import status

    class ConsolaApiView(APIView):
        def get(self, request, consola=None):
            
            consola = Consola.objects.filter(id=consola).first()
            if consola:
                serializer = ConsolaSerializer(consola)
                return Response(serializer.data, status=status.HTTP_200_OK)
                
            consolas = Consola.objects.all()
            serializer = ConsolaSerializer(consolas, many=True)

            page = request.data.get("page")
            paginator = Paginator(serializer.data, 5)

            try:
                consolas_paginated = paginator.page(page)
            except PageNotAnInteger:
                consolas_paginated = paginator.page(1)
            except EmptyPage:
                consolas_paginated = paginator.page(paginator.num_pages)

            return Response({
                "cantidad_paginas": paginator.num_pages,
                "pagina_actial": page,
                "hay_siguiente": consolas_paginated.has_next(),
                "pagina_siguiente": consolas_paginated.next_page_number() if consolas_paginated.has_next() else False,
                "consolas": consolas_paginated.object_list
            }, status=status.HTTP_200_OK)

        def post(self, request):
            serializer = ConsolaSerializer(data=request.data)
            if serializer.is_valid():
                serializer.save()
                return Response(serializer.data, status=status.HTTP_201_CREATED)
            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

        # Eliminar un registro:
        def delete(self, request, consola):
            # se busca el valor:
            consola = Consola.objects.filter(id=consola).first()
            # si existe se borra:
            if consola:
                consola.delete()
                return Response("Consola eliminada", status=status.HTTP_204_NO_CONTENT)
            return Response("No existe consola", status=status.HTTP_400_BAD_REQUEST)


PUT - Actualizar registros
**************************

.. code-block:: python 
    :linenos:

    from email.policy import HTTP
    from rest_framework.views import APIView
    from rest_framework.response import Response 
    from API.models import Consola
    from API.serializers.consolaSerializer import ConsolaSerializer
    from django.core.paginator import Paginator, PageNotAnInteger, EmptyPage
    from rest_framework import status

    class ConsolaApiView(APIView):
        def get(self, request, consola=None):
            consola = Consola.objects.filter(id=consola).first()
            if consola:
                serializer = ConsolaSerializer(consola)
                return Response(serializer.data, status=status.HTTP_200_OK)
                
            consolas = Consola.objects.all()
            serializer = ConsolaSerializer(consolas, many=True)

            page = request.data.get("page")
            paginator = Paginator(serializer.data, 5)

            try:
                consolas_paginated = paginator.page(page)
            except PageNotAnInteger:
                consolas_paginated = paginator.page(1)
            except EmptyPage:
                consolas_paginated = paginator.page(paginator.num_pages)

            return Response({
                "cantidad_paginas": paginator.num_pages,
                "pagina_actial": page,
                "hay_siguiente": consolas_paginated.has_next(),
                "pagina_siguiente": consolas_paginated.next_page_number() if consolas_paginated.has_next() else False,
                "consolas": consolas_paginated.object_list
            }, status=status.HTTP_200_OK)

        def post(self, request):
            serializer = ConsolaSerializer(data=request.data)
            if serializer.is_valid():
                serializer.save()
                return Response(serializer.data, status=status.HTTP_201_CREATED)
            return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)


        def delete(self, request, consola):
            consola = Consola.objects.filter(id=consola).first()
            if consola:
                consola.delete()
                return Response("Consola eliminada", status=status.HTTP_204_NO_CONTENT)
            return Response("No existe consola", status=status.HTTP_400_BAD_REQUEST)


        # actualizamos registros con put:
        def put(self, request, consola):
            # se recupera el registro a editar:
            consola = Consola.objects.get(id=consola)

            # se envía el objeto y la data recibida por put para hacer los cambios:
            serializer = ConsolaSerializer(consola, data=request.data, partial=True)  # la opción partial indica que no es necesario enviar todo

            # se comprueba que todo es correcto:
            if serializer.is_valid():
                serializer.save()
                return Response(serializer.data, status=status.HTTP_200_OK)
            return Response("Hay errores en la actualización", status=status.HTTP_400_BAD_REQUEST)


Con esto ya tenemos listo el ViewSet.

.. note::
    Si entramos a la ruta http://localhost:8000/api/consolas veremos una interfaz con el resultado, pero lo más recomendable es trabajar con software como Postman o Insomnia


Rutas de la API
###############

* Archivo principal de rutas urls.py:

.. code-block:: python 
    :linenos:

    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls),
        path('api/', include('API.urls'))
    ]

* Archivo de rutas adicional: (API/urls.py):

.. code-block:: python 
    :linenos:

    from django.urls import path 
    from API.views.consolaViewset import ConsolaApiView

    urlpatterns = [
        path('consolas', ConsolaApiView.as_view(), name='consolas'),
        # agregamos la ruta para una consola individual:
        path('consolas/<int:consola>', ConsolaApiView.as_view(), name='consola')
    ]

Ahora podemos ejecutar la API en ``http://localhost:8080/api/consolas`` o ``http://localhost:8080/api/consolas/1`` y ver como podemos añadir registros.

.. attention::
    Con el nivel actual de permisos cualquiera puede introducir valores en la API. Para cambiar eso tenemos que ir al apartado de **permisos**


Permisos 
########

Tenemos varios tipos de permisos para gestionar nuestra API. Para establecer permisos creamos una lista al final de (prueba_api/settings.py):

* Por defecto nuestra API estará disponible para lectura y escritura ante cualquier extraño.

Permisos Globales (settings.py)
*******************************
Se pueden establecer permisos globales en toda la aplicación editando settings.py:

* Establecer permisos a solo lectura:

.. code-block:: python 
    :linenos:

    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [                     
            'rest_framework.permissions.DjangoModelPermissionsOrAnonReadOnly',
        ],
    }

* Añadir acceso por login para poder editar y ver datos.

.. code-block:: python 
    :linenos:

    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [                     
            'rest_framework.permissions.IsAuthenticated',
        ],
    }

* Login requerido para editar y visualización sin login:

.. code-block:: python
    :linenos:

    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [                     
            'rest_framework.permissions.IsAuthenticatedOrReadOnly',
        ],
    }

Permisos individuales
*********************

En los ViewSets se pueden definir permisos para cada vista usando la variable **permission_classes**:

.. code-block:: python
    :linenos:

    # Se importan los permisos que vayamos a establecer como IsAuthenticatedOrReadOnly, IsAuthenticate, o IsAdminUser:
    from rest_framework.permissions import IsAuthenticatedOrReadOnly

    class ConsolaApiView(APIView):
        # se asigna al atributo siguiente el tipo de permiso de esta APIView:
        permission_classes = [IsAuthenticatedOrReadOnly]

        def get(self, request, consola=None):
        ...


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
    from API.permissions import SoloMeOrReadOnly

    class ConsolaApiView(APIView):
        # se agrega el permiso como cualquier estandar:
        permission_classes = [SoloMeOrReadOnly]

        def get(self, request, consola=None):
        ...

.. note::
    El método **has_object_permission** que se ocupa de los permisos de un elemento en la tabla no es obligatorio si vamos a tener los mismos permisos como en el ejemplo anterior.


Crear documentación automática
##############################

Es muy interesante crear un sistema de documentación automática en nuestra api rest.

Para ello se hace lo siguiente:

1. Instalar coreapi: ``pip install coreapi``
2. Crear la ruta de la documentación en API/urls.py:

.. code-block:: python
    :linenos:

    from django.urls import path 
    from API.views.consolaViewset import ConsolaApiView
    # cargamos el modulo de rutas de rest_framework:
    from rest_framework.documentation import include_docs_urls

    urlpatterns = [
        path('consolas', ConsolaApiView.as_view(), name='consolas'),
        # agregamos la ruta para una consola individual:
        path('consolas/<int:consola>', ConsolaApiView.as_view(), name='consola'),
            path('docs/', include_docs_urls(title='Nombre API', public=False))
    ]

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

3. Toca añadir las rutas para obtener el token de autenticación en API/urls.py:

.. code-block:: python 
    :linenos:

    from django.urls import path 
    from API.views.consolaViewset import ConsolaApiView
    from rest_framework.documentation import include_docs_urls
    # Se importan los metodos para obtener y refrescar el token:
    from rest_framework_simplejwt.views import TokenObtainPairView, TokenRefreshView

    urlpatterns = [
        path('consolas', ConsolaApiView.as_view(), name='consolas'),
        path('consolas/<int:consola>', ConsolaApiView.as_view(), name='consola'),
            path('docs/', include_docs_urls(title='Nombre API', public=False)),
        # Añadimos la ruta para obtener el token y para refrescarlo:
        path('token', TokenObtainPairView.as_view(), name='token_obtain_pair'),
        path('token/refresh/', TokenRefreshView.as_view(), name='token_refresh')
    ]

Obtener un Token
****************

Para obtener un Token se hace lo siguiente:
1. Abrir Postman o Insomnia (u otro cliente API).
2. Ejecutar una petición **POST** a la ruta **http://127.0.0.1:8000/api/token** con usuario y contraseña:

.. code-block:: json 
    :linenos:

    	{
            "username":"pepillo",
            "password":"maizfrito"
        }

3. Esto nos devolverá un token por ejemplo:

.. code-block:: json 
    :linenos:

    {
        "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTY0NjA1MzkxNCwiaWF0IjoxNjQ1OTY3NTE0LCJqdGkiOiJmOGVhOWUzNTdhMGU0ZWU4ODU0Y2NiNWE2NTdjOGY1ZiIsInVzZXJfaWQiOjN9.9DvZVyzfZcmB-v9P_mgETFighXz2KjChPc_EslH5X3M",
        "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjQ1OTY3ODE0LCJpYXQiOjE2NDU5Njc1MTQsImp0aSI6IjBhNmEyNWM2YjVlMDQ4ZjQ5MzQxYzM2MGNlODM2OTdiIiwidXNlcl9pZCI6M30.He7w5XxjCrgeWupFOnGdVH4EusJ5fRZMbY3zkyZetCI"
    }

4. Ahora este token "access" se utilizará para todas las operaciones contra la API que requieran autenticación. Solo hay que elegir en la pestaña Auth de Postman la opción Bearer e ingresar el token en cada consulta.

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

    data = '{"username":"misterg@gmail.com", "password":"maizfrito"}'

    r = requests.post('http://127.0.0.1:8000/api/token', headers=headers, data=data)
    print(r.status_code)
    token = r.json()

2. Petición de datos (listado de series):

.. code-block:: python 
    :linenos:

    headers['Authorization'] = 'Bearer ' + token.get('access')

    r = requests.get('http://127.0.0.1:8000/api/consolas', headers=headers)
    print(r.status_code)
    print(r.content)