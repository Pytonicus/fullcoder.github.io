Framework: React Native   
=======================

.. image:: /logos/logo-react-native.png
    :scale: 35%
    :alt: Logo React native
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica de React Native para desarrollo de aplicaciones Híbridas.

.. contents:: Índice
  
Configuraciones
###############  

Instalar dependencias de react native 
*************************************

Tener instalado NodeJS desde su página oficial: https://nodejs.org/es/

.. attention::
    npx viene instalado con npm y es su versión en la nube. De modo que si necesitas un paquete y no deseas instalarlo en tu máquina utiliza npx en lugar de npm.

Herramientas de desarrollo 
**************************

App para ejecutar proyecto en fase desarrollo:

- Android: https://play.google.com/store/search?q=expo&c=apps&hl=es&gl=US

Emular aplicación
*****************

- Para utilizar un emulador de Android, instalamos Android Studio y ejecutamos el icono del movil con la cabeza de android para ejecutar el ADV Manager. Arrancamos un emulador y ya podemos usarlo ejecutando el proyecto con ``npm run android`` o ``npm start`` y luego tecla **a**.

Comandos básicos 
****************

- Crear proyecto: ``npx create-expo-app my-app`` (crea un proyecto en blanco o con sistema de navegación y seguir los pasos).
- Ejecutar proyecto con emulador: ``npm run android`` (existen tres opciones: **android**, **ios** y **web**).
- Ejecutar proyecto en la App oficial (recomendado): ``npm start`` (muestra un qr que podremos escanear con nuestro movil con la app de expo)

.. attention:: 
    Utilizamos npx para no tener que instalar expo y así tener compatibilidad en cualquier sistema a la hora de instalar.

Estructura básica de react native 
*********************************

La estructura básica de react native es similar a la de React. El archivo **App.js** se presenta de la siguiente forma:

.. code-block:: 

    import { StatusBar } from 'expo-status-bar';
    import { StyleSheet, Text, View } from 'react-native';

    export default function App() {
    return (
        <View style={styles.container}>
        <Text>Buenas!</Text>
        <StatusBar style="auto" />
        </View>
    );
    }

    const styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#fff',
        alignItems: 'center',
        justifyContent: 'center',
    },
    });

Estructura similar a React  
**************************

La programación es básicamente idéntica a la de react en su base. Por tanto es recomendable echar un ojo al manual de react: 
https://pytonicus.github.io/fullcodersite/javascript/react.html


Estructura recomendada para el proyecto
***************************************

Lo ideal es crear una estructura escalable, este es un ejemplo de estructura recomendada:

- **src**: Crear carpeta en la raiz del proyecto llamada src para todo nuestro código. Dentro de ella creamos:
    - **components**: carpeta para los componentes del proyecto.
    - **screens**: carpeta para las pantallas del proyecto. Por cada pantalla creamos una carpeta.
    - **navigation**: carpeta para añadir la configuración de navegación 
    - **data**: carpeta para guardar información en la aplicación.

Trabajando con componentes 
##########################

Crear una pantalla o screen 
***************************

En la carpeta screens, creamos una carpeta para la pantalla a la que llamaremos **main** y el archivo será **index.js** al que le pasaremos casi toda la lógica de *App.js**:

.. code-block:: 

    import { StyleSheet, Text, View } from 'react-native';

    export default function MainScreen() {
        return (
            <View style={styles.container}>
                <Text>Prueba de Index</Text>
            </View>
        );
    }

    const styles = StyleSheet.create({
        container: {
            flex: 1,
            backgroundColor: '#fff',
            alignItems: 'center',
            justifyContent: 'center',
        },
    });

- Ahora para cargar la pantalla vamos a editar **App.js**:

.. code-block:: 

    // importamos la pantalla nueva:
    import Main from "./src/screens/main/index";

    export default function App() {
    // retornamos solamente la pontalla ya que si usamos view por ejemplo nos limitará.
    return (
        <Main /> 
    );
    }

.. note::
    El componente que se utiliza para pintar una pantalla es **<View>** y solo podemos utilizarlo una vez por pantalla.

Trabajando con estilos 
**********************

.. code-block:: 

    import { StyleSheet, Text, View } from 'react-native';

    export default function MainScreen() {
        return (
            <View style={styles.container}>
                {/* cargar un estilo en componente: */}
                <Text style={styles.text}>Texto normal</Text>
                {/* cargar varios estilos en componente: */}
                <Text selectable style={[styles.text, styles.textSelect]}>Texto seleccionable</Text>
            </View>
        );
    }

    // definición de estilos (cambia el metodo de escritura de kebab-case a camelCase):
    const styles = StyleSheet.create({
        container: {
            flex: 1,
            backgroundColor: '#fff',
            alignItems: 'center',
            justifyContent: 'center',
        },
        text: {
            color: "#ff0000",
            fontSize: 30
        },
        textSelect: {
            backgroundColor: "blue",
            fontSize: 15
        }
    });

Tipos de Componentes React Native 
#################################

Componente View (pantalla)
**************************

Es un componente para crear una pantalla:

.. code-block:: 

    import { Text, View } from 'react-native';

    export default function MainScreen() {
        // todo lo que vaya dentro de View se mostrará en la pantalla del dispositivo de modo similar al componente Template de ReactJS:
        return (
            <View>
                <Text>Texto dentro de pantalla</Text>
            </View>
        );
    }

Componente Text (textos)
************************

.. code-block:: 

    import { StyleSheet, Text, View } from 'react-native';

    export default function MainScreen() {
        return (
            <View style={styles.container}>
                {/* Ejemplos de texto: */}
                <Text>Texto normal</Text>
                <Text selectable>Texto seleccionable</Text>
            </View>
        );
    }

    const styles = StyleSheet.create({
        container: {
            flex: 1,
            backgroundColor: '#fff',
            alignItems: 'center',
            justifyContent: 'center',
        },
    });

