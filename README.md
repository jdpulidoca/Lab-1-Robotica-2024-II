# Laboratorio 1 Robótica 2024-II
### Integrantes
#### Julian David Pulido Castañeda
#### Omar Armando Pérez Ospino
## Descripción de la solución planteada
### Problemática
En la industria de alimentos, en especial panadería, quieren mejorar su proceso de producción. Ellos consideran que el proceso de decoración de sus tortas puede ser ejecutado por robots. Se propone hacer la decoración de una torta virtual, es decir, sobre una superficie plana bien sea redonda o rectangular, escribir 5 primeras letras de los nombres de cada uno de los integrantes del grupo y una decoracion a su gusto. En este caso se desea generar los <i>paths</i> o los movimientos de robot necesarios para representar las letras y la decoración. 

Se deben tener en cuenta las siguientes restricciones:
<ul>
  <li>El tamaño de la torta es para 20 personas.</li>
  <li>Las trayectorias a desarrollar deberan realizarse en un rango de velocidades entre 100 y 1000.</li>
  <li>La zona tolerable de errores maxima debe ser de z10.</li>
  <li>El movimiento debe partir de una posición home especificada (puede ser el home del robot), realizar la trayectoria de cada palabra y decoración con un trazo continuo. El movimiento debe finalizar en la misma posicion de home en la que se inicio.</li>
  <li>La decoracion de la torta debe ser realizada sobre una papel. El papel puede ser fijado sobre una superficie horizontal o sobre una plano inclinado.</li>
  <li>Los nombres deben estar separados.</li>
  
</ul>

Además se deben incluir señales de entrada y salidas. Se deben crear dos entradas y dos salidas digitales configurándolas correctamente en el codigo de RAPID.

<ul>
  <li>La primera señal de entrada debe iniciar una rutina de decorado sobre cualquier superficie y encender una luz de indicacion. Al final de la rutina el brazo debe regresar a su posicion de HOME donde todos los angulos articulares son 0 grados.</li>
  <li>La segunda señal de entrada debe posicionar el brazo en una pose de mantenimiento donde se pueda instalar o desinstalar la herramienta y se indique el estado con la segunda luz.</li>
</ul>

### Solucion

En cuanto a la solucion, se plantea el tamaño que debe tener un pastel circular para 20 personas por lo cual se realiza la consulta y se obtiene el dato de que en promedio este es de un tamaño de 25 cm de diametro con una altura de entre 10 y 20 cm. Por lo cual se parte de estas dimensiones para realizar los recorridos de las decoraciones.

Para los nombres, se usaron los primeros nombres o abreviaciones de los mismo, ademas de la primera letra del apellido de cada integrante. Ademas, con el fin de crear un diseño simple pero llamativo con los nombres, se usa una recreacion de la fuente usado en videojuego <i>Devil May Cry 5</i> como fuente base del diseño.

<div align="center">
  <img src="./Media/Fotos/nombres.PNG" width="600" title="nombres">
  <p>Figura 1. Nombres con fuente estilizada.</p>
</div>

En cuento a la decoracion, se busco usar un logo ya existen con el fin de agilizar el trazado de las trayectorias del robot. Se opto por el emblema de la saga <i>Assassin's Creed</i> debido a que presenta un equlibrio optimo entre simplicidad y complejidad.

<div align="center">
  <img src="./Media/Fotos/logo.PNG" width="600" title="logo">
  <p>Figura 2. Emblema <i>Assassin's Creed</i>.</p>
</div>

Por ultimo se modelan estos dibujos junto a las dimensiones del pastel en un entorno 3D (<i>OnShape</i>) con el fin de facilitar la creacion de puntos y trayectorias en <i>RobotStudio</i> mediante la seleccion de vertices que permite el software.

<div align="center">
  <img src="./Media/Fotos/pastel.PNG" width="600" title="pastel">
  <p>Figura 3. CAD Pastel decorado.</p>
</div>



## Diagrama de flujo de acciones del robot

Se planteo el siguiente diagrama de flujo sobre las acciones que el robot debe cumplir para dar solucion a la problematica planteada.

<div align="center">
  <img src="./Media/Fotos/DiagramaFlujo.PNG" width="900" title="digflu">
  <p>Figura 1. Diagrama de Fujo de las acciones del robot.</p>
</div>

En primera instancia se da un reinicio general a los testigos y posicion con el fin de evitar problemas durante la ejecucion de las rutinas. Posteriormente, se evalua si la primera entrada digital esta activa:

<ul>
<li> En caso afirmativo, se enciende el testigo correspondiente y ejecuta la rutina de los nombres y el logo en orden, y por ultimo de vuelve el manipulador a su posicion inicial y apaga el testigo.
<li> En caso neagtivo, continua a la siguinete funcion.
</li>
</ul>

La siguiente funcion corresponde a evaluar si la segunda entrada digital esta activa:

<ul>
<li> En caso afirmativo, se enciende el testigo correspondiente y pociona el manipulador en su ubicacion de mantenimiento, y espera hasta que se vuelva a activar la segunda entrada digital. Si se activa la señal, el manipulador vuelve a su posicon incial y apaga el testigo.
<li> En caso negativo, continua a la siguinete funcion.
</li>  
</ul>

Ambas condiciones estan en un ciclo perpetuo, por lo cual si ninguna de la señales de entra es accionada, se repeti el ciclo de verificacion hasta que alguna sea activada.

## Plano de planta de la ubicación de cada uno de los elementos

<div align="center">
  <img src="./Media/Fotos/Planta.PNG" width="300" title="digflu">
  <p>Figura 1. Diagrama de Fujo de las acciones del robot.</p>
</div>

<div align="center">
  <img src="./Media/Fotos/Planta2.PNG" width="300" title="digflu">
  <p>Figura 1. Diagrama de Fujo de las acciones del robot.</p>
</div>

## Descripción de las funciones utilizadas

<ul>
  <li><code>main()</code> Es la función principal del programa, llama a todas las funciones que realizan el movimiento del manipulador y contiene toda la lógica de la entradas y salidas digitales.
  <li><code>goHome()</code> Posee una sola instrucción tipo MoveAbsJ que envía todas las articulaciones del robot a cero.</li>
  <li><code>mantenimiento()</code> De manera similar a <code>goHome()</code>, esta función utiliza una instrucción MoveAbsJ para envíar las articulaciones del robot a una posición específica. En este caso envía las articulaciones 3 y 5 a las posiciones -30° y -50°, respectivamente.</li>
  <li><code>omarp()</code></li> Realiza la trayectoria que dibuja la secuencia de letras "omar p".
  <li><code>julip()</code></li> Realiza la trayectoria que dibuja la secuencia de letras "juli p".
  <li><code>logo()</code></li> Realiza la trayectoria que dibuja el logo diseñado.
</ul>

## Diseño de la herramienta
Para el diseño de la herramienta se buscó que fuese posible cambiar fácilmente el instrumento de escritura, que en este caso se trata de un marcador borrable, y que a su vez éste se encuentre correctamente firmemente agarrado a la herramienta. Para ello se ha diseñado una abrazadera (figura 1), que se ajusta a objetos cilíndricos de aproximadamente 16 mm, que es la medida del diámetro del tipo de marcador usado.

<div align="center">
  <img src="./Media/Fotos/abrazadera.PNG" width="300" title="abrazadera">
  <p>Figura 1. Abrazadera diseñada para sostener el elemento de escritura.</p>
</div>

Adicionalmente, se ha diseñado en la herramienta una junta prismática de cuenta con un resorte para permitir un cierto grado de error en el posicionamiento del marcador. El resultado final de la herramienta diseñada se muestra en la figura 2.

<div align="center">
  <img src="./Media/Fotos/tool.PNG" width="500" title="tool">
  <p>Figura 2. Modelo CAD de la herramienta diseñada.</p>
</div>

La fabricación de la herramienta diseñada se realizó con el método manufactura aditiva utilizando PLA. En la figura 3 se muestra la herramienta fabricada.

<div align="center">
  <img src="./Media/Fotos/toolreal.jpg" width="500" title="toolreal">
  <p>Figura 3. Foto de la herramienta fabricada en PLA por medio de manufactura aditiva.</p>
</div>

Para hallar el TCP se utilizaron dos métodos: el primero fue utilizar el TCP calculado directamente mediante RobotStudio utilizando el modelo CAD y el segundo fue directamente en el FlexPendant mediante el método de definición TCP & Z. En la tabla 1 se muestra una comparación entre los resultados obtenidos mediante los dos métodos.

<table align="center">
  <tr>
    <th>TCP</th>
    <th>CAD</th>
    <th>Manual</th>
  </tr>
  <tr>
    <td>x</td>
    <td>148.954</td>
    <td>142.652</td>
  </tr>
  <tr>
    <td>y</td>
    <td>0</td>
    <td>37.0488</td>
  </tr>
  <tr>
    <td>z</td>
    <td>67.083</td>
    <td>68.0102</td>
  </tr>
  <tr>
    <td>q1</td>
    <td>0.793353</td>
    <td>0.94672</td>
  </tr>
  <tr>
    <td>q2</td>
    <td>0</td>
    <td>0.284099</td>
  </tr>
  <tr>
    <td>q3</td>
    <td>0.608761</td>
    <td>0.145287</td>
  </tr>
  <tr>
    <td>q4</td>
    <td>0</td>
    <td>0.0435988</td>
  </tr>
</table>
<p align="center">Tabla 1. Comparación de valores de TCP obtenidos por medio del modelo CAD y de manera manual por el método TCP & Z.</p>

## Código en RAPID del módulo utilizado para el desarrollo de la practica.
## Video que contenga la simulación en RobotStudio, así como la implementación de la práctica con los robots reales.

Mira el video dando clic en la imagen:

<div align="center">
  <a href="[https://www.youtube.com/watch?v=VIDEO_ID](https://youtu.be/YRvLADFy390)">
    <img src="https://img.youtube.com/vi/YRvLADFy390/0.jpg" alt="Ver el video en YouTube">
  </a>
</div>

