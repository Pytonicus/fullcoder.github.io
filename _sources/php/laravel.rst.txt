Framework: Laravel
==================

.. image:: /logos/logo-laravel.png
    :scale: 30%
    :alt: Logo Django
    :align: center


.. |date| date::
.. |time| date:: %H:%M

Documentación básica para trabajar con Laravel 5
.. contents:: Índice
  
Configuraciones
###############  
 
Creación del proyecto
*********************

- Instalar laravel vía composer: ``composer create-project laravel/laravel proyecto-laravel "5.6.*" --prefer-dist``
- Probar que está funcionando: ``php -S localhost:8000 -t public/``

.. note::
    Dentro de Public se encuentra el archivo principal de la aplicación, es donde debe apuntar el servidor.

.. attention:: 
    Es necesario tener Composer instalado: https://getcomposer.org/download/

.. attention::
    Es importante tener instalado PHP o en su defecto un servidor Lamp o Xamp

.. attention::
    Es posible que no se ejecute el proyecto correctamente en el servidor, si es así 
    ejecutamos ``composer install`` para solventar dependencias. También pueden faltar 
    paquetes de php en linux, se instalan ``sudo apt install php-mbstring`` y ``sudo apt install php-xml``. 
    Se vuelve a ejecutar ``composer install`` y no debería de dar errores.

Estructura de Laravel
*********************
En la estructura de un proyecto Laravel estas son las partes más importantes:

- app: directorio con el contenido principal de Laravel y la aplicación.
    - http: contiene los modelos por ejemplo.
- bootstrap: Contiene un archivo que inicia el framework y la caché.
- config: contiene archivos de configuración de la aplicación. 
- database: contiene lo relacionado con las migraciones de la base de datos.
- public: contiene archivos públicos como los assets o el index
- resources: es donde se encuentran las vistas de la aplicación.
- routes: contiene las rutas de la aplicación.
- storage: almacenará archivos a subir.
- tests: carpeta con los test de la explicación.
- vendor: guarda todos los paquetes y librerías instalados con composer.
- artisan: permite ejecutar comandos cli de Laravel.
- .env: es donde se configura la conexión a la base de datos entre otros.

Comandos Artisan
****************
Laravel tiene una lista de comandos con Artisan los cuales se destacan:

- Listar rutas: ``php artisan route:list``
- Crear controlador: ``php artisan make:controller NuevoController``
- Crear controlador con CRUD: ``php artisan make:controller UserController --resource``
- Crear una migración: ``php artisan make:migration create_consolas_table --table=lista_consolas``
- Desplegar migración: ``php artisan migrate``
- Refrescar migraciones: ``php artisan migrate:refresh``
- Crear un seeder: ``php artisan make:seed lista_consolas_seed``
- Lanzar un seeder: ``php artisan db:seed --class=lista_consolas_seed``
 
Configurar conexión a base de datos
***********************************
Para configurar la base de datos se edita el archivo **.env** y se añade los datos de configuración de nuestra base de datos:

.. code-block:: 
    :linenos:

    DB_CONNECTION=mysql
    DB_HOST=127.0.0.1
    DB_PORT=3306
    DB_DATABASE=consolas
    DB_USERNAME=guillermo
    DB_PASSWORD=1234

.. note:: 
    El archivo de configuración también puede configurar correos y bases de datos redis.

Rutas en Laravel 
################

Las rutas en Laravel las podemos encontrar dentro de la carpetas **routes** en el archivo **web.php**

Ejemplo de ruta:

.. code-block:: php 
    :linenos:

    <?php

    /*
    |--------------------------------------------------------------------------
    | Web Routes
    |--------------------------------------------------------------------------
    |
    | Here is where you can register web routes for your application. These
    | routes are loaded by the RouteServiceProvider within a group which
    | contains the "web" middleware group. Now create something great!
    |
    */

    // Definición de la ruta raiz:
    Route::get('/', function () {
        // retornar una vista:
        return view('welcome');
    });


Rutas sencillas
***************

Las rutas utilizan los siguientes métodos:

- GET: recuperar información 
- POST: Enviar información 
- PUT: Actualizar datos 
- DELETE: Eliminar datos

Ejemplo de como cargar una vista en una ruta:

.. code-block:: php 
    :linenos:

    <?php

    /*
    |--------------------------------------------------------------------------
    | Web Routes
    |--------------------------------------------------------------------------
    |
    | Here is where you can register web routes for your application. These
    | routes are loaded by the RouteServiceProvider within a group which
    | contains the "web" middleware group. Now create something great!
    |
    */

    // Definición de la ruta raiz:
    Route::get('/', function () {
        // retornar una vista:
        return view('welcome');
    });


    Route::get('/prueba', function(){
        // variables que se pueden asignar al callback:
        $saludo = "Hola con Laravel";

        // la función view puede recibir un array con datos que mostrará en la plantilla:
        return view('prueba', array(
            'saludo' => $saludo
        ));
    });

    Route::get('/prueba', function(){
        // variables que se pueden asignar al callback:
        $saludo = "Hola con Laravel";

        // otro modo de cargar valores a la vista es con with:
        return view('prueba')
                ->with('saludo', $saludo); // pueden haber tantos with como hagan falta.
    });

Rutas con parámetros
********************

.. code-block:: php 
    :linenos:

    <?php

    /*
    |--------------------------------------------------------------------------
    | Web Routes
    |--------------------------------------------------------------------------
    |
    | Here is where you can register web routes for your application. These
    | routes are loaded by the RouteServiceProvider within a group which
    | contains the "web" middleware group. Now create something great!
    |
    */

    Route::get('/', function () {
        return view('welcome');
    });

    // la ruta recibe el parámetro nombre y este se debe pasar a la función callback:
    Route::get('/saludar/{nombre}', function($nombre){
        return "<h2>Hola " . $nombre . "</h2>";
    });

    // con ? se define parametro opcional pero hay que definir valor por defecto en el parámetro del callback:
    Route::get('/edad/{edad?}', function($edad = "desconocida"){
        return "<h2>Hola, tu edad es: " . $edad . "</h2>";
    });

Condiciones en las rutas
************************
Las rutas en Laravel pueden recibir condiciones gracias a la función where:

.. code-block:: php 
    :linenos:

    <?php

    /*
    |--------------------------------------------------------------------------
    | Web Routes
    |--------------------------------------------------------------------------
    |
    | Here is where you can register web routes for your application. These
    | routes are loaded by the RouteServiceProvider within a group which
    | contains the "web" middleware group. Now create something great!
    |
    */

    Route::get('/', function () {
        return view('welcome');
    });


    Route::get('/edad/{edad?}', function($edad = "desconocida"){
        return "<h2>Hola, tu edad es: " . $edad . "</h2>";
    })->where(array( // con expresiones regulares se pueden filtrar los parámetros:
        'edad' => '[0-9]+'
    ));

.. attention::
    Si se añade más condiciones y son parámetros obligatorios estos deberán cumplirse.

Cargar metodo de controlador en rutas 
*************************************
Lo lógico y más común es devolver un controlador que ya se encargará de toda la lógica que va a llevar la vista:

.. code-block:: php 
    :linenos:

    // La ruta recibe como segundo parámetro el controlador y tras la @ el método que ejecutar:
    Route::get('/consolas', 'ConsolaController@index');


Colecciones de rutas
********************
Se pueden crear prefijos para ordenar las rutas que van dentro de un CRUD:

.. code-block:: PHP 
    :linenos:

    Route::group(['prefix'=>'consolas'], function(){
        Route::get('index', 'ConsolasController@index');
        Route::get('listar', 'ConsolasController@listar');
    });

Middlewares
###########
Los middlewares son filtros en Laravel, existen ya algunos definidos por defecto:

- Crear middleware: ``php artisan make:middleware CheckConsola``
- El middelware se puede editar dentro de **Http/middleware**:

.. code-block:: php 
    :linenos:

    <?php

    namespace App\Http\Middleware;

    use Closure;

    class CheckConsola
    {
        /**
        * Handle an incoming request.
        *
        * @param  \Illuminate\Http\Request  $request
        * @param  \Closure  $next
        * @return mixed
        */
        public function handle($request, Closure $next)
        {
            // se va a filtrar el parámetro modelo:
            $modelo = $request->route('modelo');

            // si el modelo no es el que tenemos disponible:
            if(is_null($modelo) || $modelo != 'playstation'){
                // redirecciona al listado:
                return redirect()->action('ConsolaController@index');
            }
            
            return $next($request);
        }
    }

- Hay que dar de alta el middleware en **Http/kernel.php** añadidendo una nueva línea dentro del array **$routeMiddleware**: ``'checkconsola' => \App\Http\Middleware\CheckConsola::class,``
- Ahora en las rutas de **webs.php** se define el middelware:

.. code-block:: php
    :linenos:

    // añadir el middleware:
    Route::get('/consola/{modelo?}', array(
        'middleware' => 'checkconsola',
        'uses' => 'ConsolaController@consola'
    ));

De este modo, el middleware cuando reciba por parámetros una consola que no sea playstation hará un redireccionamiento al listado.

Vistas en Laravel (plantillas Blade)
####################################

Las vistas están en formato blade y las podemos encontrar en **resources/views/**. Su nomenclatura se define por terminar en **.blade.php** para 
hacer referencia que son plantillas blade.

A la hora de trabajar con vistas es bueno crear una carpeta dentro de **views** llamada **consolas**, dentro
de esta carpeta se pueden crear todas las vistas relacionadas con las consolas, por ejemplo **listar-consolas.blade.php**:

.. code-block:: php 
    :linenos:

    <h1>Listado de consolas</h1>

    <ul>
        <li>Sony PlayStation</li>
        <li>Sega Megadrive</li>
        <li>Nintendo DS</li>
    </ul>

La ruta para cargar esta vista que se encuentra dentro de una carpeta sería la siguiente:

.. code-block:: php 
    :linenos:

    Route::get('/consolas', function(){
        // con el . se indica una ruta de carpetas en views:
        return view('consolas.listar-consolas');
    });

Uso de variables
****************
Las variables se pueden cargar desde el controlador con el uso de dobles llaves **{{ $variable }}**:

.. code-block:: php 
    :linenos:

    <h1>{{ $titulo }}</h1>

    <ul>
        <li>Sony PlayStation</li>
        <li>Sega Megadrive</li>
        <li>Nintendo DS</li>
    </ul>

.. note::
    Para añadir comentarios en Blade se usa la sintaxis: **{! Comentario !}**, a diferencia de los comentarios 
    html, los comentarios blade no se muestran en el código HTML ya que queda a nivel backend.


Condicional if
**************
Las condiciones if se ejecutan con el tag **@if, @else, @endif**:

.. code-block:: php 
    :linenos:

    <h1>{{ $titulo }}</h1>

    {! Se crea la condición que se valida entre paréntesis igual que un if corriente !}
    @if($consolas)
        <ul>
            <li>Sony PlayStation</li>
            <li>Sega Megadrive</li>
            <li>Nintendo DS</li>
        </ul>
    @else 
        <p>No hay consolas disponibles</p>
    @endif 

.. note 
    se puede añadir un **@elseif($valor)** para validar otra condición adicional.

Bucle foreach
*************

Los bucles for se ejecutan con el tag **@foreach**:

.. code-block:: php 
    :linenos:

    <h1>{{ $titulo }}</h1>

    <ul>
    @foreach($consola as $consolas)
        <li>{{ $consolas }}</li>
    @endforeach
    </ul>

.. note::
    Se puede ejecutar el foreach clave => valor de un mismo modo que en PHP.

.. note::
    Existe del mismo modo el bucle for sencillo y el bucle while, sin embargo este tipo de estructuras es mejor utilizarlas en los controladores.


Plantilla Base
**************
Las plantillas base como en otros frameworks se utilizan para establecer las partes que serán genéricas en todas o la gran mayoría de páginas del proyecto,
estas plantillas se suelen guardar en la carpeta **layouts** la cual habrá que crear dentro de **views**. 

La plantilla base suele tener el nombre **base.blade.php**:

.. code-block:: php
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        {{-- es muy útil el uso de Yield para sustituir partes estratégicas: --}}
        <title>@yield('title')</title>
    </head>
    <body>
        {{-- Cada section muestra un bloque de contenido: --}}
        @section('header')
            <h1>Listado de consolas</h1>
        @show

        <div>
            {{-- con yield se define el contenido a sustituir --}}
            @yield('content')
        </div>

        @section('footer')
            <small>Laravel en Fullcoder</small>
        @show
    </body>
    </html>

- Lo siguiente será cargar la base en una plantilla como **listar-consolas.blade.php**:

.. code-block:: php  
    :linenos:

    {{-- Ahora se extiende la plantilla base: --}}
    @extends('layouts.base')

    {{-- Se reemplaza el title del sitio: --}}
    @section('title', 'Listado de consolas:')

    {{-- Se carga el section para sustituir el yield content con el listado de consolas: --}}
    @section('content')
    <ul>
        <li>Sony PlayStation</li>
        <li>Sega Megadrive</li>
        <li>Nintendo DS</li>
    </ul>
    @stop

    {{-- se puede añadir o cambiar el comportamiento de un bloque: --}}
    @section('footer')
        <p>Parte exclusiva en el footer de Listado de consolas</p>
        {{-- si se añade parent heredará el contenido original, sino sustituye el bloque completo --}}
        @parent 
    @stop

Includes
********
Se puede cargar otras vistas por ejemplo creando en la carpeta views una carpeta llamada **includes** y dentro se puede crear por ejemplo **header.blade.php**:

.. code-block:: php 
    :linenos:

    <h1>Soy una cabezera</h1>
    <hr>

Para cargar dicho header se accede a una plantilla blade como **consolas.blade.php**:

.. code-block:: php 
    :linenos:

    {! esta cabezera se puede añadir tantas veces como haga falta: !}
    @include('includes.header')

    <h1>Listado de consolas</h1>

    <ul>
        <li>Sony PlayStation</li>
        <li>Sega Megadrive</li>
        <li>Nintendo DS</li>
    </ul>

Enlaces a otras rutas
*********************

.. code-block:: php 
    :linenos:

    {{-- Con action se llama al metodo del controlador para crear el enlace: --}}
    <a href="{{ action('ConsolaController@index') }}">Listado de consolas</a>

.. note::
    Existe también el método **route()** pero para ello hay que definir un alias a la ruta.

Mostrar notificaciones
**********************

- Tenemos el caso en el que se elimina un registro:

.. code-block:: php 
    :linenos:

    public function borrarConsola($id){
        $consola = DB::table('lista_consolas')->where('id', $id)->delete();
        // se utiliza with para guardar datos en una sesión flash, osea que solo aparecerá 1 vez ideal para notificaciones:
        return redirect()->action('ConsolaController@index')->with('status', 'Consola eliminada con éxito');
    }

- En la vista se puede utilizar las sesiones para cargar el status que hemos creado:

.. code-block:: php
    :linenos:

    @extends('layouts.base')

    @section('title', 'Listado de consolas:')

    @section('content')
    <ul>
        @foreach($consolas as $consola)
        <li>{{ $consola->marca }}</li>
        @endforeach
    </ul>
    @stop

    @section('footer')
        <p>Parte exclusiva en el footer de Listado de consolas</p>
        @parent 
    @stop

    {{-- Con blade se muestran los datos almacenados en sesión via with: --}}
    @if(session('status'))
        <h3 style="color:red;">{{ session('status') }}</h3>
    @endif

Controladores en Laravel
########################

- Crear controlador: ``php artisan make:controller ConsolaController``
- Acceder al archivo del controlador en **Http/Controllers**:

.. code-block:: php
    :linenos:

    <?php

    // se crea un namespace para poder llamar al controlador:
    namespace App\Http\Controllers;

    // se recupera el request para las peticiones http:
    use Illuminate\Http\Request;

    // se genera una clase vacía que hereda de controller:
    class ConsolaController extends Controller
    {
        // crear una vista principal que devuelva el listado de consolas:
        public function index(){
            // tendrá un array de consolas:
            $consolas = ['Sony Playstation', 'Sega Megadrive', 'Gameboy'];

            // se retorna una vista:
            return view('consolas.listar-consolas', array(
                'consolas' => $consolas
            ));
        }
    }

- Ahora se llama al controlador desde las rutas:

.. code-block::
    :linenos:

    // La ruta recibe como segundo parámetro el controlador y tras la @ el método que ejecutar:
    Route::get('/consolas', 'ConsolaController@index');

.. note::
    La vista ahora se puede recorrer el valor con foreach para cargar las consolas en un listado.

Manejar parámetros en el controlador
************************************

.. code-block:: php 
    :linenos:

    <?php

    namespace App\Http\Controllers;

    use Illuminate\Http\Request;

    class ConsolaController extends Controller
    {
        // el método recibirá cada parámetro de la ruta con su nombre:
        public function consola($modelo){
            // listado de consolas:
            $consolasDetalle = [
                'playstation' => array(
                    'marca' => 'Sony',
                    'modelo' => 'Playstation',
                    'lanzamiento' => 1994
                )
                ];
            
            // dudoso modo de validar el índice:
            $modelo = $modelo ? $consolasDetalle[$modelo] : Null;
            
            // respuesta:
            return view('consolas.consola', array(
                'consola' => $modelo
            ));
        }
    }


Redirección a otra ruta
***********************

.. code-block:: php 
    :linenos:

    public function volver(){
        // se le pasa el método redirect y el método del controlador que va a disparar la acción:
        return redirect()->action('ConsolaController@index')
    }

Crear Crud y enrutamiento automático
************************************
Con Artisan se puede crear un CRUD completo y recuperar todas sus rutas de manera automática:

1. Crear controlador con CRUD: ``php artisan make:controller UserController --resource``
2. Crear ruta con método **resources()**:

.. code-block:: php 
    :linenos:

    // ruta de un CRUD completo:
    Route::resource('user', 'UserController');

3. Comprobar que existen las rutas nuevas: ``php artisan routes:list``

Y con esto ya existen todos los métodos de un CRUD. Muy útil para crear servicios REST.

Formularios
###########

- Crear un formulario en blade:

.. code-block:: php 
    :linenos:

    <h1>Formulario registro consola</h1>

    <form action="{{ action('ConsolaController@nuevaConsola') }}" method="POST">
        {{-- es imprescindible enviar el csrf para evitar fallos: --}}
        {{ csrf_field() }}
        <label for="marca">Marca: </label>
        <input type="text" name="marca" />
        <label for="modelo">Modelo: </label>
        <input type="text" name="modelo" />
        <label for="lanzamiento">Lanzamiento: </label>
        <input type="text" name="lanzamiento" />

        <input type="submit" value="registrar" />
    </form>

- Crear las rutas que muestran el formulario y la que recibe los datos:

.. code-block::
    :linenos:

    // rutas para el formulario:
    Route::get('/consolas/nueva', 'ConsolaController@nuevaConsola');
    Route::post('/consolas/nueva', 'ConsolaController@nuevaConsola');

- Crear un nuevo método en el controlador **ConsolaController** para mostrar formulario:

.. code-block:: php 
    :linenos:

    public function nuevaConsola(Request $request){
        $response = view('consolas.nuevaConsola');

        
        $marca = $request->input('marca');
        $modelo =  $request->input('modelo');
        $lanzamiento =  $request->input('lanzamiento');

        if($request->input('marca') && $request->input('modelo') && $request->input('lanzamiento')){
            $response = $marca . " " . $modelo . " fue lanzada en " . $lanzamiento;
        }
        
        return $response;
    }

Con este controlador se ha establecido la validación cuando reciba todos los datos mostrará una respuesta.

Bases de datos 
##############

Migraciones
***********

- Crear una nueva migración: ``php artisan make:migration create_consolas_table --table=lista_consolas``
- Las migraciones se encuentra en **database/migrations/** ahí se puede ver el archivo **create_consolas_table**:

.. code-block:: PHP
    :linenos:

    <?php

    use Illuminate\Support\Facades\Schema;
    use Illuminate\Database\Schema\Blueprint;
    use Illuminate\Database\Migrations\Migration;

    class CreateConsolasTable extends Migration
    {
        /**
        * Run the migrations.
        *
        * @return void
        */
        public function up() // up crea la tabla
        {   // se cambia el schema table por create para crear la tabla o fallará ya que no existe la tabla en mysql:
            Schema::create('lista_consolas', function (Blueprint $table) {
                // Se definen los campos:
                $table->increments('id'); // el tipo increments será autoincremental y por defecto primary key.
                $table->string('marca', 255);
                $table->string('modelo', 255);
                $table->integer('lanzamiento');
                // buena practica es crear un timestamps para registrar cambios en los datos:
                $table->timestamps();
            });
        }

        /**
        * Reverse the migrations.
        *
        * @return void
        */
        public function down() // borra la tabla
        {
            // se define el drop para eliminar la tabla:
            Schema::drop('lista_consolas');
        }
    }


- Lanzar todas la migraciones: ``php artisan migrate``
- Refrescar los cambios en las migraciones: ``php artisan migrate:refresh``

.. attention::
    Es necesario tener configurado el archivo **.env** para conectarse a la base de datos.

.. attention::
    Al refrescar las tablas se borran los registros.


Generar Seeders
***************

Los seeders se utilizan para rellenar datos de prueba en una aplicación:

- Lo primero es ejecutar el comando: ``php artisan make:seed lista_consolas_seed``
- En la carpeta **database/seeds/** se ha creado el archivo **lista_consolas_seed.php**:

.. code-block:: php 
    :linenos:

    <?php

    use Illuminate\Database\Seeder;

    class lista_consolas_seed extends Seeder
    {
        /**
        * Run the database seeds.
        *
        * @return void
        */
        public function run()
        {   
            // crear registros:
            $consolas = [
                array(
                    'marca' => 'Sega',
                    'modelo' => 'Dreamcast',
                    'lanzamiento' => 1998,
                    'n_ventas' => 2000000
                ),
                array(
                    'marca' => 'Nintendo',
                    'modelo' => 'WiiU',
                    'lanzamiento' => 2015,
                    'n_ventas' => 11000
                )
            ];

            // aquí se ejecuta la consulta que va a introducir en la base de datos una vez ejecutemos el seed:
            DB::table('lista_consolas')->insert($consolas);

            // lanzamos un mensaje por consola:
            $this->command->info('Se ha rellenado la tabla de lista_consolas');
        }
    }



- Ahora para lanzar el seed y que guarde los registros: ``php artisan db:seed --class=lista_consolas_seed``

.. attention::
    En caso de que indique un error de tipo **no se encuentra la clase lista_consolas_seed.php** habrá que ejecutar el comando ``composer dump-autoload`` para solucionar el problema.


Relaciones de tablas y tablas ya existentes
*******************************************

Aparte de las relaciones entre tablas veremos como tener un modelo que trabaja con una tabla que se creó desde mysql:

* Tabla con relación de uno a muchos (Category):

.. code-block:: php 
    :linenos:

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;

    class Category extends Model
    {
        use HasFactory;
        // tabla creada en mysql:
        protected $table = 'categories';

        // relación de uno a muchos:
        public function posts(){
            return $this->hasMany('App\Post');
        }
    }

* Tabla con relación inversa (Post):

.. code-block:: php 
    :linenos:

    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;

    class Post extends Model
    {
        use HasFactory;
        // tabla creada en mysql:
        protected $table = 'posts';

        // relación de uno a muchos inversa (muchos a uno):
        public function user(){
            return $this->belongsTo('App\Models\User', 'user_id');
        }

        public function category(){
            return $this->belongsTo('App\Models\Category', 'category_id');
        }
    }



Query Builder Laravel
*********************

Consultar datos
+++++++++++++++

.. code-block:: php 
    :linenos:

    public function index(){
            
            // consulta para listar datos:
            $consolas = DB::table('lista_consolas')->get();
            // recuperar solo registros concretos: 
            $consolas = DB::table('lista_consolas')->where('marca', '=', 'Sega')->get();
            // ordenar registros:
            $consolas = DB::table('lista_consolas')->orderBy('modelo', 'desc')->get();


            return view('consolas.listar-consolas', array(
                'consolas' => $consolas
            ));
        }

    public function consola($id){
        // buscar un registro:
        $consola = DB::table('lista_consolas')->where('id', '=', $id)->first();
        
        // respuesta:
        return view('consolas.consola', array(
            'consola' => $consola
        ));
    }

Insertar datos
++++++++++++++

.. code-block:: php 
    :linenos:

    public function nuevaConsola(Request $request){
        $response = view('consolas.nuevaConsola');

        
        $marca = $request->input('marca');
        $modelo =  $request->input('modelo');
        $lanzamiento =  $request->input('lanzamiento');
        $ventas = 0;

        if($marca && $modelo && $lanzamiento){
            // guardar registro:
            $consola = DB::table('lista_consolas')->insert(array(
                'marca' => $marca,
                'modelo' => $modelo,
                'lanzamiento' => $lanzamiento,
                'n_ventas' => $ventas
            ));

            $response = redirect()->action('ConsolaController@index');
        }
        
        return $response;
    }

Borrar registros 
++++++++++++++++

.. code-block:: php 
    :linenos:

    public function borrarConsola($id){
        // consulta para borrar registro:
        $consola = DB::table('lista_consolas')->where('id', $id)->delete();

        return redirect()->action('ConsolaController@index')->with('status', 'Consola eliminada con éxito');
    }

- En la vista se puede utilizar las sesiones para cargar el status que hemos creado:

.. code-block:: php
    :linenos:

    @extends('layouts.base')

    @section('title', 'Listado de consolas:')

    @section('content')
    <ul>
        @foreach($consolas as $consola)
        <li>{{ $consola->marca }}</li>
        @endforeach
    </ul>
    @stop

    @section('footer')
        <p>Parte exclusiva en el footer de Listado de consolas</p>
        @parent 
    @stop

    {{-- Con blade se muestran los datos almacenados en sesión via with: --}}
    @if(session('status'))
        <h3>{{ session('status') }}</h3>
    @endif

Actualizar registros
++++++++++++++++++++

.. code-block:: php 
    :linenos:

    public function editarConsola($id, Request $request){

        // primero se recupera el registro:
        

        if ($request->isMethod('post'))
        {
            $consola = DB::table('lista_consolas')->where('id', $id)->update(array(
                'marca' => $request->input('marca'),
                'modelo' => $request->input('modelo'),
                'lanzamiento' => $request->input('lanzamiento'),
                'n_ventas' => 0
            ));
            $response = redirect()->action('ConsolaController@consola', $id);

        }else{
            $consola = DB::table('lista_consolas')->where('id', $id)->first();
            $response = view('consolas.nuevaConsola', array(
                'consola' => $consola
            ));
        }
        
        return $response;
    }


- Se puede readaptar el formulario para que muestre los datos y alterne la respuesta:

.. code-block:: php 
    :linenos:

    <h1>Formulario registro consola</h1>

    <!-- Se establece un ternario para preguntar si recibe algun dato del controlador cambiar a edición -->
    <form action="{{ isset($consola) ? action('ConsolaController@editarConsola', $consola->id) : action('ConsolaController@nuevaConsola') }}" method="POST">
        {{ csrf_field() }}
        <label for="marca">Marca: </label> <!-- con or podemos decidir si hay algo o sino valor por defecto -->
        <input type="text" name="marca" value="{{ $consola->marca or '' }}" />
        <label for="modelo">Modelo: </label>
        <input type="text" name="modelo" value="{{ $consola->modelo or '' }}" />
        <label for="lanzamiento">Lanzamiento: </label>
        <input type="text" name="lanzamiento" value="{{ $consola->lanzamiento or '' }}"/>

        <input type="submit" value="registrar" />
    </form>


API Restful
###########

