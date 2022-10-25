Manejo de paquetes
==================

.. image:: /logos/logo-composer.png
    :scale: 80%
    :alt: Logo PHP
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M

 
Manejo de paquetes y dependencias con Composer en PHP 7.4

.. contents:: Índice
   
Instalar Composer
#################
  
* Primero instalamos dependencias: ``sudo apt install curl php-cli php-mbstring git unzip``
* Ahora nos vamos a nuestro directorio personal y hacemos curl: ``curl -sS https://getcomposer.org/installer -o composer-setup.php``
* Instalamos composer: ``sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer``
 

Archivo de configuración
########################

En la raiz del proyecto se crea un archivo llamado composer.json:

.. code-block:: json
    :linenos:

    {
        "name": "ggranados/proyecto_composer",
        "require": {
            "php": ">=7.4"
        },
        "require-dev": {
            "fzaninotto/faker": "dev-master"
        }
    }

Comandos mas destacados
#######################

* **composer install**: Instala todas las dependencias de composer.json.
* **composer update**: Analiza y actualiza las dependencias de composer.json.
* **composer require autor/nombre_paquete**: instala un nuevo paquete.

.. note::
    Se pueden encontrar paquetes PHP compatibles con Composer en: https://packagist.org/

.. note::
    Los paquetes se instalan en el directorio vendor/

Ejemplo de uso paquete faker
############################

.. code-block:: php 
    :linenos:

    <?php
        // cargamos las dependencias globales:
        require_once('./vendor/autoload.php');
        // creamos una instancia de Faker:
        $faker = Faker\Factory::create();

        // en un for generamos nombres de relleno con faker:
        for($i = 0; $i < 20; $i++){
            echo $faker->name . '<br>';
        }
    ?>

 