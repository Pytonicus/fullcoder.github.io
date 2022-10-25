Framework: Codeigniter 3
========================

.. image:: /logos/logo-codeigniter.png
    :scale: 100%
    :alt: Logo Codeigniter
    :align: center


.. |date| date::
.. |time| date:: %H:%M

Documentación básica para trabajar con Codeigniter 3

.. contents:: Índice
  
Configuraciones
###############  
 
Creación del proyecto
*********************

- Descargar Codeigniter 3: ``https://www.codeigniter.com/download``
- Probar que está funcionando en la misma raiz desde consola: ``php -S localhost:8000``

.. attention:: 
    Este manual es para la versión 3, la versión 4 tiene cambios en su estructura entre otros.

.. attention::
    La versión 3 de Codeigniter funciona mínimo bajo la versión de PHP 5.6 mientras que la 4 como mínimo la 7.1

Estructura de Codeigniter 3
***************************
En la estructura de un proyecto Codeigniter 3 estas son las partes más importantes:

- **application**: directorio donde se encuentra la aplicación. Dentro de ella se encuentran las siguientes carpetas:
    - **config**: carpeta de configuración con diversos archivos los cuales se destacan **config.php**, **constants.php**, **database.php** y **routes.php**.
    - **controllers**: carpeta donde se irán añadiendo los controladores del proyecto.
    - **models**: carpeta donde se crearán los modelos de datos (en el caso de codeigniter 3 serán queries).
    - **views**: carpeta donde se crearán las vistas del proyecto.
- **index.php**: archivo principal del proyecto, es desde donde se ejecuta la aplicación en el servidor.
 


Rutas en Codeigniter 3 
######################

Las rutas en codeigniter se irán creando automáticamente a medida que vayamos añadiendo controladores y métodos siguiendo esta estructura:

- http://localhost:8000/controlador/metodo/parametro_1/parametro_2/

Vistas en CodeIgniter 3
#######################

Para crear una vista en Codeigniter 3 vamos a **application/views** y creamos un archivo por ejemplo **consolas_list.php**:

.. code-block:: php 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Listado de consolas</title>
    </head>
    <body>
        <h1>Listado de consolas</h1>

        <ul>
            <li>Sony PlayStation</li>
            <li>Sega Megadrive</li>
            <li>Nintendo DS</li>
        </ul>
    </body>
    </html>

Para cargar la vista en el controlador hacemos lo siguiente en **Consolas.php**:

.. code-block:: php 
    :linenos:

    <?php 
    defined('BASEPATH') OR exit('No direct script access allowed');

    class Consolas extends CI_Controller{
        public function index(){
            // cargar vista html:
            $this->load->view('consolas_list');
        }
    }

    /* Fin del archivo Consolas.php */


Uso de variables
****************
Las variables se pueden cargar desde el controlador del siguiente modo (Consolas.php): 

.. code-block:: php 
    :linenos:

    <?php 
    defined('BASEPATH') OR exit('No direct script access allowed');

    class Consolas extends CI_Controller{
        public function index(){
            // creamos una variable data con la información de una consola:
            $data['consola'] = 'Sony Playstation';
            // se la pasamos a la vista:
            $this->load->view('consolas_list', $data);
        }
    }

    /* Fin del archivo Consolas.php */

En la vista la mostramos del siguiente modo (consolas_list.php): 

.. code-block:: php 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Listado de consolas</title>
    </head>
    <body>
        <h1>Listado de consolas</h1>
        <!-- El contenido de la variable data se pasa como si fueran variables sueltas: -->
        <p><?php echo $consola ?></p>
    </body>
    </html>

Controladores en CodeIgntier 3
##############################

- Para crear un controlador accedemos a la carpeta **application** y dentro a la carpeta **controllers**, ahí creamos un controlador al que llamamos por ejemplo **Consolas.php**:

.. code-block:: php
    :linenos:

    <?php 
    // copiamos este código de welcome.php para evitar accesos no autorizados:
    defined('BASEPATH') OR exit('No direct script access allowed');
    // creamos la clase que estiende de CI_Controller:
    class Consolas extends CI_Controller{
        // creamos la función para controlar la primera vista index:
        public function index(){
            echo "Página de consolas";
        }
    }

    // en lugar de cerrar el código php comentamos el final del archivo:
    /* Fin del archivo Consolas.php */

- Las ruta se genera automáticamente en base al nombre del controlador, para la vista principal tendríamos la ruta: http://localhost:8000/index.php/consolas/ 
- Para cada vista individual tenemos por ejemplo en este caso: http://localhost:8000/index.php/consolas/index

.. important::
    Asegúrate siempre de que el nombre del archivo y la clase sean exactamente el mismo o las rutas podrían no funcionar.

Manejar parámetros en el controlador
************************************

- Para añadir parámetros al controlador basta con pasarle los parámetros al método que se vaya a ejecutar:

.. code-block:: php 
    :linenos:

    <?php 
    defined('BASEPATH') OR exit('No direct script access allowed');

    class Consolas extends CI_Controller{

        // parámetros get por el método:
        public function index($consola = null){
            echo $consola;
        }
    }

    /* Fin del archivo Consolas.php */

- Ojo! ahora como estamos recibiendo parametros en el index debemos indicar el método que se esta utilizando en la ruta, de este modo: http://localhost:8000/consolas/index/Switch

Redirección a otra ruta
***********************

- Para cargar el redireccionador lo recomendado es importar en el constructor el helper url:

.. code-block:: php 
    :linenos:

    <?php 
    defined('BASEPATH') OR exit('No direct script access allowed');

    class Consolas extends CI_Controller{
        // cargar el constructor:
        function __construct(){
            parent::__construct();
            // se carga el helper url:
            $this->load->helper('url');
        }

        public function index($consola = null){
            echo "Estás en el índice";
        }

        // creamos un método que nos redirija al indice:
        public function redirigir(){
            // ejecutamos la función redirect y le decimos a que metodo tiene que viajar:
            redirect('/consolas/index/', 'refresh');
        }
    }

    /* Fin del archivo Consolas.php */

- Si ejecutamos localhost:8000/consolas/redirigir nos llevará al index de consolas via redireccionamiento. 

.. note::
    Si queremos viajar al index de un controlador basta con escribir el nombre del mismo: ``redirect('consolas')``que en el caso expuesto sería lo mas adecuado.

Formularios
###########

Crear un formulario con Codeigniter 3
*************************************

- Desde el controlador llamar al helper form (consolas.php):

.. code-block:: php 
    :linenos:

    class Consolas extends CI_Controller{
    
        function __construct(){
            parent::__construct();
            $this->load->model('Consolas_model');

            // utilizamos el helper form:
            $this->load->helper('form');
        }
        public function index(){

            $consolas_list = $this->Consolas_model->get_all();

            if(empty($consolas_list)){
                $data['consolas_list'] = "No existen consolas";
            }

            $data['consolas_list'] = $consolas_list;
                
            $this->load->view('consolas_list', $data);
        }

        // crear un controlador para el create:
        public function add(){
            // recibir información por POST:
            if($this->input->post()){
                $data['new_console'] = $this->input->post(); 
            }else{
                $data['new_console'] = "pendiente de resultados";
            }
            // cargamos la vista:
            $this->load->view('add_consola', $data);

        }
    }

- en una nueva vista a la que llamamos **add_consola.php** le cargamos el formulario:

.. code-block:: php 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Añadir consola</title>
    </head>
    <body>
    <h1>Añadir consola</h1>
    <hr/>
    <br/>

    <!-- creamos una variable para construir la estructura de cada campo: -->
    <?php 
        $input_marca = array(
            'name' => 'marca',
            'id' => 'marca',
            'class' => 'input_marca'
        );
        $input_modelo = array(
            'name' => 'modelo',
            'id' => 'modelo',
            'class' => 'input_modelo'
        );
        // en caso de ser un desplegable tendremos dos arrays:
        $input_en_coleccion = array(
            'name' => 'en_coleccion',
            'id' => 'en_coleccion',
            'class' => 'input_en_coleccion'
        );
        $en_coleccion = array(
            '0' => 'No',
            '1' => 'Si'
        );
    ?>

    <!-- Al construir el formulario con el helper el action se construye a partir de la ruta del controlador -->
    <?php 
        echo form_open('');
        
        echo form_label('Marca', 'marca');
        echo form_input($input_marca);
        echo "<br/><br/>";
        echo form_label('Modelo', 'modelo');
        echo form_input($input_modelo);
        echo "<br/><br/>";
        echo form_label('En posesión', 'en_posesion');
        echo form_dropdown($input_en_coleccion,$en_coleccion);
        echo "<br/><br/>";
        echo form_submit('btn_consola', 'añadir consola');
        echo form_close();
    ?>

    <hr />
    <!-- aquí mostramos el resultado: -->
    <pre><?php echo var_dump($new_console); ?></pre>
    </body>
    </html>

- Ahora tenemos el formulario para añadir consolas en http://localhost:8000/consolas/add

.. note:: 
    Si estamos usando un puerto de salida distinto al 80 deberemos modificar el parámetro **base_url** en la ruta **config/config.php**, modificamos el valor del array 
    con un valor por ejemplo: ``$config['base_url'] = 'http://localhost:8000';``

Bases de datos 
##############

Crear base de datos
*******************

- Instala MariaDB si estas usando linux o busca y servidor Wamp o xamp que soporte Mysql 5, con la versión de Mysql 8 tendrás problemas.
- Ejecutamos en el terminal **sudo mysql** y creamos una base de datos llamada **curso_codeigniter**:

.. code-block::

    CREATE DATABASE curso_codeigniter;


- Creamos un nuevo usuario:

.. code-block:: sql 
    :linenos:

    CREATE USER 'guillermo'@'localhost' IDENTIFIED BY '1234';

- Le otorgamos privilegios en la base de datos nueva:

.. code-block:: sql 
    :linenos:

    GRANT ALL PRIVILEGES ON curso_codeigniter.* TO 'guillermo'@'localhost';

- Desplegar los privilegios para que se puedan usar ya:

.. code-block:: sql 
    :linenos:

    FLUSH PRIVILEGES;

- Seleccionamos la base de datos:

.. code-block:: sql 
    :linenos:

    USE curso_codeigniter;

- creamos la tabla consolas:

.. code-block:: sql 
    :linenos:

    CREATE TABLE consolas (
        id INT auto_increment NOT NULL,
        marca varchar(100) NULL,
        modelo varchar(100) NULL,
        PRIMARY KEY(id)
    )
    ENGINE=InnoDB;

- Creamos unos registros para tener datos que listar a continuación:

.. code-block:: sql 
    :linenos:
    
    INSERT INTO consolas VALUES
        (NULL, "sony", "playstation"),
        (NULL, "nintendo", "switch"),
        (NULL, "sega", "mega drive"),
        (NULL, "microsoft", "xbox");

Con esto ya tenemos todo lo necesario para trabajar.

Conectar a la base de datos 
***************************

- En el proyecto nos vamos a **application/config/database.php** y al final editamos el array **$db['default']**:

.. code-block:: php 
    :linenos:

    $db['default'] = array(
        'dsn'	=> '',
        'hostname' => 'localhost', // localhost el servidor 
        'username' => 'guillermo', // este es el usuario para conectar
        'password' => '1234', // la contraseña en blanco si no definimos una
        'database' => 'curso_codeigniter', // el nombre de la base de datos
        'dbdriver' => 'mysqli',
        'dbprefix' => '',
        'pconnect' => FALSE,
        'db_debug' => (ENVIRONMENT !== 'production'),
        'cache_on' => FALSE,
        'cachedir' => '',
        'char_set' => 'utf8',
        'dbcollat' => 'utf8_general_ci',
        'swap_pre' => '',
        'encrypt' => FALSE,
        'compress' => FALSE,
        'stricton' => FALSE,
        'failover' => array(),
        'save_queries' => TRUE
    );

Crear modelo de datos y READ 
****************************

Para crear un modelo de datos nos vamos a **application/models** y creamos un archivo por ejemplo **Consolas_model.php**:

.. code-block:: php 
    :linenos:

    <?php 
    // creamos una clase para el modelo:
    class Consolas_model extends CI_Model {
        // preparamos el constructor:
        function __construct(){
            parent::__construct();
            // cargamos la base de datos:
            $this->load->database();
        }

        // creamos una función para traer del modelo todos los registros:
        public function get_all(){
            // recuperar datos de la tabla:
            $query = $this->db->get('consolas');
            // devolvemos la información:
            return $query->result();
        }
    }    

    /* Fin del archivo Consolas_model.php */

- En el controlador realizamos la consulta **Consolas.php**:

.. code-block:: php 
    :linenos:

    <?php 
    defined('BASEPATH') OR exit('No direct script access allowed');

    class Consolas extends CI_Controller{

        function __construct(){
            parent::__construct();
            // cargamos el modelo en el constructor:
            $this->load->model('Consolas_model');
        }

        public function index(){

            // utilizamos el método para recuperar los datos del la tabla:
            $consolas_list = $this->Consolas_model->get_all();

            // comprobamos si está vacío:
            if(empty($consolas_list)){
                // pasamos al data que no existen consolas:
                $data['consolas_list'] = "No existen consolas";
            }

            // asignamos a la data la lista:
            $data['consolas_list'] = $consolas_list;
                
            // se la pasamos a la vista:
            $this->load->view('consolas_list', $data);
        }
    }

    /* Fin del archivo Consolas.php */


- Por úlitmo en el template lo mostramos **consolas_list.php**:

.. code-block:: php 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Listado de consolas</title>
    </head>
    <body>
        <h1>Listado de consolas</h1>
        <!-- El contenido de la variable data se pasa como si fueran variables sueltas: -->
        <ul>
            <?php foreach($consolas_list as $key => $consola){
                echo "<li>" . $consola->marca . " " . $consola->modelo . "</li>";
            }
            ?>
        </ul>
    </body>
    </html>

- Ahora si vamos a la ruta http://localhost:8000/consolas veremos la lista creada en la base de datos.

.. attention::
    Es posible que tengamos que habilitar la extensión **mysqli.dll** quitando el ; de la línea correspondiente en el archivo **php.ini** 


Insertar datos
**************

- En el modelo añadimos una nueva función en **Consolas_model.php**:

.. code-block:: php 
    :linenos:

    <?php 

    class Consolas_model extends CI_Model {
        
        function __construct(){
            parent::__construct();
            $this->load->database();
        }

        public function get_all(){
            $query = $this->db->get('consolas');
            return $query->result();
        }
        // creamos una función para insertar datos:
        public function create(){
            // recuperamos los datos recibidos por post:
            $data = $this->input->post();
            // quitamos el botón submit que se reconoce como un input mas y da error (tambien quitamos el campo en_coleccion que tampoco existe en la tabla):
            unset($data['btn_consola']);
            unset($data['en_coleccion']);
            // insertamos los datos recibidos por post pasandole a insert la tabla y la operación post:
            $this->db->insert('consolas', $data);

            // retornamos el resultado:
            return $this->db->insert_id();
        }
    }    

    /* Fin del archivo Consolas_model.php */

- A continuación editamos el controlador **Consolas.php**:

.. code-block:: php 
    :linenos:

    <?php 
    defined('BASEPATH') OR exit('No direct script access allowed');

    class Consolas extends CI_Controller{
        function __construct(){
            parent::__construct();
            $this->load->model('Consolas_model');
            $this->load->helper('form');
        }

        public function index(){

            $consolas_list = $this->Consolas_model->get_all();

            if(empty($consolas_list)){
                $data['consolas_list'] = "No existen consolas";
            }

            $data['consolas_list'] = $consolas_list;
                
            $this->load->view('consolas_list', $data);
        }

        public function add(){

            if($this->input->post()){
                // si llegan valores por post vamos a insertarlos:
                $id_result = $this->Consolas_model->create();
                // para hacer pruebas le pasamos a new_console el id resultante:
                $data['new_console'] = $id_result; 
            }else{
                $data['new_console'] = "pendiente de resultados";
            }


            $this->load->view('add_consola', $data);

        }
    }

    /* Fin del archivo Consolas.php */

- Y ya solo falta nuestro formulario que lo hemos podido crear en la sección **Formularios**.

Borrar registros 
****************

- Creamos una nueva función en el modelo **Consolas_model.php**:

.. code-block:: php 
    :linenos:

    <?php 

    class Consolas_model extends CI_Model {
        
        function __construct(){
            parent::__construct();
            $this->load->database();
        }

        public function get_all(){
            $query = $this->db->get('consolas');
            return $query->result();
        }

        public function create(){
            $data = $this->input->post();

            unset($data['btn_consola']);
            unset($data['en_coleccion']);

            $this->db->insert('consolas', $data);

            return $this->db->insert_id();
        }

        // para eliminar creamos una nueva función delete que recibirá un id:
        public function delete($id){
            if($id){
                // buscamos el id del elemento a eliminar en la tabla:
                $this->db->where('id', $id);
                // decimos que se debe borrar de la tabla correspondiente:
                $this->db->delete('consolas');
            }
        }
    }    

    /* Fin del archivo Consolas_model.php */

- Ahora pasamos al controlador **Consolas.php**:

.. code-block:: php
    :linenos:

    <?php 
    defined('BASEPATH') OR exit('No direct script access allowed');

    class Consolas extends CI_Controller{
        function __construct(){
            parent::__construct();
            $this->load->model('Consolas_model');
            $this->load->helper('form');
            // cargamos el helper url para poder hacer redirecciones:
            $this->load->helper('url');
        }

        public function index(){

            $consolas_list = $this->Consolas_model->get_all();

            if(empty($consolas_list)){
                $data['consolas_list'] = "No existen consolas";
            }

            $data['consolas_list'] = $consolas_list;
                
            $this->load->view('consolas_list', $data);
        }

        public function add(){

            if($this->input->post()){
                $id_result = $this->Consolas_model->create();
                $data['new_console'] = $id_result; 
            }else{
                $data['new_console'] = "pendiente de resultados";
            }


            $this->load->view('add_consola', $data);
        }

        // creamos una nueva función para eliminar un contacto:
        public function delete($id = null){
            // comprobamos que recibimos un id:
            if($id){
                // realizamos la eliminación del elemento:
                $this->Consolas_model->delete($id);
            }

            // redirigimos a la lista:
            redirect('consolas');
        }
    }

    /* Fin del archivo Consolas.php */

- Si vamos a la ruta siguiente y vamos cambiando el numero id se borraran los registros que tengan dicho id: localhost:8000/index.php/consolas/delete/1

Actualizar registros
********************

- Como en los  otros casos comenzamos con el modelo que estabamos usando **Consolas_model.php**:

.. code-block:: php 
    :linenos:

    <?php 

    class Consolas_model extends CI_Model {
        
        function __construct(){
            parent::__construct();
            $this->load->database();
        }

        public function get_all(){
            $query = $this->db->get('consolas');
            return $query->result();
        }

        public function create(){
            $data = $this->input->post();

            unset($data['btn_consola']);
            unset($data['en_coleccion']);

            $this->db->insert('consolas', $data);

            return $this->db->insert_id();
        }

        public function delete($id){
            if($id){
                $this->db->where('id', $id);
                $this->db->delete('consolas');
            }
        }

        // creamos una metodo para traer una consola:
        public function get($id){
            if($id){
                $query = $this->db->where('id', $id);
                $query = $this->db->get('consolas');

                // retornamos el resultado:
                return $query->result();
            }
        }

        // creamos un método para actualizar un registro:
        public function update($id){
            // recuperamos los datos de post y quitamos el botón:
            $update_data = $this->input->post();
            unset($update_data['btn_consola']);

            // buscamos el registro que queremos modificar:
            $this->db->where('id', $id);
            // registramos los cambios:
            $this->db->update('consolas', $update_data);
    
        }
    }    

    /* Fin del archivo Consolas_model.php */


- Continuamos por el controlador **Consolas.php**:

.. code-block:: php 
    :linenos:

    <?php 
    defined('BASEPATH') OR exit('No direct script access allowed');

    class Consolas extends CI_Controller{
        function __construct(){
            parent::__construct();
            $this->load->model('Consolas_model');
            $this->load->helper('form');
            // recuerda tener el helper de redirecciones cargado:
            $this->load->helper('url');
        }

        public function index(){

            $consolas_list = $this->Consolas_model->get_all();

            if(empty($consolas_list)){
                $data['consolas_list'] = "No existen consolas";
            }

            $data['consolas_list'] = $consolas_list;
                
            $this->load->view('consolas_list', $data);
        }

        public function add(){

            if($this->input->post()){
                $id_result = $this->Consolas_model->create();
                $data['new_console'] = $id_result; 
            }else{
                $data['new_console'] = "pendiente de resultados";
            }


            $this->load->view('add_consola', $data);
        }

        public function delete($id = null){
            if($id){
                $this->Consolas_model->delete($id);
            }

            redirect('consolas');
        }

        // crear un nuevo metodo para actualizar registros:
        public function update($id = null){
            // vamos a redireccionar si no nos llega un id:
            if($id == null){
                redirect('consolas');
            }else{
                // si nos llega algo cargamos los datos haciendo una consulta:
                $data['consola'] = $this->Consolas_model->get($id);
                // si no recuperamos nada (no existe el registro) regresamos a la lista:
                if(empty($data['consola'])){
                    redirect('consolas');
                }
            }

            // verificamos si recibimos valores vía post:
            if($this->input->post()){
                $this->Consolas_model->update($id);
                redirect('consolas');
            }

            // cargamos la vista para actualizar consolas:
            $this->load->view('update_consola', $data);
        }
    }

    /* Fin del archivo Consolas.php */

- Finalmente creamos una vista similar a la que tenemos  para crear registros y la llamamos **update_consola.php**:

.. code-block:: php 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Actualizar consola</title>
    </head>
    <body>
    <h1>Actualizar consola</h1>
    <hr/>
    <br/>

    <!-- pasamos el resultado del data por el atributo value: -->
    <?php 
        $input_marca = array(
            'name' => 'marca',
            'id' => 'marca',
            'class' => 'input_marca',
            'value' => set_value('marca', $consola[0]->marca) // para establecer un valor en el formulario se usa set_value()
        );
        $input_modelo = array(
            'name' => 'modelo',
            'id' => 'modelo',
            'class' => 'input_modelo',
            'value' => set_value('modelo', $consola[0]->modelo)
        );
        $en_coleccion = array(
            '0' => 'No',
            '1' => 'Si'
        );
    ?>

    <!-- Hemos quitado el selector porque no lo vamos a usar -->
    <?php 
        echo form_open('');
        
        echo form_label('Marca', 'marca');
        echo form_input($input_marca);
        echo "<br/><br/>";
        echo form_label('Modelo', 'modelo');
        echo form_input($input_modelo);
        echo "<br/><br/>";
        echo form_submit('btn_consola', 'actualizar consola');
        echo form_close();
    ?>

    <hr />
    </body>
    </html>

- Si vamos por ejemplo a la ruta: http://localhost:8000/index.php/consolas/update/2 podremos actualizar el registro si existe. Si dicho registro no existe establecimos que hiciera un redireccionamiento a la lista.

