Testing en Python 
=================

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Testing en diferentes casos con Python 
  
.. contents:: Índice

Testing en Django  
#################

TestTipe en Apps django 
***********************
Se abre una app django y se edita el archivo **test.py**:

.. code-block:: python
    :linenos:

    # Se importa TestCase por defecto:
    from django.test import TestCase
    # importamos los modelos serie y episodios:
    from .models import Serie, Episodio

    # Se crea una clase para cada test:
    class TestSerie(TestCase):
        # podemos crear información temporal en la base de datos:
        def _generate_serie(self):
            serie = Serie.objects.create(title='Los amigos', description='Descripcion de los amigos')

            for i in range(1, 6):
                Episodio.objects.create(serie_id=serie.pk, name='episodio amigos', number=i+1)

            return serie

        # vamos a probar un endpoint:
        def test_list_serie(self):
            # recuperamos el endpoint con get post put o delete:
            response = self.client.get('/api/series/')

            # Comprueba si el código es igual a 200:
            self.assertEqual(response.status_code, 200)

        # prueba usando 
        def test_retreive_serie(self):
            # Se recupera la serie que se ha creado temporal:
            serie = self._generate_serie()

            # Ahora vamos a probar a recuperar el detalle de la serie:
            response = self.client.get('/api/series/{}/'.format(serie.pk))

            self.assertEqual(response.status_code, 200)

            # vamos a conseguir el json:
            response_json = response.json()

            # Comprobamos que la respuesta es un diccionario:
            self.assertIsInstance(response_json, dict)
            # comprobamos cada uno de los campos si son del formato correcto:
            self.assertIsInstance(response_json.get('id'), int)
            self.assertIsInstance(response_json.get('title'), str)
            self.assertIsInstance(response_json.get('description'), str)
            self.assertIsInstance(response_json.get('episodes'), list)


TestTipe autenticación 
**********************

En algunos casos es necesario logearse para poder realizar algunas operaciones en la aplicación:

.. code-block:: python 
    :linenos:

    from django.test import TestCase
    from .models import Serie, Episodio
    # Se importa el modelo de usuarios:
    from django.contrib.auth.models import User

    class TestSerie(TestCase):
        
        # se genera un usuario de prueba:
        def _generate_user(self) -> User:
            user = User.objects.create(username='fake', password='insegura', email='fakemail@fake.com')

            return user

        # se crea un test que necesite de login como crear una serie:
        def test_create_serie(self):
            user = self._generate_user()
            # se fuerza el login sin necesidad de que tenga contraseña o permisos: 
            self.client.force_login(user)
            # preparamos la información:
            serie_dict = {'title': 'serie de prueba', 'description': 'descripcion de prueba'}
            # se hace la consulta: 
            response = self.client.post('/api/series/', serie_dict)

            # se hacen todas las comprobaciones:
            self.assertEqual(response.status_code, 201)

            response_json = response.json()

            self.assertIsInstance(response_json, dict)
            self.assertIsInstance(response_json.get('id'), int)
            self.assertIsInstance(response_json.get('title'), str)
            self.assertIsInstance(response_json.get('description'), str)


Fixtures - generar datos base 
*****************************
Vamos a recuperar unos datos que pasaremos a json para poder usar en todos los test:

1. Se crea en la raiz del proyecto la carpeta **fixtures**
2. Ahora para ejecutar un fixture que genere datos de usuarios: ``python manage.py dumpdata --format=json auth.user > fixtures/users.json``
3. Se puede hacer lo mismo pero con un solo registro: ``python manage.py dumpdata --format=json --pks 1 series.serie > fixtures/serie.json``
4. Si queremos importar los episodios: ``python manage.py dumpdata --format=json --pks 1 series.episodio >> fixtures/serie.json``
5. Indicar donde se guardan las Fixtures en **settings.py**:  ``FIXTURE_DIRS = [str(BASE_DIR.joinpath('fixtures/'))]``
6. Para reemplazar los generates por las fixtures se hace lo siguiente en los tests:

.. code-block:: python 
    :linenos:

    from django.test import TestCase
    from .models import Serie, Episodio
    from django.contrib.auth.models import User

    class TestSerie(TestCase):
        # ahora se pueden cargar fácilmente la información de las fixtures:
        fixtures = ['serie', 'users']

        def test_create_serie(self):
            # Se reemplaza la consulta por una con el ORM:
            user = User.objects.first()
            self.client.force_login(user)

            serie_dict = {'title': 'serie de prueba', 'description': 'descripcion de prueba'}
            response = self.client.post('/api/series/', serie_dict)

            self.assertEqual(response.status_code, 201)

            response_json = response.json()

            self.assertIsInstance(response_json, dict)
            self.assertIsInstance(response_json.get('id'), int)
            self.assertIsInstance(response_json.get('title'), str)
            self.assertIsInstance(response_json.get('description'), str)



        def test_list_serie(self):
            response = self.client.get('/api/series/')

            self.assertEqual(response.status_code, 200)

        def test_retreive_serie(self):
            # Se reemplaza la consulta por una con el ORM:
            serie = Serie.objects.first()

            response = self.client.get('/api/series/{}/'.format(serie.pk))

            self.assertEqual(response.status_code, 200)

            response_json = response.json()

            self.assertIsInstance(response_json, dict)
            self.assertIsInstance(response_json.get('id'), int)
            self.assertIsInstance(response_json.get('title'), str)
            self.assertIsInstance(response_json.get('description'), str)
            self.assertIsInstance(response_json.get('episodes'), list)




.. attention::
    En el paso 4 debemos arreglar la información manualmente ya que se añade un segundo listado de forma incorrecta



Herramienta Coverage
####################

La herramienta coverage mide la covertura de los test que preparamos:

1. Instalar la herramienta: ``pip install coverage``
2. Para ejecutar tests: ``coverage run manage.py test`` (osea el comando de testing que usamos)
3. Generar reporte: ``coverage report``

