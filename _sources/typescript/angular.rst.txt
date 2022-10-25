Framework: Angular
==================

.. image:: /logos/logo-angular.png
    :scale: 20%
    :alt: Logo Angular
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica de Angular 12

.. contents:: Índice
 
Configuraciones
###############  
   
Instalación de Angular CLI
**************************
Para gestionar Angular hay que instalar Angular CLI: ``npm install -g @angular/cli``

.. note::
    Para instalar en Linux utilizar el comando ``sudo npm install -g @angular/cli``

ANGULAR CLI y otros comandos 
############################
Para ejecutar un comando de Angular CLI el prefijo que se utiliza es ``ng``:

* Comprobar versión de angular/cli: ``ng --version``
* Crear proyecto: ``ng new nombre-proyecto``
* Levantar servidor y abrir navegador: ``ng serve -o`` (ruta por defecto: localhost:4200)
* Levantar en otro puerto: ``ng serve -o --port 4500``
* Crear un componente:  ``ng generate component nombre_componente``
* Crear componente en linea: ``ng generate component comonente_linea -s -t``
* Crear un pipe: ``ng generate pipe nombrePipe``
* Crear un servicio: ``ng generate service nombreServicio``
* Crear interface en angular: ``ng generate interface nombreInterface``
* Construir aplicación: ``ng build`` (se guarda en la carpeta dist)
* Instalar librerías en angular: ``ng add @angular/material``

Otros comandos útiles de npm
****************************
* Instalar todas las dependencias: ``npm install`` (no es un comando ng pero es importante recordarlo)
* Instalar servidor para aplicación construida: ``npm install -g serve``
* Ejecutar aplicación angular ya construida (desde su carpeta dentro de dist): ``serve``

.. attention::
    Para ejecutar en Windows estos comandos CLI se usará la aplicación ``nodejs command prompt`` o ejecutar con el prefijo ``npm run ng``

Estructura del proyecto 
#######################

Partes importantes del proyecto:

* package.json: archivo con las dependencias del proyecto.
* angular.json: se encuentra la configuración del proyecto.
* e2e: Carpeta test de integración 
* src: carpeta del proyecto en la cual vemos: 

    - index.html: pagina de entrada de la aplicación. 
    - main.ts: es donde se cargan los módulos.
    - style.css: estilos a nivel global.
    - test.ts: archivo para realizar tests.
    - enviorments: carpeta para variables de entornos.
    - assets: carpeta de archivos estáticos como imágenes.
    - app: carpeta del módulo principal donde se irá añadiendo el resto de componentes.

Componentes
###########

Los componentes se encuentran en la carpeta **src**.
Es ideal crear una carpeta **components** dentro de **src** para ordenarlos ya que se van a reutilizar en distintos módulos.
Cada componente se organizará en una carpeta con el siguiente contenido:

* Hoja de estilo CSS u otro tipo.
* Archivo HTML.
* Controlador Typescript.
* Modulo Typescript.

Crear un componente 
*******************

Para crear un componente se ejecuta el comando: ``ng generate component nombre_componente``
Crear componente dentro de una carpeta **components**: ``ng generate component components/menu``

* Lo primero que vamos a hacer es borrar el contenido del archivo **app.component.html** y lo reemplazamos por:

.. code-block::  
    :linenos:

    <div>
        <h1>Componente principal</h1>
        <hr>
        <app-menu></app-menu>
    </div>

* Ahora editamos el contenido de **menu.component.html**:

.. code-block::  
    :linenos:

    <div id="menu">
        <h2>Soy el menú</h2>
    </div>

* Y de paso editamos el css de menu en **menu.component.css**:

.. code-block:: css 
    :linenos:

    h2{
        color: red;
    }

Esto mostrará el título del módulo y el subtítulo del componente menú de color rojo.

.. attention::
    Mover la carpeta de un componente de forma manual causará fallos en la aplicación ya que no coincidirán las 
    rutas.

Crear componente en línea
*************************

Un componente en línea contiene en un solo archivo ts, la lógica, el código html y el código css:

* Crear componente en linea: ``ng generate component comonente_linea -s -t``

Data Binding
############

Atributos 
*********

* Crear y asignar en componente **app.component.ts**:

.. code-block:: Typescript
    :linenos:

    import { Component } from '@angular/core';

    @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.css']
    })
    export class AppComponent {
        // crear una variable en el componente:
        mensaje: string = "Mensaje desde el componente app";
    }

* Utilizar variable en plantilla **app.template.html**:

.. code-block::  
    :linenos:

    <h1>{{mensaje}}</h1>


Métodos
*******

Retornar datos de un método:

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
    selector: 'app-interpolation',
    templateUrl: './interpolation.component.html',
    styleUrls: ['./interpolation.component.css']
    })
    export class InterpolationComponent implements OnInit {
    // vamos a crear un objeto mixto sin interface:
    consola: any = {
        marca: 'Sony',
        modelo: 'PlayStation',
        lanzamiento: new Date(1995, 9, 29)
    }

    constructor() { }

    ngOnInit(): void {
    }

    // para averiguar la edad creamos un método:
    getEdad(): number {
        const edad = (new Date().getTime() - this.consola.lanzamiento.getTime()) / (365 * 24 * 60 * 60 * 1000);
        return Math.ceil(edad);
    }

    }

Uso en el template:

.. code-block::  
    :linenos:

    <div class="card">
        <p>Consola: {{consola.marca}} {{consola.modelo}}</p>
        <p>Edad: {{getEdad()}} años</p>
    </div>

Assets
******

* Tratamiento estático de assets en templates:

.. code-block::  
    :linenos:

    <div class="card">
        <img src="/assets/img/imagen-prueba.jpg">
    </div>

* Asignación de assets en componentes:

.. code-block:: Typescript
    :linenos:

    imagen: string = '/assets/img/prueba-imagen.jpg';


Atributos dinámicos
*******************

* En el controlador existe un atributo con una ruta, se carga la variable en el template:

.. code-block:: 
    :linenos:

    <img [src]="imagen">

.. note:: 
    Esto vale para cargar información en cualquier atributo de la etiqueta.


Eventos del DOM (event binding)
*******************************

Angular dispone de todos los métodos tácticos del DOM usados en HTML para dispara acciones:

* En el componente se crea un método:

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-saludar',
        templateUrl: './saludar.component.html',
        styleUrls: ['./saludar.component.css']
    })
    export class SaludarComponent implements OnInit {
        // se crea un atributo para el HTML:
        public saludo: string;

        constructor() {
            // Se inicializa el atributo con un mensaje o nada:
            this.saludo = "";
        }

        ngOnInit(): void {
        }

        // este método dispara el saludo:
        startSaludo(): void{
            this.saludo = "Hola amigo, ¿quién eres?";
        }

    }


* Este método ahora se puede disparar al hacer click en el botón:

.. code-block::  
    :linenos:

    <div class="card">
        <h1>Ejemplo de saludo</h1>
        <hr>
        <p>{{ saludo }}</p>
        <button (click)="startSaludo()">Saludar</button>
    </div>


Recuperar valores de plantilla (Two Way binding)
************************************************
Para recuperar valores de la plantilla como datos de un formulario se hace lo siguiente:

1. Se carga el modulo de formularios en **app.module.ts**:

.. code-block:: Typescript
    :linenos:

    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';

    import { AppComponent } from './app.component';
    import { MenuComponent } from './components/menu/menu.component';
    import { InterpolationComponent } from './components/interpolation/interpolation.component';
    import { PropertyBindingComponent } from './components/property-binding/property-binding.component';
    import { EventBindingComponent } from './components/event-binding/event-binding.component';
    import { SaludarComponent } from './components/saludar/saludar.component';
    import { TwowaybindingComponent } from './components/twowaybinding/twowaybinding.component';
    import { FormsModule } from '@angular/forms'; // se importan los forms.

    @NgModule({
    declarations: [
        AppComponent,
        MenuComponent,
        InterpolationComponent,
        PropertyBindingComponent,
        EventBindingComponent,
        SaludarComponent,
        TwowaybindingComponent
    ],
    imports: [
        BrowserModule,
        FormsModule // se carga en los imports el modulo de forms para todos los componentes de app
    ],
    providers: [],
    bootstrap: [AppComponent]
    })
    export class AppModule { }

2. Ahora pasamos al componente con el que se quiere trabajar:

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

        @Component({
        selector: 'app-twowaybinding',
        templateUrl: './twowaybinding.component.html',
        styleUrls: ['./twowaybinding.component.css']
        })
        export class TwowaybindingComponent implements OnInit {
        // crear objeto donde se va a guardar los datos.
        consola: any = {
            marca: null,
            modelo: null
        }

        constructor() { }

        ngOnInit(): void {
        }

    }


3. Y por último se prepara el template:

.. code-block::  
    :linenos:

    <div class="card">
        <h1>Datos consola</h1>
        <hr>
        <p>Consola: {{consola.marca}} {{consola.modelo}}</p>
        <!-- se le pasa los campos con la directiva ngModel: -->
        <input type="text" placeholder="marca" [(ngModel)]="consola.marca">
        <input type="text" placeholder="modelo" [(ngModel)]="consola.modelo">
    </div>

Ciclo de vida 
#############

El ciclo de vida va en el siguiente orden:

* Constructor
* ngOnChanges
* ngOnInit
* ngDoCheck
* ngAfterContentInit
* ngAfterContentChecked
* ngAfterViewInit
* ngAfterViewChecked
* ngOnDestroy

Constructor - Cargar métodos y datos que construyen la aplicación
*****************************************************************
La primera acción que se ejecuta en el componente es el constructor y es muy útil para 
cargar la información antes de disparar cualquier evento como NgOnInit():

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-event-binding',
        templateUrl: './event-binding.component.html',
        styleUrls: ['./event-binding.component.css']
    })
    export class EventBindingComponent implements OnInit {

        // se crea un elemento, si no se inicializa dará error el linter:
        public hora: string;

        constructor() {
            // establecemos la hora con el setHora:
            this.hora = this.setHora();
        }

        ngOnInit(): void {
        }

        // creamos un seteador para la hora:
        setHora(): string {
            // recuperamos hora, minutos y segundos actuales:
            const hh = ('0' + new Date().getHours()).slice(-2);
            const mm = ('0' + new Date().getHours()).slice(-2);
            const ss = ('0' + new Date().getHours()).slice(-2);
            // cargamos el tiempo en hora:
            return hh + ':' + mm + ':' + ss;
        }

    }


ngOnInit() - Cargar método cuando se inicialice el componente
*************************************************************

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-property-binding',
        templateUrl: './property-binding.component.html',
        styleUrls: ['./property-binding.component.css']
    })
    export class PropertyBindingComponent implements OnInit {

        imagen: string = '/assets/img/prueba-imagen.jpg';

        constructor() { }

        ngOnInit(): void {
            // lo cargamos en el DOM al inicializar el componente para que se ejecute:
            this.cambiarImagen();
        }

        // crear metodo que cambia imagen:
        cambiarImagen(): void {
            const logoRojo = '/assets/img/logo-rojo.jpg';
            const logoBlanco = '/assets/img/logo-blanco.jpg';
            setInterval(()=> {
            this.imagen === logoRojo ? this.imagen = logoBlanco : this.imagen = logoRojo;
            }, 1000);
        }

    }

ngAfterContentChecked() - Ejecutar después de que se refresque un componente 
****************************************************************************

Este evento se dispará cuando angular refresca un componente permitiendo ejecutar métodos adicionales en el proceso.

* caso de ejemplo con un marcador cuyos jugadores se deben ordenar por los que más han encanastado:

.. code-block:: typescript 
    :linenos:

    import { Component, Input, OnInit } from '@angular/core';

    @Component({
        selector: 'app-top-score',
        templateUrl: './top-score.component.html',
        styleUrls: ['./top-score.component.css']
    })
    export class TopScoreComponent implements OnInit {

        @Input() equipoLocal: any;
        @Input() equipoVisitante: any;

        jugadores: any = [];

        constructor() { }

        ngOnInit(): void {
            this.jugadores = [...this.equipoLocal.jugadores, ...this.equipoVisitante.jugadores];
        }

        // hook para dispararse cada vez que haya cambios en los valores:
        ngAfterContentChecked(){
            this.sortJugadores();
        }

        sortJugadores() {
            this.jugadores.sort( (a: any, b: any)=> {
            return (b.puntos - a.puntos);
            } );
        }
    }

Pipes
#####

El pipe permite formatear valores que vienen del componente. 

Pipes de texto 
**************
 
* Tenemos un atributo texto en el componente:

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-pipes-angular',
        templateUrl: './pipes-angular.component.html',
        styleUrls: ['./pipes-angular.component.css']
    })
    export class PipesAngularComponent implements OnInit {
        // se crean un atributo con datos:
        texto: string = 'La mejor consola es la Switch'

        constructor() { }

        ngOnInit(): void {
        }

    }

* En el template vamos a ver los pipes:

.. code-block::  
    :linenos:

    <div class="card">
        <h1>Pipes de texto</h1>
        <table border=1>
            <tr>
                <th>Nombre</th>
                <th>Valor sin pipe</th>
                <th>Valor con pipe</th>
                <th>Descripción</th>
            </tr>
            <tr>
                <td>Uppercase</td>
                <td>{{ texto }}</td>
                <td>{{ texto|uppercase }}</td>
                <td>Todas las letras a mayúsculas</td>
            </tr>
            <tr>
                <td>Lowercase</td>
                <td>{{ texto }}</td>
                <td>{{ texto|lowercase }}</td>
                <td>Todas las letras a minúsculas</td>
            </tr>
            <tr>
                <td>Titlecase</td>
                <td>{{ texto }}</td>
                <td>{{ texto|titlecase }}</td>
                <td>todas las primeras letras a mayúsculas</td>
            </tr>
        </table>
    </div>


Pipes de formato y fecha
************************

* Tenemos los siguientes atributos:

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-pipes-angular',
        templateUrl: './pipes-angular.component.html',
        styleUrls: ['./pipes-angular.component.css']
    })
    export class PipesAngularComponent implements OnInit {
        // se crea un atributo de tipo mixto:
        id: any = 11;
        // también creamos una fecha:
        fecha: Date = new Date();

        constructor() {
            // ahora se combina con una nomenclatura:
            this.id = '000' + this.id;
        }

        ngOnInit(): void {

        }

    }

* Y estos son los pypes:

.. code-block::  
    :linenos:

    <div class="card">
        <h1>Pipes de formato y fecha</h1>
        <table border=1>
            <tr>
                <th>Nombre</th>
                <th>Valor sin pipe</th>
                <th>Valor con pipe</th>
                <th>Descripción</th>
            </tr>
            <tr>
            <td>Slice</td>
            <td>{{ id }}</td>
            <td>{{ id|slice: -3 }}</td>
            <td>Corta un número de caracteres</td>
            </tr>
            <tr>
            <td>Date</td>
            <td>{{ fecha }}</td>
            <td>{{ fecha|date: 'dd/MM/yyyy hh:mm' }}</td>
            <td>Formatea una fecha, también disponible opciones: "long", "medium", "short"</td>
            </tr>
        </table>
    </div>


Pipes núméricos
***************

* Estos son los atributos a modificar:

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-pipes-angular',
        templateUrl: './pipes-angular.component.html',
        styleUrls: ['./pipes-angular.component.css']
    })
    export class PipesAngularComponent implements OnInit {
        // se crea un atributo numérico:
        importe: number = 1927.327823;

        constructor() {
        }

        ngOnInit(): void {

        }

    }

* Veamos los pipes numéricos:

.. code-block::  
    :linenos:

    <div class="card">
        <h1>Pipes Numéricos</h1>
        <table border=1>
            <tr>
                <th>Nombre</th>
                <th>Valor sin pipe</th>
                <th>Valor con pipe</th>
                <th>Descripción</th>
            </tr>
            <tr>
            <td>Decimal</td>
            <td>{{ importe }}</td>
            <td>{{ importe|number: "5.2-2" }}</td>
            <td>Establece la cantidad de números mínimos de enteros y los decimales</td>
            </tr>
            <tr>
            <td>Currency</td>
            <td>{{ importe }}</td>
            <td>{{ importe|currency: "€" }}</td>
            <td>Trabaja con divisas, por defecto $ pero se puede cambiar por otro</td>
            </tr>
        </table>
    </div>


Crear un pipe 
*************

* Para crear un Pipe se utiliza el comando: ``ng generate pipe nombrePipe``
* Generar un pipe en una carpeta: ``ng generate pipe pipes/nombrePipe``
* Editar el pipe:

.. code-block:: typescript 
    :linenos:

    import { Pipe, PipeTransform } from '@angular/core';

    @Pipe({
        name: 'nombrePipe'
    })

    export class NombrePipePipe implements PipeTransform {
        // el metodo transform recibe siempre el value y luego podemos definir el tipo de dato que retorna:
        transform(value: number, decimales: number, moneda?: string): number | string { // se puede poner el parametro opcional ?
            // vamos a hacer un redondeo:
            const factor = Math.pow(10,decimales);

            let valorRedondeado;
            if(value >= 0){
            valorRedondeado = Math.round(value * factor) / factor;
            }else{
            valorRedondeado = Math.round(-value * factor) / factor;
            }
            // formatear el valor numérico similar al nuestro:
            let valorFormateado = new Intl.NumberFormat('de-DE', {minimumFractionDigits: decimales}).format(valorRedondeado);

            return moneda ? valorFormateado + ' ' + moneda : valorFormateado;
        }

    }


Ahora esto se utiliza en un número decimal del template ``{{ number|nombrePipe:2 }}`` o con una moneda ``{{ number|nombrePipe:2:'€' }}`` y lo redondeará a un entero.

.. note::
    Los args son opcionales, se puede utilizar el método transform solo con el parametro value.


Directivas angular
##################

Las directivas sirven para controlar el comportamiento de la información desde el template. 

.. attention::
    cuando se utilizan números en las cadenas estos se escriben ``*ngSwitchCase="20"``, si son cadenas ``*ngSwitchCase="'hola'"`` y si son atributos ``*ngSwitchCase="atributo"``  

Directivas de control
*********************

Condicional if 
++++++++++++++

* Creamos un atributo edad en el componente:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-directiva-if',
        templateUrl: './directiva-if.component.html',
        styleUrls: ['./directiva-if.component.css']
    })
    export class DirectivaIfComponent implements OnInit {
        // ponemos una edad:
        public edad: number;

        constructor() {
            // inicializamos la edad:
            this.edad = 0;
        }

        ngOnInit(): void {
        }

    }

* En el template veremos el ngIf:

.. code-block::  
    :linenos: 

    <div class="row">
        <h1>ngIf</h1>
        <input type="number" [(ngModel)]="edad">
        <p>Tienes {{ edad }} años.</p>
        <!-- Establecer if: -->
        <p *ngIf="edad >=18; else menor">Eres mayor de edad</p>
        <!-- para el else usamos un ng-tempalte: -->
        <ng-template #menor>
            <p>Eres menor de edad</p>
        </ng-template>
    </div>

.. attention::
    Hay que añadir el módulo FormsModule en app.module.ts


Condicional Switch
++++++++++++++++++

* Tenemos una edad en el componente igual al ejemplo anterior.
* En el template veremos ngSwitch:

.. code-block::  
    :linenos:

    <div class="row">
        <h1>ngIf</h1>
        <input type="number" [(ngModel)]="edad">
        <p>Tienes {{ edad }} años.</p>
        <!-- Establecer switch: -->
        <div [ngSwitch]="edad">
            <p *ngSwitchCase="18">Ya eres mayor de edad!</p>
            <p *ngSwitchCase="65">Ya eres un anciano!</p>
        </div>
    </div>


Condicional For
+++++++++++++++

* Creamos una lista de elementos en el componente:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-directiva-for',
        templateUrl: './directiva-for.component.html',
        styleUrls: ['./directiva-for.component.css']
    })
    export class DirectivaForComponent implements OnInit {
        // crear colección:
        consolas: Array<any>;

        constructor() {
            // harcodear datos:
            this.consolas = [
            {marca: 'Sony', modelo: 'Playstation', lanzamiento: 1995},
            {marca: 'Sega', modelo: 'Dreamcast', lanzamiento: 1998},
            {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
            {marca: 'Nintendo', modelo: 'Gamecube', lanzamiento: 2002},
            {marca: 'Sony', modelo: 'Playstation 2', lanzamiento: 2001}
            ]
        }

        ngOnInit(): void {
        }

    }

* Cargar listado en el template:

.. code-block: html 
    :linenos:

    <div class="card">
        <h1>Listado de consolas con *ngFor</h1>

        <table border=1>
            <tr>
                <th>ID</th>
                <th>Consola</th>
                <th>Marca</th>
                <th>Lanzamiento</th>
            </tr>
            <!-- Se recorre el for, opcionalmente podemos cargar el índice tras el ; -->
            <tr *ngFor="let consola of consolas; let i = index">
                <td>{{ i + 1 }}</td>
                <td>{{ consola.modelo }}</td>
                <td>{{ consola.marca }}</td>
                <td>{{ consola.lanzamiento }}</td>
            </tr>
        </table>
    </div>

.. note::
    Una cosa interesante es que cuando se producen cambios en la información del componente esto se actualizan en la vista automáticamente sin hacer nada.

Directivas de atributos 
***********************

Las directivas de atributos al igual que los atributos dinámicos [src], [value], etc... permiten asignar un valor que proviene del componente como el
nombre de una clase o el valor de un estilo css.


Implementar clase ngClass
+++++++++++++++++++++++++

* Tenemos el listado de consolas en el componente:

.. code-block:: typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-clases',
        templateUrl: './clases.component.html',
        styleUrls: ['./clases.component.css']
    })
    export class ClasesComponent implements OnInit {

        consolas: Array<any>;

        constructor() {
            // harcodear datos:
            this.consolas = [
            {marca: 'Sony', modelo: 'Playstation', lanzamiento: 1995},
            {marca: 'Sega', modelo: 'Dreamcast', lanzamiento: 1998},
            {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
            {marca: 'Nintendo', modelo: 'Gamecube', lanzamiento: 2002},
            {marca: 'Sony', modelo: 'Playstation 2', lanzamiento: 2001}
            ]
        }

        ngOnInit(): void {
        }

    }

* En el css se crean unas clases con los nombres de las marcas:

.. code-block:: css 
    :linenos:

    .Sony{
        color: gray;
    }

    .Sega{
        color: blue;
    }

    .Nintendo{
        color: red;
    }

* Ahora en el template se implementan las clases según su marca:

.. code-block::  
    :linenos:

    <div class="card">

    <table border=1>
        <tr>
            <th>ID</th>
            <th>Consola</th>
            <th>Marca</th>
            <th>Lanzamiento</th>
        </tr>
        <tr *ngFor="let consola of consolas; let i = index">
            <!-- ngClass recibe un atributo que compara con el nombre de una clase css -->
            <td [ngClass]="consola.marca">{{ i + 1 }}</td>
            <td [ngClass]="consola.marca">{{ consola.modelo }}</td>
            <td [ngClass]="consola.marca">{{ consola.marca }}</td>
            <td [ngClass]="consola.marca">{{ consola.lanzamiento }}</td>
        </tr>
    </table>
    </div>



Implementar estilo ngStyle
++++++++++++++++++++++++++

* En primer lugar añadimos un atributo edad y un método que defina los colores:

.. code-block:: typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-clases',
        templateUrl: './clases.component.html',
        styleUrls: ['./clases.component.css']
    })
    export class ClasesComponent implements OnInit {

        edad: number;

        constructor() {
            this.edad = 0;
        }

        ngOnInit(): void {
        }

        // vamos a crear un método para recuperar el color:
        getColor(){
            if(this.edad < 18){
            return "red";
            }else if(this.edad >= 18){
            return "green";
            }else{
            return "blue";
            }
        }

    }

* En el template se implementa la directiva:

.. code-block:: 
    :linenos:

    <div class="row">
        <input type="number" [(ngModel)]="edad">
        <p>Tienes {{ edad }} años.</p>
        <!-- Establecer switch: -->
        <p *ngIf="edad >=18; else menor" [ngStyle]="{'color': getColor()}">Eres mayor de edad</p>
        <!-- para el else usamos un ng-tempalte: -->
        <ng-template #menor>
            <p [ngStyle]="{'color': getColor()}">Eres menor de edad</p>
        </ng-template>
    </div>


Jerarquía de componentes 
########################

Enviar valores de padre a hijo 
******************************

* El componente padre tiene un valor:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-padre',
        templateUrl: './padre.component.html',
        styleUrls: ['./padre.component.css']
    })
    export class PadreComponent implements OnInit {
        // tenemos un valor en el padre:
        numeroPadre : number;

        constructor() {
            // al que se le asigna un número:
            this.numeroPadre = 30;

        }

        ngOnInit(): void {
        }

    }

* El padre envía a través del selector del hijo el atributo numeroPadre:

.. code-blocK::  
    :linenos:

    <div class="card">
        <h2>Componente padre</h2>
        <p>Valor número padre: {{ numeroPadre }}</p>
        <app-hijo [numeroHijo]="numeroPadre"></app-hijo>
    </div>

* El hijo se prepara en el componente para recibir valores del padre:

.. code-block:: typescript 
    :linenos:

    // se importa input:
    import { Component, OnInit, Input } from '@angular/core';

    @Component({
        selector: 'app-hijo',
        templateUrl: './hijo.component.html',
        styleUrls: ['./hijo.component.css']
    })
    export class HijoComponent implements OnInit {
        // con el decorador Input se prepara el atributo para recibir los datos:
        @Input() numeroHijo : number = 0;

        constructor() { }

        ngOnInit(): void {
        }

    }

* Ahora se puede utilizar el atributo numeroHijo con los datos del padre:

.. code-block::  
    :linenos:

    <div class="card">
        <h3>Componente hijo</h3>
        <p>Valor número hijo: {{ numeroHijo }}</p>
    </div>


Enviar valores de hijo a padre 
******************************

* El procedimiento es similar, esta vez comenzamos por el componente hijo:

.. code-block:: typescript 
    :linenos:

    // se importa output y también el emisor de eventos:
    import { Component, OnInit, Output, EventEmitter } from '@angular/core';

    @Component({
        selector: 'app-hijo',
        templateUrl: './hijo.component.html',
        styleUrls: ['./hijo.component.css']
    })
    export class HijoComponent implements OnInit {
        // con el decorador Output se crea un nuevo objeto de tipo emisor:
        @Output() valor : EventEmitter<any> = new EventEmitter();

        constructor() { }

        ngOnInit(): void {
        }

        // preparamos un método para disparar el evento:
        handleChangeValor(){
            this.valor.emit({numeroHijo: 50})
        }

    }

* Añadimos un botón en el hijo que ejecutará el método emisor:

.. code-block:: 
    :linenos:

    <div class="card">
        <h3>Componente hijo</h3>
        <button (click)="handleChangeValor()">Cargar valor en el padre</button>
    </div>

* El padre deberá tener un método para recibir el evento emitido y actualizar el atributo numérico:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-padre',
        templateUrl: './padre.component.html',
        styleUrls: ['./padre.component.css']
    })
    export class PadreComponent implements OnInit {
        numeroPadre : number;

        constructor() {
            this.numeroPadre = 0;

        }

        ngOnInit(): void {
        }

        // recibimos el valor y lo asignamos al numeroPadre:
        getValor($event: any): void{
            this.numeroPadre = $event.numeroHijo;
        }

    }

* La plantilla solo tendrá que mostrar el número por defecto que cambiará al pulsar el botón:

.. code-block::  
    :linenos:

    <div class="card">
        <h2>Componente padre</h2>
        <p>Valor recibido: {{ numeroPadre }}</p>
        <!-- Ahora se recibe el valor en un método del padre que recibirá el evento: -->
        <app-hijo (valor)="getValor($event)"></app-hijo>
    </div>


Servicios en Angular 
####################

* Crear un servicio: ``ng generate service nombreServicio``
* Crear un servicio en un directorio: ``ng generate service services/nombreServicio``:

.. code-block:: Typescript
    :linenos:

    import { Injectable } from '@angular/core';

    @Injectable({
        providedIn: 'root' // esto indica que el servicio estará disponible en toda la aplicación
    })
    export class ConsolasService {
        // se crean los atributos como privados:
        private consolas: any = [
            {marca: 'Sony', modelo: 'Playstation', lanzamiento: 1995},
            {marca: 'Sega', modelo: 'Dreamcast', lanzamiento: 1998},
            {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
            {marca: 'Nintendo', modelo: 'Gamecube', lanzamiento: 2002},
            {marca: 'Sony', modelo: 'Playstation 2', lanzamiento: 2001}
        ]

        constructor() { }

        // se generan los métodos para obtener el listado:
        getConsolas(): any {
            return this.consolas;
        }
    }

* Implementamos el servicio en un componente:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';
    // se importa el servicio:
    import { ConsolasService } from 'src/app/services/consolas.service';

    @Component({
        selector: 'app-directiva-for',
        templateUrl: './directiva-for.component.html',
        styleUrls: ['./directiva-for.component.css']
    })
    export class DirectivaForComponent implements OnInit {
        // crear colección:
        consolas: Array<any> = [];

        // se instancia por parámetros el servicio:
        constructor(private consolasService: ConsolasService) {

        }

        ngOnInit(): void {
            // cuando haya cargado la página y obtenido los clientes se carga en el Init:
            this.consolas = this.consolasService.getConsolas();
        }

    }

* Ya se puede usar el servicio en el template:

.. code-block::  
    :linenos:

    <div class="card">
        <h1>Listado de consolas con *ngFor</h1>

        <table border=1>
            <tr>
            <th>ID</th>
            <th>Consola</th>
            <th>Marca</th>
            <th>Lanzamiento</th>
            </tr>
            <tr *ngFor="let consola of consolas; let i = index">
            <td>{{ i + 1 }}</td>
            <td>{{ consola.modelo }}</td>
            <td>{{ consola.marca }}</td>
            <td>{{ consola.lanzamiento }}</td>
            </tr>
        </table>
    </div>


Cargar datos en servicio
************************

Para enviar información al servicio hacemos lo siguiente:

* Ahora se modifica el servicio para añadir un set:

.. code-block:: typescript 
    :linenos:

    import { Injectable } from '@angular/core';

    @Injectable({
        providedIn: 'root'
    })
    export class ConsolasService {
        private consolas: any = [
            {marca: 'Sony', modelo: 'Playstation', lanzamiento: 1995},
            {marca: 'Sega', modelo: 'Dreamcast', lanzamiento: 1998},
            {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
            {marca: 'Nintendo', modelo: 'Gamecube', lanzamiento: 2002},
            {marca: 'Sony', modelo: 'Playstation 2', lanzamiento: 2001}
        ]

        constructor() { }

        getConsolas(): any {
            return this.consolas;
        }

        // crear un set que añadirá el nuevo elemento en la lista:
        setConsola(consola: any): void {
            this.consolas.push(consola);
        }
    }

* Crear un componente por ejemplo **crearConsola** y editar su componente:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';
    // se importa el servicio:
    import { ConsolasService } from 'src/app/services/consolas.service';

    @Component({
        selector: 'app-crear-consola',
        templateUrl: './crear-consola.component.html',
        styleUrls: ['./crear-consola.component.css']
    })
    export class CrearConsolaComponent implements OnInit {
        // se prepara el objeto para añadir una consola:
        consola: any = {
            marca: '',
            modelo: '',
            lanzamiento: ''
        }
        // se carga el servicio en el constructor:
        constructor(private consolasService: ConsolasService) { }

        ngOnInit(): void {
        }

        // preparamos un método para añadir consola:
        crearConsola(): void{
            this.consolasService.setConsola(this.consola);
        }

    }


* En su template tendrá un formulario:

.. code-blocK::  
    :linenos:

    <div class="card">
        <label>Marca</label>
        <input type="text" name="marca" [(ngModel)]="consola.marca">
        <label>Modelo</label>
        <input type="text" name="modelo" [(ngModel)]="consola.modelo">
        <label>Lanzamiento</label>
        <input type="number" name="lanzamiento" [(ngModel)]="consola.lanzamiento">
        <button (click)="crearConsola()">Añadir</button>
    </div>

.. attention::
    Recuerda que hay que añadir FormsModule en el módulo principal app.


Interfaces Angular 
##################

* Crear interface en angular: ``ng generate interface nombreInterface``
* Crear en una carpeta específica: ``ng generate interface interfaces/nombreInterface``

.. code-block:: typescript  
    :linenos:

    export interface Consola {
        marca: string,
        modelo: string,
        lanzamiento: number
    }

Ahora para establecerlo como un tipo de propiedad lo asignamos al atributo:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';
    // se importa la interfaz consolas:
    import { Consolas } from 'src/app/interfaces/consolas';
    import { ConsolasService } from 'src/app/services/consolas.service';

    @Component({
        selector: 'app-crear-consola',
        templateUrl: './crear-consola.component.html',
        styleUrls: ['./crear-consola.component.css']
    })
    export class CrearConsolaComponent implements OnInit {
        // se prepara el objeto para añadir una consola:
        consola: Consolas = {
            marca: '',
            modelo: '',
            lanzamiento: 0
        }
        constructor(private consolasService: ConsolasService) { }

        ngOnInit(): void {
        }

        crearConsola(): void{
            this.consolasService.setConsola(this.consola);
        }

    }

Esta interfaz se puede aplicar en donde se necesite ya sea controladores o servicios.

.. note::
    Si tenemos que definir un listado de objetos podemos declararlo usando el nombre de la intefaz: ``consolas: Array<NombreInterface> = [];``


Rutas en angular
################

Si hemos añadido **angular routing** para crear nuestro proyecto podemos usar las rutas de angular de forma sencilla.


* Se crean dos componentes nuevo para páginas: ``ng generate component pages/index`` y ``ng generate component pages/about``
* Al iniciar le proyecto se crea un archivo en **apps** llamado **app-routing.module.ts** que vamos a editar:

.. code-block:: typescript 
    :linenos:

    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    // importamos los componentes:
    import { AboutComponent } from './pages/about/about.component';
    import { IndexComponent } from './pages/index/index.component';

    // Aquí se van añadiendo las rutas:
    const routes: Routes = [
        {path: '', component: IndexComponent}, // añadimos la ruta raiz
        {path: 'about', component: AboutComponent} // y las rutas que tengamos según componentes
    ];

    @NgModule({
        imports: [RouterModule.forRoot(routes)],
        exports: [RouterModule]
    })
    export class AppRoutingModule { }

Ahora se añade el enrutador al template de **app.component.html**:

.. code-block::  
    :linenos:

    <!-- Aquí añadimos la ruta: -->
    <router-outlet></router-outlet>

Enlaces de rutas
****************

Para crear enlaces en las rutas hacemos lo siguiente en un template como **app.component.html**:

.. code-block::  
    :linenos:

    <div class="navbar">
        <h2>Rutas</h2>
        <!-- Para el enrutamiento se usa routerLink y para indicar que clase css usar cuando esta activo routerLinkActive -->
        <button routerLink="/" routerLinkActive="seleccionado" [routerLinkActiveOptions]="{exact: true}">Inicio</button><!-- para que la raiz no se quede marcada hay que pasar este tercer parámetro -->
        <button routerLink="about" routerLinkActive="seleccionado">About</button>
    </div>

    <router-outlet></router-outlet>


.. note::
    Lo ideal es crear un nuevo componente para un navbar


Rutas no existente
******************

Para solucionar las rutas inexistentes se crea un componente 404: ``ng generate component pages/error``
* Se añade al enrutador:

.. code-block:: typescript 
    :linenos:

    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { AboutComponent } from './pages/about/about.component';
    import { ErrorComponent } from './pages/error/error.component';
    // se importa el componente:
    import { IndexComponent } from './pages/index/index.component';

    const routes: Routes = [
        {path: '', component: IndexComponent},
        {path: 'about', component: AboutComponent},
        {path: '**', component:ErrorComponent} // va añadido siempre al final esta ruta
    ];

    @NgModule({
        imports: [RouterModule.forRoot(routes)],
        exports: [RouterModule]
    })
    export class AppRoutingModule { }

Ahora quedaría retocar la plantilla de la página para que muestre un error 404 personalizado.


Formularios Reactivos 
#####################

Vamos a trabajar con **ReactiveFormsModule** para implementar validaciones más potentes y otras características.

* Lo primero será cargar la librería **ReactiveFormsModule** en **app.module.ts**:

.. code-block:: typescript 
    :linenos:

    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';

    import { AppRoutingModule } from './app-routing.module';
    import { AppComponent } from './app.component';
    import { AboutComponent } from './pages/about/about.component';
    import { IndexComponent } from './pages/index/index.component';
    import { ErrorComponent } from './pages/error/error.component';
    import { CrearConsolaComponent } from './componets/crear-consola/crear-consola.component';
    // se importa la librería ReactiveFormsModule
    import { ReactiveFormsModule } from '@angular/forms';

    @NgModule({
        declarations: [
            AppComponent,
            AboutComponent,
            IndexComponent,
            ErrorComponent,
            CrearConsolaComponent
        ],
        imports: [
            BrowserModule,
            AppRoutingModule,
            ReactiveFormsModule // y se declara para usar en el modulo app
        ],
        providers: [],
        bootstrap: [AppComponent]
    })
    export class AppModule { }

* Ahora se trabaja el componente:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';
    // se importa formgroup, formcontrol y validators:
    import { FormControl, FormGroup, Validators } from '@angular/forms';

    @Component({
        selector: 'app-crear-consola',
        templateUrl: './crear-consola.component.html',
        styleUrls: ['./crear-consola.component.css']
    })
    export class CrearConsolaComponent implements OnInit {
        // creamos el atributo que manejara el form con el tipo FormGroup:
        public consolaForm: FormGroup;

        constructor() {
            // se implementa el formulario con sus campos:
            this.consolaForm = new FormGroup({ // también se aplicarán los validadores:
            marca: new FormControl('', [Validators.required]),
            modelo: new FormControl('', [Validators.required]),
            lanzamiento: new FormControl(0, [Validators.required])
            });
        }

        ngOnInit(): void {

        }

        enviarConsola(): void{
            console.log('se dispara');
            console.log(this.consolaForm.value);
        }

    }

* Ahora pasamos al template a crear el formulario:

.. code-block::  
    :linenos:

    <div class="card">
    <!-- se carga la directiva formgroup con el atributo a una función que guardará la información:-->
    <form [formGroup]="consolaForm" (ngSubmit)="enviarConsola()">
        <label>Marca</label>
        <input type="text" formControlName="marca">
        <div *ngIf="consolaForm.controls['marca'].invalid">El campo es requerido</div>
        <label>Modelo</label>
        <input type="text" formControlName="modelo">
        <div *ngIf="consolaForm.controls['modelo'].invalid">El campo es requerido</div>
        <label>Lanzamiento</label>
        <input type="number" formControlName="lanzamiento">
        <div *ngIf="consolaForm.controls['lanzamiento'].invalid">El campo es requerido</div>
    <!-- Validar todo el formulario antes de poder activar el botón: -->
    <button [disabled]="consolaForm.invalid" type="submit">Enviar</button>
    </form>
    <!-- Para depurar el formulario cargamos con pre los elementos: -->
    <pre>{{ consolaForm.value | json }}</pre>
    </div>



Tipos de validaciones comunes:

- pristine: limpio, nada escrito.
- dirty: se ha escrito.
- touched: ha sido seleccionado.
- untouched: no esta seleccionado.
- valid: es válido.
- invalid: no es válido.


Peticiones HTTP
###############

Partimos de un proyecto nuevo creado con ``ng new consolasfront``

Preparativos
************
Lo primero será cargar el modulo **HttpClientsModule** en los imports de **app.module.ts**:

.. code-block:: typescript 
    :linenos:

    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';

    import { AppComponent } from './app.component';
    import { FormsModule } from '@angular/forms';
    import { DirectivaIfComponent } from './components/directiva-if/directiva-if.component';
    import { DirectivaForComponent } from './components/directiva-for/directiva-for.component';
    import { CrearConsolaComponent } from './components/crear-consola/crear-consola.component'; // se importan los forms.
    // se carga la librería HttpClientModule:
    import { HttpClientModule } from '@angular/common/http';

    @NgModule({
    declarations: [
        AppComponent,
        DirectivaForComponent,
        CrearConsolaComponent,
    ],
    imports: [
        BrowserModule,
        HttpClientModule, // cargamos el httpclientmodule
        FormsModule
    ],
    providers: [],
    bootstrap: [AppComponent]
    })
    export class AppModule { }

Crear servicio Http
*******************

Se crea un nuevo servicio en angular con ``ng generate service services/consolas`` y se edita:

.. code-block:: typescript 
    :linenos:

    // se importa la librería http:
    import { HttpClient } from '@angular/common/http';
    import { Injectable } from '@angular/core';
    // importamos map de rxjs:
    import { map } from 'rxjs/operators';

    @Injectable({
    providedIn: 'root'
    })
    export class ConsolasService {
        // definimos la ruta base que será la del servidor API:
        base: string = 'http://localhost:3500';

        // se carga la librería http en el constructor:
        constructor(private http: HttpClient) { }

        // utilizamos el getter para hacer la petición get:
        getConsolas(): any {
            // esto retorna una petición con get y una respuesta con pipe:
            return this.http.get(this.base)
                            .pipe( // se mapea la respuesta con rxjs:
                            map((data: any)=> {
                                return data;
                            })
                            );
        }

        // recuperar un solo valor del mismo modo que antes pero con un endpoint recibido por parametros:
        getConsola(marca: any): any {
            return this.http.get(`${this.base}/consola/${marca}`)
                            .pipe(
                            map((data: any)=> {
                                return data;
                            })
                            );
        }

        // Hacemos un método POST:
        postConsola(consola: any): any {
            return this.http.post(`${this.base}/consola/crear/`, consola)
                            .pipe(
                            map((data: any) => {
                                return data;
                            })
                            );
        }

        // Hacemos un método PUT:
        putConsola(consola: any, modelo: string): any {
            return this.http.put(`${this.base}/consola/actualizar/${modelo}`, consola)
                            .pipe(
                            map((data: any) => {
                                return data;
                            })
                            );
        }

        // hacemos el metodo delete:
        deleteConsola(modelo: string){
            return this.http.delete(`${this.base}/consola/eliminar/${modelo}`)
                            .pipe(
                            map((data: any) => {
                                return data;
                            })
                            );
        }
    }

* Creamos un nuevo componente ``ng generate components pages/index`` para sacar un listado de consolas.
* Se crea un nuevo componente ``ng generate component pages/crearConsola``
* Se crea un componente ``ng generate component pages/actualizar``
* Añadimos las rutas de los nuevos componentes:

.. code-block:: typescript 
    :linenos:

    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { ActualizarComponent } from './pages/actualizar/actualizar.component';
    import { CrearConsolaComponent } from './pages/crear-consola/crear-consola.component';
    import { IndexComponent } from './pages/index/index.component';

    const routes: Routes = [
    {path: '', component: IndexComponent},
    {path: 'crear', component: CrearConsolaComponent},
    {path: 'actualizar/:modelo', component: ActualizarComponent}
    ];

    @NgModule({
    imports: [RouterModule.forRoot(routes)],
    exports: [RouterModule]
    })
    export class AppRoutingModule { }


Peticiones GET
**************

* Se edita el componente:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';
    import { Consolas } from 'src/app/interfaces/consolas';
    import { ConsolasService } from 'src/app/services/consolas.service';

    @Component({
        selector: 'app-index',
        templateUrl: './index.component.html',
        styleUrls: ['./index.component.css']
    })
    export class IndexComponent implements OnInit {

        // se crea una colección de objetos de tipo consolas:
        consolas: Array<Consolas> = [];
        // se carga el servicio en el constructor:
        constructor(private consolasService: ConsolasService) {

        }

        ngOnInit(): void {
            // hay que subscribir los datos a la hora de obtenerlos con rxjs:
            this.consolasService.getConsolas() // o se usa any o se valida que es de tipo colección de consolas:
                                .subscribe((res:Array<Consolas>)=>{
                                this.consolas = res;
                                }, (err: any) =>{ // si falla se ejecuta esta linea
                                console.log(err);
                                });
        }

    }

* Se edita el template:

.. code-block::  
    :linenos:

    <h2>Listado de consolas</h2>
    <table border=1>
    <tr>
        <th>Marca</th>
        <th>Modelo</th>
        <th>Lanzamiento</th>
    </tr>
    <tr *ngFor="let consola of consolas">
        <td>{{ consola.marca }}</td>
        <td>{{ consola.modelo }}</td>
        <td>{{ consola.lanzamiento }}</td>
    </tr>
    </table>

Peticiones POST
***************

* se edita el componente:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';
    // cargamos el router para una redirección:
    import { Router } from '@angular/router';
    // se importa la interfaz consolas:
    import { Consolas } from 'src/app/interfaces/consolas';
    import { ConsolasService } from 'src/app/services/consolas.service';

    @Component({
        selector: 'app-crear-consola',
        templateUrl: './crear-consola.component.html',
        styleUrls: ['./crear-consola.component.css']
    })
    export class CrearConsolaComponent implements OnInit {
        // se prepara el objeto para añadir una consola:
        consola: Consolas = {
            marca: '',
            modelo: '',
            lanzamiento: 0
        }
        // se trae el servicio de consolas y el router para uan redirección:
        constructor(private consolasService: ConsolasService, private route: Router) { }

        ngOnInit(): void {
        }

        crearConsola(): void{
            this.consolasService.postConsola(this.consola)
                                .subscribe((res: any) => {
                                console.log(res); // esto se quita en producción
                                // haremos una redirección al listado:
                                this.route.navigate(['/']);
                                }, (err: any) => {
                                console.log(err);
                                });
        }

    }

* Y ahora se edita el template:

.. code-block::
    :linenos:

    <h2>Crear nueva consola</h2>

    <div>
        <label>Marca</label>
        <input type="text" name="marca" [(ngModel)]="consola.marca">
        <label>Modelo</label>
        <input type="text" name="modelo" [(ngModel)]="consola.modelo">
        <label>Lanzamiento</label>
        <input type="number" name="lanzamiento" [(ngModel)]="consola.lanzamiento">
        <button (click)="crearConsola()">Añadir</button>
    </div>

.. note::
    Se debería crear un comnponente solo para el formulario y reutilizar en la vista editar pero esto es un ejemplo básico.



Peticiones PUT 
**************

* En el template del listado se añade el botón con un parámetro para buscar el elemento:

.. code-block::  
    :linenos:

    <h2>Listado de consolas</h2>
    <table border=1>
    <tr>
        <th>Marca</th>
        <th>Modelo</th>
        <th>Lanzamiento</th>
    </tr>
    <tr *ngFor="let consola of consolas">
        <td>{{ consola.marca }}</td>
        <td>{{ consola.modelo }}</td>
        <td>{{ consola.lanzamiento }}</td>
        <td>
        <button routerLink="actualizar/{{ consola.modelo }}">editar</button>
        </td>
    </tr>
    </table>

* Se edita el componente actualizar:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';
    import { ActivatedRoute, Router } from '@angular/router';
    // cargar el interface:
    import { Consolas } from 'src/app/interfaces/consolas';
    // importar el servicio:
    import { ConsolasService } from 'src/app/services/consolas.service';

    @Component({
        selector: 'app-actualizar',
        templateUrl: './actualizar.component.html',
        styleUrls: ['./actualizar.component.css']
    })
    export class ActualizarComponent implements OnInit {
        // crear un atributo donde guardar la marca:
        modelo: string;
        // se prepara el objeto para añadir una consola:
        consola: Consolas = {
            marca: '',
            modelo: '',
            lanzamiento: 0
        }

        // cargar el modulo de ruta activa para coger el parámetro get y el servicio:
        constructor(private route: ActivatedRoute, private router: Router, private consolasService: ConsolasService) {
            // asignar el valor de modelo recibido por parámetros:
            this.modelo = this.route.snapshot.params['modelo'];
            // nos subscribimos al servicio:
            this.consolasService.getConsola(this.modelo)
                                .subscribe((res: any) =>{
                                console.log(res);
                                }, (err: any) => {
                                console.log(err);
                                });
        }

        ngOnInit(): void {
        }

        editarConsola(): void {
            this.consolasService.putConsola(this.consola, this.modelo)
                                .subscribe((res: any) =>{
                                console.log(res);
                                // redireccionamos:
                                this.router.navigate(['/']);
                                }, (err: any) => {
                                console.log(err);
                                });
        }

    }

* Crear el template:

.. code-block::  
    :linenos:

    <h2>Editar {{modelo}}</h2>

    <div>
        <label>Marca</label>
        <input type="text" name="marca" [(ngModel)]="consola.marca">
        <label>Modelo</label>
        <input type="text" name="modelo" [(ngModel)]="consola.modelo">
        <label>Lanzamiento</label>
        <input type="number" name="lanzamiento" [(ngModel)]="consola.lanzamiento">
        <button (click)="editarConsola()">Actualizar</button>
    </div>


Peticiones DELETE 
*****************

* Empezamos en el template del listado:

.. code-block::  
    :linenos:

    <h2>Listado de consolas</h2>
    <table border=1>
    <tr>
        <th>Marca</th>
        <th>Modelo</th>
        <th>Lanzamiento</th>
    </tr>
    <tr *ngFor="let consola of consolas">
        <td>{{ consola.marca }}</td>
        <td>{{ consola.modelo }}</td>
        <td>{{ consola.lanzamiento }}</td>
        <td>
        <button routerLink="actualizar/{{ consola.modelo }}">editar</button>
        </td>
        <td>
        <!-- añadir el nuevo boton de eliminar -->
        <button (click)="eliminarConsola(consola.modelo)">Eliminar</button>
        </td>
    </tr>
    </table>

* Creamos el metodo y hacemos la petición delete:

.. code-block:: typescript 
    :linenos:

    import { Component, OnInit } from '@angular/core';
    import { Consolas } from 'src/app/interfaces/consolas';
    import { ConsolasService } from 'src/app/services/consolas.service';

    @Component({
        selector: 'app-index',
        templateUrl: './index.component.html',
        styleUrls: ['./index.component.css']
    })
    export class IndexComponent implements OnInit {

        consolas: Array<Consolas> = [];
        constructor(private consolasService: ConsolasService) {

        }

        ngOnInit(): void {
            this.cargarClientes();
        }

        eliminarConsola(modelo: string){
            this.consolasService.deleteConsola(modelo)
                                .subscribe((res:any)=>{
                                // refrescar pantalla:
                                this.cargarClientes();
                                }, (err: any)=>{
                                console.log(err);
                                });
        }

        // recuperamos la petición del listado y la añadimos a esta función para reutilizar de manera limpia:
        cargarClientes(){
            this.consolasService.getConsolas()
            .subscribe((res:Array<Consolas>)=>{
            this.consolas = res;
            }, (err: any) =>{
            console.log(err);
            });
        }

    }

Angular Material 
################

Angular material es una librería de estilos muy útil en ángular. 

Preparación
***********

* Instalar angular material: ``ng add @angular/material``
* Crear módulo para separar la lógica de angular material: ``ng generate module material``
* Cargar modulo **material.module.ts** en **app.material.ts**:

.. code-block:: typescript 
    :linenos:

    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';

    import { AppRoutingModule } from './app-routing.module';
    import { AppComponent } from './app.component';
    import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
    // importamos el módulo:
    import { MaterialModule } from './material/material.module';

    @NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        BrowserModule,
        AppRoutingModule,
        BrowserAnimationsModule,
        MaterialModule
    ],
    providers: [],
    bootstrap: [AppComponent]
    })
    export class AppModule { }


Uso de componentes 
******************

* Editar modulo **material.module.ts** para cargar componentes de angular material y exportarlos:

.. code-block:: typescript 
    :linenos:

    import { NgModule } from '@angular/core';
    // cargamos el modulo del elemento a usar de angular material:
    import {MatToolbarModule} from '@angular/material/toolbar';


    @NgModule({
    declarations: [],
    imports: [ // se importa y se exporta:
        MatToolbarModule
    ],
    exports: [
        MatToolbarModule
    ]
    })
    export class MaterialModule { }

* En cualquier template se puede cargar el componente añadido, en este caso **MatToolbarModule**:

.. code-block::  
    :linenos:

    <mat-toolbar color="primary">
        <span>Taller angular</span>
    </mat-toolbar>


.. note::
    En la página https://material.angular.io/components/categories se pueden ver los distintos componentes que pueden añadirse.

    