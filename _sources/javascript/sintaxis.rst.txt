Sintaxis javascript
===================

.. image:: /logos/JavaScript-logo.png
    :scale: 25%
    :alt: Logo JavaScript
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Sintáxis básica de JavaScript
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################

Instalación
***********
* Instalación: No se requiere, con un navegador compatible como Chrome o Firefox es suficiente.
* Extensión de archivos: **.js**
 
Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: javascript
    :linenos:
 
    // comentario de una sola linea

* Comentarios multilínea:

.. code-block:: javascript
    :linenos:

    /* Comentario 
    multilinea 
    en Javascript */

Entrada y salida estandar
*************************
Datos de entrada y salida a través de la consola y/o el navegador.

.. code-block:: javascript 
    :linenos:

    // Ejecutar ventana emergente:
    alert('Soy un mensaje emergente');

    // retorno en consola:
    console.log("Mensaje desde consola");

    // Entrada desde ventana emergente:


Estructura en javascript
************************

* Código javascript puro:

.. code-block:: javascript
    :linenos:

    // Ejemplo de carga Javascript cuando todo el DOM está listo:
    document.addEventListener('DOMContentLoaded', () => {
            alert("Soy una alerta JavaScript");
        });

* código javascript junto a HTML:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <p>Soy un párrafo</p>
        <script type="text/javascript">
            document.addEventListener('DOMContentLoaded', () => {
                alert("Soy una alerta JavaScript");
            });
        </script>
    </body>
    </html>


* Cargar JavaScript en HTML:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <p>Soy un párrafo</p>
        <script src="script.js"></script>
    </body>
    </html>

Concatenación
*************
Concatenación de variables y cadenas se realiza con **+**

.. code-block:: javascript 
    :linenos:

    var nombre = "Guillermo";

    // Concatenación básica:
    console.log("Te llamas " + nombre);

    // uso de templates: 
    console.log(`te llamas ${nombre}`);

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: javascript 
    :linenos:

    // declaración y asignación variable global:
    var consola = "PlayStation";

    // variable local de alcance limitado:
    let consola = "PlayStation";

    // tipos:
    var cadena = "Cadena de texto";
    var entero = 150;
    var decimal = 10.25;
    var booleano = true;


.. attention:: 
    var se utiliza comunmente para declarar variables que se van a usar en cualquier parte del codigo,
    esto implica que pueden suceder posibles errores y conflitos si se agranda el código. Por ello se 
    recomienda el uso de let especialmente en funciones y otros ámbitos para limitar su uso en otras partes.
    
* Constantes:

.. code-block:: javascript
    :linenos:

    const nacimiento = 1987;

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: javascript 
    :linenos:

    var suma = 10 + 20;
    var resta = 10 - 10;
    var multiplicar = 10 * 2;
    var division = 6 / 2;
    var resto = 10 % 3;

* Incremento y decremento:

.. code-block:: javascript 
    :linenos:

    // Incremento
    var dato = 10;
    dato++
    // decremento:
    dato--

* Asignar operación:

.. code-block:: javascript 
    :linenos:

    suma += 10 ;
    resta -= 10;
    multiplicar *= 10;
    division /= 6;
    resto %= 10;

Operadores relacionales
***********************
Validación entre dos números.

* Mayor que: **>**.
* Menor que: **<**.
* Mayor o igual que: **>=**.
* Menor o igual que: **<=**.
* Igual que: **==**.

Operadores lógicos
******************
Expresiones de operaciones lógicas.

* and: **&&**.
* or: **||**.
* not: **!**.

Estructuras de control
######################

Condicional if
**************

* if sencillo:

.. code-block:: javascript 
    :linenos:

    // variables:
    var numA = 11;
    var numB = 15;

    // comprobar cual es mayor:
    if(numA > numB){
        console.log("Número A es mayor que número B");
    }

* if / else:

.. code-block:: javascript 
    :linenos:

    // variables:
    var numA = 11;
    var numB = 15;

    // comprobar cual es mayor:
    if(numA > numB){
        console.log("Número A es mayor que número B");
    }else{
        console.log("Número B es mayor que número A");
    }

* else-if:

.. code-block:: javascript 
    :linenos:

    // variables:
    var numA = 15;
    var numB = "15";

    // comprobar cual es mayor:
    if(numA > numB){
        console.log("Número A es mayor que número B");
    }else if(numA === numB){
        console.log("Son idénticos");
    }else if(numA == numB){
        console.log("Son parecidos pero uno es String");
    }else{
        console.log("Número B es mayor que número A");
    }

.. attention::
    En este ejemplo se observa una === ya que en JavaScript al comparar dos números con == si uno es cadena
    devuelve true la condición, en este caso si quitamos las comillas de numB se cumplirá la condición === que 
    está antes.

* Operador ternario:

.. code-block:: javascript 
    :linenos:

    // variables:
    var numA = 11;
    var numB = 15;

    // comprobar cual es mayor:
    var total = numA > numB ? "Número A es mayor que número B" : "Número B es mayor que número A";

    console.log(total);

Condicional Switch
******************
Estructura de un switch:

.. code-block:: javascript 
    :linenos:

    var nota = 6;

    // asignamos la variable a evaluar dentro del switch:
    switch(nota){
        // Vamos asignando casos a evaluar:
        case 0:
            console.log("Suspenso");
            break;
        case 1:
            console.log("Suspenso");
            break;
        case 2:
            console.log("Suspenso");
            break;
        case 3:
            console.log("Suspenso");
            break;
        case 4:
            console.log("Suspenso");
            break;
        case 5:
            console.log("Suficiente");
            break;
        case 6:
            console.log("Aprovado");
            break;
        case 7:
            console.log("Bien");
            break;
        case 8:
            console.log("Notable");
            break;
        case 9:
            console.log("Notable Alto");
            break;
        case 10:
            console.log("Sobresaliente");
            break;
        default:
            console.log("No reconozco la nota"); 
    }

Bucle for
*********

* for básico:

.. code-block:: javascript 
    :linenos:

    // introducir un valor:
    var tabla = prompt("Introduce una tabla");

    // recorrer valor e incrementar la tabla
    for(let i = 1; i <= 10; i++){
        console.log(`${tabla} x ${i} = ${tabla * i}`);
    }

* foreach:

.. code-block:: javascript 
    :linenos:

    // Array de valores:
    var consolas = ["PlayStation", "MegaDrive", "GameBoy", "Super Nintendo"];

    // recorrer valor e incrementar la tabla
    for(let i in consolas){
        console.log("Consola: " + consolas[i]);
    }


Bucle while
***********

* While sencillo:

.. code-block:: javascript 
    :linenos:

    var productos = 5;

    while(productos >= 0){
        console.log("Productos en stock: º " + productos);
        productos--;
    }

* do-while:

.. code-block:: javascript 
    :linenos:

    var productos = 0;

    do{
        console.log("Quedan: " + productos + " artículos");
        productos --;
    }while(productos >= 0);

Detener secuenda de script
**************************

.. code-block:: javascript
    :linenos:

    for(let i = 0; i < 10; i++){

        console.log("Valor es igual a: " + i);
        
        if(i > 5){
            console.log("Una pausita");
            // Rompemos la instrucción.
            break;
        }
    }
    console.log("Fuera del ciclo");


Tipos de datos avanzados
########################

Arrays
******

- Declaración tradicional:

.. code-block:: javascript 
    :linenos:

    var consolas = ["PlayStation", "MegaDrive", "Saturn"];
    
    console.log(consolas[2]);

- Array multidimensional:

.. code-block:: javascript 
    :linenos:

    var domesticas = ["PlayStation", "MegaDrive", "Saturn"];
    var portatiles = ["GameBoy", "PSP", "PS Vita"];

    var consolas = [domesticas, portatiles];

    console.log(consolas[1][2]);

    // nueva portatil:
    consolas[1].push("3DS");
    console.log(consolas[1][3]);

* Desestructuración de Arrays:

.. code-block:: javascript 
    :linenos:

    // array:
    var consolas = ["PlayStation", "MegaDrive", "Saturn"];
    
    // desestructuración:
    var [consola1, consola2, consola3] = consolas;

    console.log(`${consola1}, ${consola2}, ${consola3}`);

Objetos literales
*****************

* Declaración tradicional:

.. code-block:: javascript 
    :linenos:

    var objeto = {
        "nombre":"Pepe", 
        "apellidos": "García Gámez",
        "edad": 27,
        "casado": false,
        "aficiones": ["golf", "esquiar", "pescar"]
        };

    console.log(`${objeto.nombre} ${objeto.apellidos} tiene ${objeto.edad} años.`);

* Recorrer valores en array de objetos:

.. code-block:: javascript 
    :linenos:

    // lista de consolas:
    var consolas = [
        {"nombre": "PlayStation", "lanzamiento": 1994},
        {"nombre": "PlayStation 2", "lanzamiento": 2001},
        {"nombre": "PSP", "lanzamiento": 2005}
    ];
    
    for(let objeto in consolas){
        console.log(`La videoconsola ${consolas[objeto].nombre} fue lanzada en ${consolas[objeto].lanzamiento}`);
    }

* Desestructuración de objetos:

.. code-block:: javascript 
    :linenos:
    
    // objeto:
    var persona = {"nombre": "Alfredo", "apellidos": "Lopez Gavilán"};
    

    // desestructuración:
    var {nombre, apellidos} = persona;

    console.log(`${nombre} ${apellidos}`);

Control de errores
##################

.. code-block:: javascript
    :linenos:

    try{
        var boton = document.getElementById("boton");
        // Cremos un error a proposito:
        boton.addEventListener("DOMContentLoaded", ()=>{
            console.log("Has pulsado");
        });
    }catch(e){
        console.log("Error al activar listener: " + e);
    }

Programación modular
####################
 
Funciones
*********

* Procedimienos:

.. code-block:: javascript 
    :linenos:

    function saludar(){
        var saludo = "Hola mundo";
        console.log(saludo);
    }

* funciones:

.. code-block:: javascript 
    :linenos:

    function saludar(){
        var saludo = "Hola mundo";
        return saludo;
    }

* uso de parámetros:

.. code-block:: javascript 
    :linenos:

    function saludar(nombre, edad){
        var resultado = "Hola " + nombre + ", tienes " + edad + " años.";
        return resultado;
    }

    var mensaje = saludar("Guillermo", 31);

    console.log(mensaje);

* Parametros REST:

.. code-block:: javascript 
    :linenos:

    // REST envia un número indefinido de parámetros separados por coma:
    function consolasFavoritas(...consolas){
        console.log("Mis consolas favoritas: " + consolas);
    }

    consolasFavoritas("PlayStation", "MegaDrive", "GameBoy", "GameCube");

* Operador SPREAD:

.. code-block:: javascript
    :linenos:

    // podemos asignarle el parámetro rest para recibir los valores SPREAD:
    function cocinar(ingrediente1, ingrediente2, ingrediente3, ...otros){
        console.log("Necesitamos: " + ingrediente1 + ", " + ingrediente2 + ", " + ingrediente3 + ", " + otros);
    }
    // Especias:
    var especias = ['Ajo', ' Mezcla cajún'];

    // Y pasarle parámetros SPREAD:
    cocinar("Pollo", "Pan rallado", "huevos", ...especias);

* Funciones anónimas:

.. code-block:: javascript 
    :linenos:

    // Función anónima asignada a una variable:
    var saludar = function(nombre){
        var mensaje = "Hola de nuevo " + nombre;
        return mensaje;
    }

    var persona = prompt("¿Quíen eres?");

    // invocamos la función a través de su variable:
    console.log(saludar(persona));

* Arrow Functions:

.. code-block:: javascript 
    :linenos:

    // Creamos una variable y le psamos una función lambda:
    var saludar = (nombre)=>{
        console.log("Hola " + nombre);
    }

    // Inicializamos la variable como una función:
    saludar("Guillermo");

* Callbacks:

.. code-block:: javascript 
    :linenos:

    // Creamos una función normal a la que le pasamos un callback llamado sumarCB:
    function calcular(datoA, datoB, sumarCB){
        var suma = datoA + datoB;
        // Ejecutamos la función callback pasándole la variable suma:
        sumarCB(suma);
    }

    // Ejecutamos la función calcular y creamos la función callback que recibirá arriba:
    calcular(2, 3, (resultado) => {
        // La función callback imprimirá el valor que recibe de la función anterior:
        console.log(resultado);
    });

Programación orientada a objetos
################################

Los elementos de una clase se definen con ámbito **public**, **private** y **protected**. 
Adicionalmente se puede agregar el modificador **static** para poder acceder a los atributos y métodos sin crear un objeto.

Clases y objetos
****************

* Estructura clase:

.. code-block:: javascript 
    :linenos:

    // clase:
    class Consola{
        // Los atributos se inicializan en el constructor:
        constructor(marca, modelo, lanzamiento){
            // atributos:
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
        }

        // metodos:
        saberConsola(){
            console.log(`Es una ${this.marca} ${this.modelo} que apareció en el año ${this.lanzamiento}`);
        }
    }

* Get y Set:

.. code-block:: javascript 
    :linenos:

    class Consola{
        constructor(marca, modelo, lanzamiento){
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
        }

        saberConsola(){
            console.log(`Es una ${this.marca} ${this.modelo} que apareció en el año ${this.lanzamiento}`);
        }

        // get y set:
        get marca(){
            return this.marca;
        }

        set marca(value){
            this.marca = value;
        }
    }

* Creación de objeto:

.. code-block:: javascript
    :linenos:

        // crear objeto:
        var consola = new Consola("Sony", "PlayStation", 1994);
        // utilizar un método:
        consola.saberConsola();
        // asignar nuevo valor:
        consola.modelo = "Play Station";
        // asignar con set atributo:
        consola.marca = "Nintendo";
        // devolver un valor con get:
        console.log(consola.marca);

        consola.saberConsola();

* Herencia:

.. code-block:: javascript 
    :linenos:

    class Consola{
        constructor(marca, modelo, lanzamiento){
            this.marca = marca;
            this.modelo = modelo;
            this.lanzamiento = lanzamiento;
        }

        saberConsola(){
            console.log(`Es una ${this.marca} ${this.modelo} que apareció en el año ${this.lanzamiento}`);
        }
    }

    // clase hija:
    class PlayStation extends Consola{
        constructor(...juegosFamosos){
            // pasar atributos al constructor padre usando el superconstructor:
            super("Sony", "PlayStation", 1994);

            this.juegosFamosos = juegosFamosos;
        }

        saberJuegos(){
            console.log(`Los juegos más famosos de ${this.modelo} son ${this.juegosFamosos}`);
        }
    }

    var playstation = new PlayStation("Metal Gear Solid", "Tekken", "Final Fantasy");
    // cargar metodo de la clase hija:
    playstation.saberJuegos();
    // cargar metodo de la clase padre:
    playstation.saberConsola();



Importar y exportar
###################

* En el archivo **HTML** cargar el script principal como un módulo:

.. code-block:: html 
    :linenos:

    <script src="main.js" type="module"></script>

* Exportar función:

.. code-block:: javascript 
    :linenos:

    function saludar(nombre){
        console.log("Hola " + nombre);
    }

    export default saludar;

* Importar función:

.. code-block:: javascript 
    :linenos:

    import saludar from './saludar.js';

    saludar("Guillermo");
