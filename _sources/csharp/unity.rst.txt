Unity 
=====
 
.. image:: /logos/logo-unity.png
    :scale: 80%
    :alt: Logo Unity
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M
 

Funciones y otros elementos de Unity

.. contents:: Índice
 

Estructura base
###############

.. code-block:: C#
    :linenos:

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine; // unity utiliza su propia libería en cada script

    public class NewBehaviourScript : MonoBehaviour // también heredan todos de una clase padre
    {
        // Este método es llamado antes de arrancar el juego
        void Start()
        {
            
        }

        // Este método se actualiza con cada frame del juego
        void Update()
        {
            
        }
    }


objetos
#######

Assets
######
Los assets son archivos que contienen imágenes, scripts y otro tipo de comportamientos en Unity:
- C# Script: Archivo de código que se puede asignar a uno o varios objetos.
- Material: aspecto que se le puede asignar a uno o varios objetos.
- Physc Material: comportamiento físico que se puede agregar a uno o varios elementos.

En la carpeta assets creamos la siguiente estructura de carpetas:
- Materials: carpeta de materiales.
- Physc Materials: Materiales de física.
- Scenes: Escenarios.
- Scripts: archivos de código.
- Prefabs: donde se guardan los objetos prefabricados.

Prefabs
*******
Los prefabs son objetos que se encuentran guardado y preparados en la carpeta de assets. Para crear un prefab solo
hay que arrastrar de la jerarquía un objeto a la carpeta prefabs dentro de assets.

Componentes
###########

Rigidbody
*********
Componente de física que contiene las siguientes funciones:

- Mass(masa): establece un valor numérico que indica la cantidad de masa que tiene un objeto.
- Drag(arrastre): genera un nivel de amortiguación, a más cantidad, más se frenará solo el objeto al moverse y al caer.
- Angular Drag(ángulo de arrastre): Amortiguación rotacional
- Use Gravity(usar gravedad): Activa o desactiva la gravedad
- Is Kinematic (es cinemático): Activa o desactiva física
- Interpolate (interpolar): Asegura la sincronía de física y animaciones
- Collition Detection (detector de colisiones)
- COnstraints (restrinciones): Limita o impide modificaciones en los ejes seleccionados.

.. attention:
    El componente Rigidbody no se establece por defecto, cualquier objeto que no lo posea no reaccionará a movimiento ni impacto de otros objetos

Creamos un objeto **sphere** y le añadimos el siguiente script:

.. code-block:: C#
    :linenos:

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine; 

    public class NewBehaviourScript : MonoBehaviour
    {
        public float velocidad = 2f; // establecemos la velocidad
        Rigidbody cuerpoRigido; // declaramos un objeto de tipo cuerpo rígido
 
        void Start()
        {
            // inicializamos el cuerpo rígido recuperando el componente de únity:
            cuerpoRigido = GetComponent<Rigidbody>();
        }

        void Update()
        {
            // ahora vamos a recuperar movimientos del teclado:
            float moverVertical = Input.GetAxis("Vertical");
            float moverHorizontal = Input.GetAxis("Horizontal");

            // vamos a crear movimiento con un vector X,Y,Z siendo la Y nada en este caso:
            Vector3 movimiento = new Vector3(moverHorizontal, 0f, moverVertical);

            // ahora toca añadir fuerza a la pelota para que responda a los movimientos:
            cuerpoRigido.AddForce(movimiento * velocidad);
        }
    }


Colliders
*********
Son los colisionadores, establecen la forma física no traspasable de un objeto:
* Box Collider - cajas
* Sphere Collider - Esferas
* Mesh Collider - Mallas (objetos irregulares)
* Physc Material: acepta un material de tipo física para añadir rebote entre otras cosas.
* Capsule Collider - Cápsulas
* Terrain - Terreno

Métodos:
* Is trigger: convierte al objeto en disparador
* Material: Agrega efectos físicos como rebote y brillo metalizado entre otros.
* Center: El centor del Collider
* Radious: Solo para esferas, establece el radio de contacto del objeto.
* Size: excepto esferas, establece el radio de contacto de un objeto.

Triggers
********
Son los detonantes (is trigger debe estar activado), el 
elemento puede perder su física para disparar un evento.
* ideal para objetos recolectables.

Prueba a colocar junto a la esfera anterior un cubo al que le asignamos "is trigger" y le añadimos el siguiente script:

.. code-block:: C#
    :linenos:

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;

    public class NewBehaviourScript1 : MonoBehaviour
    {
        // para activar un trigger usamos este método en lugar de los preestablecidos:
        private void OnTriggerEnter(Collider other)
        {
            print("Hola amigo");
            // destruir el objeto al tocarlo:
            Destroy(gameObject);
        }

    }

Random
######
Junto con Mathf se invoca bastante y existe una versión diferente de esta librería en Unity.

Ejemplo editando el código C# del cubo:

.. code-block:: C#
    :linenos:

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;

    public class NewBehaviourScript1 : MonoBehaviour
    {
        private void OnTriggerEnter(Collider other)
        {
            // podemos crear un número aleatorio cada vez que se toque el cubo:
            float aleatorio = Random.Range(0f, 10f);
            print(aleatorio);
        }

    }
