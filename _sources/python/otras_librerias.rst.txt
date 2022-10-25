Otras Librerías Python
======================

.. image:: /logos/logo-pillow.png
    :scale: 100%
    :alt: Logo Pillow 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Librerías de uso común en Python.

.. contents:: Índice

Pillow: Tratamiento de imágenes
###############################
   
* Instalación: ``pip3 install Pillow``
 
.. code-block:: python
    :linenos:

    # pip3 install pillow y pip3 install requests

    import requests
    from io import BytesIO
    from PIL import Image

    # buscamos una imagen en internet:
    r = requests.get('https://i.pinimg.com/originals/0a/a9/2d/0aa92d0ca0473e1a8717a4cda29225cb.jpg')

    print('status code: {}'.format(r.status_code))

    # con bytesIO y pillow abrimos de r.content la imagen:
    imagen = Image.open(BytesIO(r.content))

    # imprimimos las propiedades de la imagen:
    print(imagen.size, imagen.format, imagen.mode)

    # establecemos una ruta para guardar la imagen:
    path = './imagen.' + imagen.format

    try:
        # guardamos la imagen en nuestro ordenador:
        imagen.save(path, imagen.format)
        print('Se ha guardado la imagen')
    except IOError:
        print('No se pudo guardar la imagen')

Speechrecognition: Reconocimiento de voz
########################################

* Instalación: ``pip3 install SpeechRecognition``

.. code-block:: python
    :linenos:

    # Importamos la librería speech:
    import speech_recognition as sr 

    # creamos el objeto reconocedor de voz:
    r = sr.Recognizer()

    # Ahora abrimos el micrófono:
    with sr.Microphone() as source:
        print('Di algo: ')
        # guardamos en audio lo que suene por microfono.
        audio = r.listen(source)

        try:
            # establecemos el idioma y convertimos el audio en texto:
            texto = r.recognize_google(audio, language='es-ES')
            print('Lo que has dicho: {}'.format(texto))
        except:
            print('Lo siento, pero no te he entendido')

   