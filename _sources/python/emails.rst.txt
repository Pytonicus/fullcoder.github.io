Emails con Python
=================

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Envío de emails con Python
 
.. contents:: Índice
 
smtplib: Envío de emails
########################
  
Modo básico
***********
 
.. code-block:: python
    :linenos:

    import smtplib

    # conectamos al servidor:
    conn = smtplib.SMTP('smtp.gmail.com', 587)
    # habilitar el tls:
    conn.starttls()
    # comprobamos si funciona:
    conn.ehlo()
    # iniciamos sesion:
    conn.login('pepe@fakemail.com', 'contraseña_email')

    # y enviamos el correo:
    conn.sendmail('pepe@fakemail.com', 'destino@correoremitente.com', 'Subject: Hey que tal\n\n Texto del mensaje, \n Hey que tal, puedo seguir escribiendo sin miedo\n - <b>Firmado guillermo</b>')

    conn.quit()

Modo enriquecido con HTML
*************************

.. code-block:: python
    :linenos:

    import smtplib

    # Correos implicados:
    yo = 'pepe@fakemail.com'
    cliente = 'cliente@mail.com'

    # Contenedor Mime con datos del correo:
    msg = MIMEMultipart('alternative')
    msg['Subject'] = 'Email de prueba'
    msg['From'] = yo
    msg['To'] = cliente
    
    # Cuerpo HTML:
    html = """\
    <html>
        <head><head>
        <body>
            <h1>Correo de prueba</h1>
            <p>Este es un correo de prueba para:</p>
            <ul>
                <li>Nombre: Pedro.</li>
                <li>Apellidos: Leal a ti.</li>
                <li>Email: {}. </li>
                <li>Número de teléfono: 600600666.</li>
            </ul>
        </body>
    </html>
    """.format(cliente)

    # Mime cuerpo y añadir al mensaje:
    mime_html = MIMEText(html, 'html')

    msg.attach(mime_html)

    # Preparar envio y enviar:
    conn = smtplib.SMTP('smtp.gmail.com', 587)
    conn.starttls()
    conn.ehlo()
    conn.login(yo, 'contraseña')
    conn.sendmail(cliente, yo, msg.as_string())
    conn.quit()
