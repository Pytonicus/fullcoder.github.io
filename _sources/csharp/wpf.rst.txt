Interfaces gráficas: WPF
========================

.. image:: /logos/logo-csharp.png
    :scale: 80%
    :alt: Logo C#
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M
 

Interfaces gráficas con WPF en C#

.. contents:: Índice 

Configurar Visual Studio
########################

* Abrir el Visual Studio Installer
* Añadir en carga de trabajos **Desarrollo de escritorio .NET**
 
Crear un Proyecto
*****************
* Para crear un nuevo proyecto seleccionamos la opción **APlicacion de WPF (.NET Framework)** y le ponemos el nombre que queramos.
* Cargará el proyecto con una ventana inicial.

.. note::
    Se puede trabajar tanto en la ventana como en el código.

.. note:: 
    A la izquierda podemos desplegar un **cuadro de herramientas** para añadir cosas a la ventana.

XAML
####

Es un lenguaje que permite escribir toda la interfaz de usuario.

Estructura básica
*****************

Al crear el proyecto tenemos el siguiente archivo principal llamado MainWindow.xaml

.. code-block:: xml
    :linenos:

    <Window x:Class="wpf_01.MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
            xmlns:local="clr-namespace:wpf_01"
            mc:Ignorable="d"
            Title="MainWindow" Height="450" Width="800">
        <!-- Dentro de grid se agrega el contenido de la ventana -->
        <Grid>
            <!-- Cada etiqueta de elemento tiene dentro unos atributos que ajustan su estilo -->
            <Button Content="Botón de prueba" Height="30" Width="120"></Button>
        </Grid>
    </Window>

Tipos de contenedores
*********************

StackPanel
++++++++++

.. code-block:: xml 
    :linenos:

    <!-- Stack panel apila elementos de arriba abajo y reemplaza al Grid: -->
    <StackPanel>
        <TextBlock HorizontalAlignment="Center" Margin="12">Tus videoconsolas</TextBlock>
        <ListBox Height="80" Width="500">
            <ListBoxItem Content="PlayStation" />
            <ListBoxItem Content="Gameboy" />
            <ListBoxItem Content="Nintendo DS" />
        </ListBox>
        <Button Content="Añadir consola" Margin="20" Click="Button_Click"></Button>
    </StackPanel>

WrapPanel
+++++++++

.. code-block:: xml
    :linenos:

    <WrapPanel>
        <TextBlock Text="Hola amigo" Margin="20" />
        <Button Margin="20">Botón</Button>
        <Button Margin="20">Otro botón</Button>
    </WrapPanel>

Grid
++++

.. code-block:: xml 
    :linenos:

    <Grid>
        <!-- Opcionalmente se puede definir las columnas: -->
        <Grid.ColumnDefinitions>
            <!-- cada columna tendrá una posición como un array: -->
            <ColumnDefinition Width="200"/>
            <ColumnDefinition Width="200"/>
            <ColumnDefinition Width="200"/>
            <ColumnDefinition Width="200"/>
        </Grid.ColumnDefinitions>
        <!-- Opcionalmente se pueden definir filas: -->
        <Grid.RowDefinitions>
            <!-- con * se ajusta todo el alto o ancho que pueda: -->
            <RowDefinition Height="*"/>
            <RowDefinition Height="*"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
        <!-- Asignar botón a primera columna segunda fila: -->
        <Button Content="Botón" Grid.Column="0" Grid.Row="1" />
        <!-- Asignar botón a segunda columna primera fila: -->
        <Button Content="Botón" Grid.Column="1" Grid.Row="0" />
        <!-- Asignar botón a tercera columna tercera fila: -->
        <Button Content="Botón" Grid.Column="2" Grid.Row="2" />
    </Grid>

Elementos Comunes
*****************

Button
++++++

Botón sencillo.

Estructura del elemento:

.. code-block:: xml
    :linenos:

    <Button Height="30" Click="Lanzar_Mensaje">Texto</Button>

Atributos comunes:

* Content: texto del botón, también se puede poner en entre etiquetas.
* Height: define el alto. Recibe valor numérico.
* Width: define el ancho. Recibe valor numérico.
* FontSize: Tamaño de fuente. Recibe valor numérico.
* Foreground: Color de fuente. Recibe color en texto o hexadecimal.
* HorizontalAlignment: Alineación horizontal. Valores Left, Center y Right.
* Margin: margen entre elementos externos. Recibe valor numérico.
* ToolTip: Mensaje de ayuda que se muestra al situar el ratón sobre el elemento.
* Name: Se asigna un identificador al elemento para localizarlo en el código.

TextBlock
+++++++++

Bloque de texto.

Estructura del elemento:

.. code-block:: xml
    :linenos:

    <TextBlock HorizontalAlignment="Center" Margin="12">Tus videoconsolas</TextBlock>

Atributos comunes:

* Content: texto del botón, también se puede poner en entre etiquetas.
* Height: define el alto. Recibe valor numérico.
* Width: define el ancho. Recibe valor numérico.
* FontSize: Tamaño de fuente. Recibe valor numérico.
* Foreground: Color de fuente. Recibe color en texto o hexadecimal.
* HorizontalAlignment: Alineación horizontal. Valores Left, Center y Right.
* Margin: margen entre elementos externos. Recibe valor numérico.
* ToolTip: Mensaje de ayuda que se muestra al situar el ratón sobre el elemento.
* Name: Se asigna un identificador al elemento para localizarlo en el código.

ListBox y ListBoxItem
+++++++++++++++++++++

Listado de elementos y elementos internos del mismo.

Estructura del elemento:

.. code-block:: xml
    :linenos:

    <ListBox Height="80" Width="500" >
        <ListBoxItem Content="PlayStation" />
        <ListBoxItem Content="Gameboy" />
        <ListBoxItem Content="Nintendo DS" />
    </ListBox>

Atributos comunes:

* Content: texto del botón, también se puede poner en entre etiquetas.
* Height: define el alto. Recibe valor numérico.
* Width: define el ancho. Recibe valor numérico.
* FontSize: Tamaño de fuente. Recibe valor numérico.
* Foreground: Color de fuente. Recibe color en texto o hexadecimal.
* HorizontalAlignment: Alineación horizontal. Valores Left, Center y Right.
* Margin: margen entre elementos externos. Recibe valor numérico.
* ToolTip: Mensaje de ayuda que se muestra al situar el ratón sobre el elemento.
* Name: Se asigna un identificador al elemento para localizarlo en el código.

TextBlock
+++++++++

Caja de texto.

Estructura del elemento:

.. code-block:: xml 
    :linenos:

    <TextBox Width="80" Height="25" Margin="10" />

Atributos comunes:

* Text: Contenido autodefinido de la caja.
* Height: define el alto. Recibe valor numérico.
* Width: define el ancho. Recibe valor numérico.
* FontSize: Tamaño de fuente. Recibe valor numérico.
* Foreground: Color de fuente. Recibe color en texto o hexadecimal.
* HorizontalAlignment: Alineación horizontal. Valores Left, Center y Right.
* Margin: margen entre elementos externos. Recibe valor numérico.
* ToolTip: Mensaje de ayuda que se muestra al situar el ratón sobre el elemento.
* Name: Se asigna un identificador al elemento para localizarlo en el código.

Slider
++++++

Barra de selección con valor decimal.

Estructura del elemento:

.. code-block:: xml 
    :linenos:

    <Slider Name="SliderPrueba" Minimun="0" Maximum="100" />

Atributos comunes:

* Value: Valor autodefinido de la caja.
* Minimun: valor mínimo aceptado.
* Maximum: Valor máximo permitido.
* IsSnapToTickEnabled: definie si el valor es entero en lugar de decimal.
* Height: define el alto. Recibe valor numérico.
* Width: define el ancho. Recibe valor numérico.
* HorizontalAlignment: Alineación horizontal. Valores Left, Center y Right.
* Margin: margen entre elementos externos. Recibe valor numérico.
* ToolTip: Mensaje de ayuda que se muestra al situar el ratón sobre el elemento.
* Name: Se asigna un identificador al elemento para localizarlo en el código.

Dependency Properties: Propiedades de dependencias
**************************************************

Es un modo de generar estilos y animaciones a los elementos de WPF:

.. code-block:: xml 
    :linenos:

    <Button Height="50" Width="100" Content="Botón mágico" Background="Green">
            <!-- Se genera un estilo con el elemento -->
            <Button.Style>
                <!-- dentro del elemento se añade una etiqueta de estilo que apunte al elemento que queremos cambiar: -->
                <Style TargetType="Button">
                    <!-- Se puede establecer uno o varios elementos disparadores: -->
                    <Style.Triggers>
                        <!-- ejemplo de disparador por posición: -->
                        <Trigger Property="IsMouseOver" Value="True">
                            <!-- Adherimos el nuevo atributo del elemento escogido: -->
                            <Setter Property="FontSize" Value="24"/>
                            <Setter Property="Foreground" Value="Red"/>
                        </Trigger>
                    </Style.Triggers>
                </Style>
            </Button.Style>
        </Button>

.. Note::
    Esta estructura se puede aplicar a otros elementos para generar estilos y animaciones interactivas.


Lógica de WPF
#############

Si la estructura de una ventana en XAML se escribe en **MainWindow.xaml**:

.. code-block:: xml 
    :linenos:

    <Window x:Class="wpf_01.MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
            xmlns:local="clr-namespace:wpf_01"
            mc:Ignorable="d"
            Title="MainWindow" Height="450" Width="800">
        <Grid>
            <Button Content="Lanzar mensaje" Width="200" Height="40" Click="Lanzar_Mensaje" ></Button>
        </Grid>
    </Window>


la lógica se añade en el archivo MainWindow.xaml.cs en código C#:

.. code-block:: C#
    :linenos:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Data;
    using System.Windows.Documents;
    using System.Windows.Input;
    using System.Windows.Media;
    using System.Windows.Media.Imaging;
    using System.Windows.Navigation;
    using System.Windows.Shapes;

    namespace wpf_01
    {
        /// <summary>
        /// Lógica de interacción para MainWindow.xaml
        /// </summary>
        public partial class MainWindow : Window
        {
            public MainWindow()
            {
                InitializeComponent();
            }
            // método creado que se dispara al hacer clic en el botón
            private void Lanzar_Mensaje(object sender, RoutedEventArgs e)
            {
                // mostrar una ventana emergente:
                MessageBox.Show("Soy una ventana emergente");
            }
        }
    }

.. note::
    Al establecer un evento Visual Studio nos brinda la opción de generar automáticamente el método.
    Es recomendado utilizar esa acción ya que también te implementa los parámetros correctos.

RoutedEvents: Eventos
*********************

* Click: Dispara un evento al pulsarlo. Recibe el nombre de la función que ejecutará.
* MouseUp: Dispara un evento al hacer click y luego soltar el botón derecho. Recibe el nombre de la función que ejecutará.
* PreviewMouseLeftButtonDown: Dispara un evento al hacer click izquierdo.
* PreviewMouseRightButtonDown: Dispara un evento al hacer click derecho.
* PreviewMouseLeftButtonUp: Dispara un evento al hacer click izquierdo y soltar.
* PreviewMouseRightButtonUp: Dispara un evento al hacer click derecho y soltar.


Data Binding: Enlace de datos
*****************************

Como se establece un enlace de datos desde un origen en C# al destino en XAML:

* OneWay: Enlace desde origen a destino.
* TwoWay: Comunicación mutua entre origen y destino.
* OneWayToSource: Enlace desde destino a origen.
* OneTime: Enlace desde origen a destino que se ejecuta solo una vez.

Binding: Enlazando datos 
++++++++++++++++++++++++

Enlace de datos que se realiza con llaves y que puede contener las siguientes propiedades:
* ElementName: Nombre del elemento con el que va a vincularse.
* Path: Atributo del elemento vinculado que va a recuperar.
* Mode: Modo de enlace (OneWay, TwoWay, OneWayToSource, OneTime)

.. code-block:: xml 
    :linenos:

    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="*" />
            <RowDefinition Height="*" />
            <RowDefinition Height="*" />
            <RowDefinition Height="200" />
        </Grid.RowDefinitions>
        <WrapPanel Grid.Row="0" HorizontalAlignment="Center">
            <TextBlock Text="Número 1" Margin="20" />
            <TextBox Width="80" Height="25" Margin="10" Name="Num1" />
            <TextBlock Text="Número 2" Margin="20" />
            <TextBox Width="80" Height="25" Margin="10" Name="Num2"/>
        </WrapPanel>
        <WrapPanel Grid.Row="1" HorizontalAlignment="Center">
            <TextBlock Text="{Binding ElementName=Num1, Path=Text, Mode=OneWay}" Margin="5" />
            <TextBlock Name="Operacion" Text="+" Margin="5" />
            <TextBlock Text="{Binding ElementName=Num2, Path=Text, Mode=OneWay}" Margin="5" />
            <TextBlock Text="=" Margin="5" />
            <TextBlock Name="Resultado" Text="0" Margin="5" />
        </WrapPanel>
        <WrapPanel Grid.Row="2" HorizontalAlignment="Center">
            <Button Content="sumar" Width="80" Margin="10" Height="30"/>
            <Button Content="restar" Width="80" Margin="10" Height="30"/>
            <Button Content="multiplicar" Width="80" Margin="10" Height="30"/>
            <Button Content="dividir" Width="80" Margin="10" Height="30"/>
        </WrapPanel>
        <Button Grid.Row="3" Width="150" Height="50" FontSize="24" Content="calcular" />
    </Grid>

INotfyPropertyChanged: Detectar y recuperar datos
+++++++++++++++++++++++++++++++++++++++++++++++++

Detectar cambios en XAML y recuperarlos en C#.

* Asignar variables Binding en XAML:

.. code-block:: xml 
    :linenos:

    