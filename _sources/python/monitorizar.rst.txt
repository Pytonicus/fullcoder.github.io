Monitorización en Python  
========================

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Monitorización de aplicaciones en Python 
  
.. contents:: Índice

Monitorización en Django  
########################

Monitorizar Loggins
*******************

1. Configurar el **logger** en **settings.py**:

.. code-block:: python 
    :linenos:

    # importar sys:
    import sys

    # Se habilita la constante logging:
    # Se habilita la constante logging:
    LOGGING = {
        'version': 1,
        'disable_existing_loggers': False, # Evitar que pise otros loggers como DEFAULT_LOGGING
        'formatters': { # se define el formato de salida
            'default': { # se utiliza el formater estandar de logging:
                'class': 'logging.Formatter',
                # y se define la estructura del mensaje, en este caso TIEMPO - NIVEL - LOGGER - MENSAJE:
                'format': '%(asctime)s - %(levelname)s - %(name)s: %(message)s'
            }
        },
        'handlers': {
            'console': { # se define la salida por consola
                'class': 'logging.StreamHandler', # la clase que controla los logs
                'stream': sys.stdout, # el stream que los manejará
                'formatter': 'default' # formato default
            },
            'error_file': { # aquí saldría por archivo
                'class': 'logging.FileHandler', # se usa el filehandler para guardar archivos
                'filename': 'error.log', # se define el nombre del archivo
                'formatter': 'default',
                # 'level': 'ERROR', Si solo queremos almacenar los mensajes de error
            }
        },
        'loggers': {
            '': { # vamos a coger todos los loggers:
                'level': 'INFO', # Nivel del mensaje.
                'handlers': ['console', 'error_file'] # definir la salida por consola y archivo (o solo una)
            }
        }
    }

2. Ir a la vista o viewset que se quiere monitorizar:

.. code-block:: python 
    :linenos:

    # Se importa logging:
    import logging


    class SerieView(View):

        def get(self, request):
            context = {
                'series': list(Serie.objects.all())
            }

            return render(request, 'series/series.html', context)

    class SerieViewSet(viewsets.ModelViewSet):
        queryset = Serie.objects.all()
        serializer_class = SerieSerializer
        permission_classes = [IsAuthenticatedOrReadOnly]

        # en el constructor de la clase:
        def __init__(self, *args, **kwargs):
            # se carga el logger en un atributo:
            self.logger = logging.getLogger(__name__)
            super().__init__(*args, **kwargs)

        def get_serializer_class(self):
            # Se monitoriza el método que devuelve las series:
            self.logger.error(self.action)
            
            serializer = self.serializer_class

            if self.action == 'retrieve':
                serializer = DetailSerieSerializer
                
            return serializer

* En este caso solo se está monitorizando las series, pero lo ideal es monitorizar cada parte.
* El mensaje que muestra cada acción es: **2022-03-03 08:52:36,241 - ERROR - series.views: list**
* Los logs se almacenan en la ruta raiz del proyecto con el nombre que hemos definido antes: **error.log**

.. attention::
    Si definimos un LOGGING este reemplaza a DEFAULT_LOGGER, es importante que tanto en LOGGING como en DEFAULT_LOGGING se encuentre el valor ``'disable_existing_loggers': False``


Avisar de errores automáticamente
*********************************

Para realizar esto hay que habilitar la constante **DEFAULT_LOGGING** en **settings.py**:

.. code-block::
    :linenos:

    # Habilitar el logger que se encarga de las queries a la base de datos:
    DEFAULT_LOGGING = {
        'version': 1,
        'disable_existing_loggers': False, # no pisar los otros logger
        'filters': { # filtrados:
            'require_debug_false': { # comprobar que no vienen de debug:
                '()': 'django.utils.log.RequireDebugFalse'
            },
            'require_debug_true': { # comprobar que vienen de debug:
                '()': 'django.utils.log.RequireDebugTrue'
            }
        },
        'formatters': {
            'django.server': {
                '()': 'django.utils.log.ServerFormatter',
                'format': '[{server_time}] {message}',
                'style': '{',
            }
        },
        'handlers': {
            'console': {
                'level': 'INFO',
                'filters': ['require_debug_true'], # si el modo debug esta en True saldrá por consola.
                'class': 'logging.StreamHandler',
                'formatter': 'django.server'
            },
            'mail_admins': {
                'level': 'ERROR',
                'filters': ['require_debug_false'], # si el modo debug esta en False (producción) nos enviará un email.
                'class': 'django.utils.log.AdminEmailHandler'
            }
        },
        'loggers': {
            'django': {
                'handlers': ['console', 'mail_admins'] # saldrá por consola y por email los loggersf
            }
        }
    }

    # Creamos el listado de administradores que se ocupan de la aplicación:
    ADMINS = [('Guillermo', 'guillermo@gggmail.com')]

    # Configuramos un email backend de prueba por si no tenemos servidor de email aún configurado:
    EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'


Avisar de errores customizados en LOGGING 
*****************************************

Podemos configurar la salida de errores en producción para que los envíe por email:

.. code-block::
    :linenos:

        import sys

        LOGGING = {
            'version': 1,
            'filters': { # Se van a definir un par de filtros que tienen que ver con el entorno de Desarrollo y producción:
                'require_debug_false': { # comprobar si estamos en Desarrollo:
                    '()': 'django.utils.log.RequireDebugFalse'
                },
                'require_debug_true': { # comprobar si estamos en Producción:
                    '()': 'django.utils.log.RequireDebugTrue'
                }
            },
            'formatters': { 
                'default': { 
                    'class': 'logging.Formatter',
                    'format': '%(asctime)s - %(levelname)s - %(name)s: %(message)s'
                }
            },
            'handlers': {
                'console': { 
                    'class': 'logging.StreamHandler', 
                    'stream': sys.stdout, 
                    'formatter': 'default' 
                },
                'error_file': { 
                    'class': 'logging.FileHandler',
                    'filename': 'error.log',
                    'formatter': 'default',
                    'level': 'ERROR', 
                }, # Se carga el mail admins:
                'mail_admins': {
                    'level': 'ERROR',
                    'filters': ['require_debug_false'], # si el modo debug esta en False (producción) nos enviará un email.
                    'class': 'django.utils.log.AdminEmailHandler'
                }
            },
            'loggers': {
                '': { 
                    'level': 'INFO',
                    'handlers': ['console', 'error_file', 'mail_admins'] # se añade el mail_admins para los correos
                }
            }
        }

        # Creamos el listado de administradores que se ocupan de la aplicación:
        ADMINS = [('Guillermo', 'guillermo@gggmail.com')]

        # Configuramos un email backend de prueba por si no tenemos servidor de email aún configurado:
        EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'