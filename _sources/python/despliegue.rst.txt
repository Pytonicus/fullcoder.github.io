Gunicorn: Despliegue web 
========================

.. image:: /logos/logo-gunicorn.png
    :scale: 20%
    :alt: Logo Gunicorn
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica para realizar despliegues con Gunicorn

.. contents:: Índice

Protocolo WSGI
##############
 
Es un protocolo estandar que utilizan las aplicaciones python en el ámbito web definiendo como debe comportarse. 

Gunicorn
********
Se encarga de comunicarse con el protocolo WSGI desde línea de comandos. 

Comandos útiles:

* Instalar Gunicorn: ``pip install gunicorn``
* Ejecutar servidor Gunicorn: ``gunicorn nombreProyecto.wsgi:application``
* Específicar número de procesos simultaneos: ``gunicorn nombreProyecto.wsgi:application --workers=4``
* Crear archivo de configuración en la raiz del proyecto **gunicorn.conf.py**:

.. code-block:: python 
    :linenos:

    import multiprocessing

    # Definir numero de procesos en contraste al número de procesadores:
    workers = multiprocessing.cpu_count()

    # Se puede cambiar la dirección o el puerto:
    bind = '127.0.0.1:8500'


Supervisor
**********
Es un programa externo que se utiliza para cargar procesos externos del sistema en segundo plano. En este caso se utilizará para ejecutar en segundo plano Gunicorn en nuestro Virtual Server.

Nginx
*****
Es un software que se utiliza para servir sitios web al igual que apache, el más utilizado para trabajar con aplicaciones Python. 

PaaS (Platform as a Service) 
****************************
Es un entorno cloud que nos permite crear una máquina virtual para ejecutar la aplicación web con Python.

Algunas de las PaaS más famosas:

* DigitalOcean
* Heroku
* Amazon Web Services
* Azure
* Google Cloud

Deploy en Django 
################

1. Instalar Gunicorn: ``pip install gunicorn``
2. Crear **settings_prod.py** para ajustar valores de producción:

.. code-block:: python 
    :linenos:

    # se importan todo el módulo de settings.py:
    from mi_proyecto.settings import *

    # La secret_key la metemos por variable de entorno:
    SECRET_KEY = os.environ.get('SECRET_KEY')

    # Se prepara para producción 
    DEBUG = False

    # Se habilitan los hosts que tendrán permisos, ['*'] así cogerá todas las peticiones.
    ALLOWED_HOSTS = ['www.paginaprueba.es', 'prueba.paginados.es']

    # se crea la ruta estática para recolectar luego todos los archivos estátitcos:
    STATIC_ROOT = BASE_DIR.joinpath('static/')

    # Cambiamos la base de datos por una de producción:
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'USER': os.getenv('DATABASE_USER'),
            'NAME': os.getenv('DATABASE_NAME'),
            'PASSWORD': os.getenv('DATABASE_PASSWORD'),
            'PASSWORD': os.getenv('DATABASE_HOST'),
            'PORT': '3306'
        }
    }

3. Generamos una secret_key: ``python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'`` la cual luego guardaremos en la variable de entorno del servidor virtual.
4. A la hora de desplegar el proyecto debe apuntar a las **settings_prod.py**

CONTINUARÁ...