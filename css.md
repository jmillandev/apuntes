# 1 Fundamentos

## 1.1 Sintaxis
Puede echarle un vistazo a al vocabulario de css [aqui](http://apps.workflower.fi/vocabs/css/en#comment)
- Comentarios:

`/* Esto es un comentario en CSS */`

- Variable:
```css
/* Esta es la manera de declarar las variables en css: */
:root {
    --nameVar1: value;
    --nameVar2: value;
}
/* Una ves declarada la variable la utilizamod escribiendo 'var(--nameVar)' */
```

## 1.2 Estilos del navegador
Por defecto cada browser contiene un estilo de css. Esto puede ocasionar distinta clase de problemas a la hora de nosotros implementar nuestros estilos.
La manera de resolver esto es utilizando una libreria de terceros llamada [normalize](https://necolas.github.io/normalize.css/) que como su nombre lo indica nos normaliza los estilos por defecto que vayamos a utilizar.

# 2 Selectores
Se dividen esencialmente en 3 tipos:

1. Sencillos.
2. Compuestos.
3. De atributos.

## 2.1 Sencillos
Son selectores de un solo elemento. Existen varios:

### 2.1.1 Selector de elemento o tipo
Es el mas sencillo de todos que es basicamente el nombre de una etiqueta HTML o XML. Ejemplo:

`body { ... }`

*NOTA:* **NO** es recomendado modificar estos estilos a menos que estes muy claro de lo que estas haciendo.

### 2.1.2 Selectores de clases
Son los mas recomentados y utiles al momento de escribir los estilos de un proyecto. Se escribe anteponiendo el nombre de la clases por un punto(.). Ejemplo:

`.nameClass { ... }`

### 2.1.3 Selectores de ID
Se escribe anteponiendo el nombre de la clases por un  hash(#). Ejemplo:

`#nameID { ... }`

*NOTA:* Su uso no es para nada recomendado en css

### 2.1.4 Selector universal
Se denota con el caracter *. Como su nombre lo indica le aplica los estilos a todos los elementos. Ejemplo:

`* { ... }`

**IMPORTANTE:** *NO* utilices este selector a menos que estes muy claro(pero extremadamente claro) de lo que estas haciendo y tienes ya tienes un nivel elevado en CSS. **Puede ocasionar bugs**.

## 2.2 Compuestos
Estos a su vez se dividen en varios tipos. Es importante aclarar que el nombre oficial no es 'selectores compuestos' este nombre es unicamente para objetivos didacticos.

### 2.2.1 Selectores agrupados
Nos permiten asignar estilos a varios selectores en un mismo bloque de codigo. Esto lo hacemos separando los selectores con comas(,). Ejemplo:
```CSS
/* El siguiete codigo coloca un fondo color rojo para los elementos de las clase
'nameClass1', el elemento de ID 'nameID' y los parrafos. */

.nameClass1,
#nameID,
p {
    background: red;
}
```

### 2.2.2 Selectores desendientes
Nos permiten asignar estilos a un elemento que sea *desendiente* (hijo, nieto, etc) de otro elemento. Esto lo hacemos dejando un escio en blanco(' ') entre los selectores. Ejemplo:

```css
/* El siguiente codgio le coloca un fondo blanco a los parrafos que sean hijo de la clase dashboard-dark*/

.dashboard-dark p {
    background: white;
}
```

**IMPORTANTE:** esta debe ser una de las *ULTIMAS* opciones que utilicemos. Esto nos puede traer o ocasionar bugs.

*NOTA:* Debes tener cuidado de dejar el espacio en blanco entre los selectores, de no ser asi estas indicando que quieres seleccionar un elemento que cumple con TODAS las caracteristicas descritas(para el caso del ejemplo anterior, un parrafo que pertenece a la clase dashboard-dark).

### 2.2.3 Selector hijo directo
Es utilizador para asignar estilo a un *hijo directo*(no nietos, ni hermanos, ni nada mas. Solo hijos directos) de otro elemento. Esto lo hacemos a traves del operador *mayor que(>)* Ejemplo:
```css
/* En el siguiente codigo ocultaremos los formulario que sean hijo directos de un elemento de clase 'desabilitado' */

.deshabilitado > form {
    display: none;
}
```

### 2.2.4 Selector hermano siguiente
Es utilizado para asignarle estilo al hermano(del arbol DOM) que le sigue inmediatamente al primer elemento. Este lo hacemos a traves de el operador mas(+) Ejemplo:
```css
/* Si el elemento que sigue despues de un h1 es un parrafo este tendra una fuente color rojo */

h1 + p {
    color: red;
}
```

### 2.2.5 Selector hermanos siguientes
Es utilizado para asignarle estilo a **todos** los hermanoz(del arbol DOM). Este lo hacemos a traves de el operador mas(~) Ejemplo:

```css
/* Todos los hermano de h1 que sigan despues de el y  tengan la clase bg-black tendra una un fondo negro */

h1 ~ p {
    background: red;
}
```
## 2.3 Selectores de atributos
La forma de utilizar estos selectores es por medio de los corchetes( [] ). Exites varias maneras de hacer la implementacion:

### 2.3.1 Atributo y valor
Los hacemos de la misma manera como seria en codigo *HTML* pero esta vez encerrandolo en corchetes. Tambien podemos escribir solo el atributo sin espeficicar el valor. Ejemplo:
 ```css
 /* El siguiente codigo le coloca un fondo rojo y letras blancas a un button de tipo submit */

 [type='submit'] {
     background: red;
     color: white;
 }
 
 /* Se le asigna un borde solido rojo de un pixcel a los elementos de tipo requeridos */

 [required] {
     border: 1px solid red;
 }
 ```

 **NOTA:** Podemos utilizar notaciones para escapar caracteres. entre las opciones disponibles tenemos:

- Selecciona todos los elementos que su atributo href **comiencen** con losvalores /
```css
[href^='/'] {
    /* Asignacion de estilos */
}
```

- Selecciona todos los elementos que su atributo href **terminen** con los valores .jgp
```css
[href$='.jpg'] {
    /* Asignacion de estilos */
}
```

- Selecciona todos los elementos que su atributo class **contine** el valor button-
```css
[href*='button-'] {
    /* Asignacion de estilos */
}
```

- Selecciona todos los elementos que su atributo class **contine(separado por espacios)** el valor btn
```css
[href~='btn'] {
    /* Asignacion de estilos */
}
```

# 3 Especificidad
Al crecer nuestro codigo css es muy probable que tengamos problemas al asignarle dos estilos distintos a un mismo elemento. Esto es muy comun cuando utilizamos librerias de 3eros en nuestro codigo. Aqui es donde entra en juego la especificidad, que trata de ¿que tan espeficico es el selector que utilizamos?. Esto se calcula a traves de una suma, a continuacion una tabla con los elementos y su valor. El selector con mayor espeficidad gana.

| Elemento   | Valor                           |
| -----------|--------------------------------:|
| Tag        | 1                               |
| clases     | 10                              |
| id         | 100                             |
| inline     | 1000                            |
| !important | Es el dios (no debe utilizarce) |

**NOTA:** los selectores deberia ir escalando en su espeficidad a medida que crece el proyecto para evitar bugs.

# 4 Cascada y Herencia
Los que esta despues sobre escribe a lo que estaba antes. Tomando en cuenta que ambos selectores tienen la misma especificidad.

Todos los elementos heredan estilos de sus padres, abuelos, y su asendencia. Estos son los estilos que se mostraran por defecto a menos que sean sobre escritos por el mismo. La herencia funciona como una cascada en el arbol DOM.

**NOTA:** existen dos *keywords* que son **initial** y **inherit** que pueden  ser utilizadas como valor y lo que hacen respectivamente es inicializar(al valor por defecto) y forzar la herencia del padre respectivamente.

# 5 Box Model

## 5.1 Introduccion
El Box Model es el algoritmo a traves del cual el navegador dibuja las cajas en la pantalla. Para hablar del box model debemos tener presente alguno conceptos base:
### 5.1.1 Layout
Geometria de los elementosque se definen como, con que tamaño, com que separacion respecto a los elentos adyacentes y en que posicion se va adibujar en la pantalla.

### 5.1.2 Elemento en linea y de bloque.
Como ya debes saber HTML. Existen elemento de linea y de bloque por naturaleza. Nosotros en CSS podemos modificar la naturaleza de estos elementos(modificando su propiedad display). Algunas caracteristicas de estos elementos son las siguientes:

1. **Inline:** 
    - No crean nuevas lineas para cada elemento(los elementos se ajustan uno a los lados de los otros).
    - No se les puede definir un alto ni un ancho. Este es automatico.
    - Se ajustan a su contenido.

2. **Block:**
    - Crean una nueva linea para cada de elemento.
    - Ocupan todo el espacio horizontal disponible
    - Se les puede definir un alto y un ancho.

En CSS tenemos un tercer tipo de elemento que es el **inline-block** que combina lo mejos de ambos mundo:
- Tienen un alto y ancho que puede ser modificado.
- No crean nuevas lineas para los elementos.

## 5.2 Box Model
El box model trata justamente del modelo o modelado de las cajas(ya imaginaras que este es un elemento de caja)

**NOTA:** existe un atributo llamado **box-sizing**(sus valores son: *content-box*, *padding-box* y *border-box*).
Con el cual le indicamos al navegador que caja tendra los valores de *width* y *height* del elemento(por defecto este esta en *content-box*).

**NOTA IMPORTANTE:** Si el tamaño del alto del padre es automatico NO podremos utilizar porcentajes en el alto del elemento(no funcionara). Solo funcionan porcentaje en el alto del elemento si su padre tiene un alto definidos.
### 5.2.1 Caja de contenido
Content box. La definimos(por defecto, a menos que cambiemos el **box-sizing**) con las propiedades **width** y **height**.

### 5.2.2 Caja de relleno
Padding box. La definimos con la propiedad **padding**.
La implementacion es muy similar a la del margin(seccion 5.2.4). Aun asi una diferencia **importante** a la hora de trabajar con porcentajes en el padding es que este toma como referencia al inverso del papa. Es decir que cuando si el padre de nuestro elemento tiene un ancho de 200px y hacemos `padding-botton: 10%` lo que estamos diciendo es que asigne al elemento un padding abajo de 20px. Esto lo podemos utilizar para hacer diseños a escaja.

### 5.2.3 Caja del Borde
Border box. La definimos con la propiedad **border**.

### 5.2.4 Margin
Separacion de la caja con las cajas adyacentes.
#### 5.2.4.1 Propiedades
Las propiedades que se encanrgan de modificar los valores del margen son:

- **margin-top:** Valor_superior
- **margin-right:** Valor_derecho
- **margin-botton:** Valor_inferios
- **margin-left:** Valor_izquierdo

Ademas exites de un shorthand que es:

- **margin:** el shorthand acepta de 1 a 4 valores. a continuacion una tabla que indica como son asignados los valores

| N° Valores | Arriba | Derecha | Abajo | Izquiera |
|------------|--------|---------|-------|---------:|
| 4          | 1ero   | 2do     | 3ero  | 4to      |
| 3          | 1ero   | 2do     | 3ero  | 2do      |
| 2          | 1ero   | 2do     | 1ero  | 2do      |
| 1          | 1ero   | 1ero    | 1ero  | 1ero     |

**NOTA:** Los valores pueden ser en pixceles o en porcentaje. Tambien existe la opcion de colocar *auto*.

# 6 Bordes y Sombras

## 6.1 ¿Donde se Dibuja?
El borde se dibuja siempre por dentro de la caja, recordemos que el unico elemento externo del model box es el margen.
**NOTA:** una buena practica recordemos que es aconfigurar el `box-sizing: border-box;`. De esta manera no evitamos problemas con el maquetado ya que aunque el borde esta por dentro de nuestra caja si no hacemos esta configuracion ñe aumentara las dimensiones a la misma.

## 6.2 Propiedades bases
El borde tiene 3 propiedades bases:
### 6.2.1 border-width
Configura el grosor de la linea.
### 6.2.2 border-style
Indica el estilo que se le aplicara a la linea. Sus posibles valores son:
- none(por defecto).
- hidden.
- solid.
- dotted.
- dashed.
- double.
- groove.
- ridge.
- inset.
- outset.

### 6.2.3 border-color
EL color de la linea.

### 6.2.4 Shorthands
Existen distintos shortand para los border:

1. **border:** *width_value* *style_value* *color_value*
2. **border-top:** *width_value_top* *style_value_top* *color_value_top*
3. **border-right:** *width_value_right* *style_value_right* *color_value_right*
4. **border-botton:** *width_value_botton* *style_value_botton* *color_value_botton*
5. **border-left:** *width_value_left* *style_value_left* *color_value_left*
6. **border-width:** *width_value_top* *width_value_right* *width_value_botton* *width_value_left*
7. **border-style:** *style_value_top* *style_value_right* *style_value_botton*
*style_value_left*
8. **border-color:** *color_value_top* *color_value_right* *color_value_botton*
*color_value_left*

## 6.3 border-radius
Esta propiedad nos permite "recordar" un arco de circunferencia(de 45°) en las esquinas de nuestras cajas. 

La sintaxis es la siguiente:

- **border-top-left-radius:** *x_radius y_radius*;
- **border-top-right-radius:** *x_radius y_radius*;
- **border-botton-right-radius:** *x_radius y_radius*;
- **border-botton-left-radius:** *x_radius y_radius*;
- **border-radius:** *x_radius_top_left x_radius_top_right x_radius_botton_right x_radius_botton_left / y_radius_top_left y_radius_top_right y_radius_botton_right y_radius_botton_left*;

**NOTA:** Los valores de los radios pueden darse en *px* o en *%*

## 6.4 outline
Funciona muy parecido al borde, con la diferencia que se dibuja por fuera de la caja. si sixtaxis es: `outline: width_value style_value color_value`

## 6.5 box-shadow
Los sombras son una de las caracteristicas mas facinantes de ccs. Todo esta en practicar y experimentar con ellas. sintaxis: `box-shadow: x-off y-offset blur spread color | inset(optional)`

# 7 Fondos
El background es una propiedad muy completa en css, sus propiedades son mostradas a continuacion.

## 7.01 Color
La propiedad es tan sencilla como puede ser posible, su sintaxis es: `background-color: color_value;`

## 7.02 Image
Sintaxis: `background-image: url(PATH)`

## 7.03 Repeat
Sintaxis: `background-repeat: value`

Posibles valores:
- repeat (por defecto)
- no-repeat
- repeat-x
- repeat-y

## 7.04 clip
Indica que parte de la caja es cubierta por el fondo.
Sintaxis: `background-clip: value`

Posibles valores:
- border-box(por defecto)
- padding-box
- content-box

## 7.05 origin
Indica desde parte caja se comienza a dibujar el fondo.
Sintaxis: `background-origin: value`

Posibles valores:
- border-box(por defecto)
- padding-box
- content-box

## 7.06 size
Nosotros podemos modificar el tamaño a mostrar de una imagen con ccs. La sintaxis de esta propiedad es: `background-size: value`

Posibles valores:
- widht=height (un solo valor puede ser en px o %)
- widht height (dos valores pueden  ser en px o %)
- content (ajusta la imagen para que se muestre completa lo mas grande posible)
- cover (ajusta la imagen para que se muestre en el 100% de la caja, sin deformar la imagen)
- auto (esta es la opcion por defecto, muestra la imagen en su tamaño origina)

## 7.07 position
Esta propiedad es utilizada para especificar desde que coordenada se dibujara la imagen(la coordenadad [0,0] es igual a [left,right]). Sintaxis: `background-position: value`

Posibles valores:
- x (y se pone automaticamente, Puede ser en px o %)
- x y (Puede ser en px o %)
- left | center | right <unit> top | center | bottom <unit>

## 7.08 attachment
Esta propiedad nos permite  espeficicar la manera de mantener una imagen en el fondo.
Sintaxis: `background-attachment: value`

Posibles valores:
- scroll (por defecto)
- fixed
- local

## 7.09 multiples
Es pusible tener multiples fondos en una sola caja. Para manipular las propiedades de cada imagen las dividimos a traves de comas(,) comenzando por la url. Ejemplo:
```css
body {
    background-image: url(PATH_image1), url(PATH_image2), url(PATH_image3);
    background-size: 10%, 50 px, content;
}
```

## 7.10 shorthand
la sintaxis del shorthand es la siguiente:
`background: image position / size repeat attachment origin clip`

Los valores pueden ir en cualquier posicion menos las propiedades **position / size** estas si deben ir en este orden especifico. Position seguido del size separaados por un /.

# 8 Textos

## 8.1 Unidades
### 8.1.1 em
Es el tamaño de fuente del contexto(es variable depende del padre)
**NOTA:** Si el padre es el body, em=rem.

### 8.1.2 rem
Es el tamaño de fuente del root(es ctte depende del html)

## 8.2 Alineacion
### 8.2.1 Direction
Nos permite cambiar la direccion del texto. Su sintaxis es la siguiente: `direction: value;`.

Sus posibles valores son:
- ltr (left to right)
- rtl (right to left)

### 8.2.2 Indent
Nos Permite modificar la indentacion de la primera linea de un texto.

Sintaxis: `text-indent: value;`

Valores en *px* y *relativos*(em o rem).

### 8.2.3 Align
Indica la alineacion del texto.

Sintaxis: `text-align: value`

Posibles Valores:
- start (tiene que ver con direccion)
- end (tiene que ver con la direccion)
- left
- center
- right
- justify (se considera mala practica. Se ve feo en algunas pantallas)

**NOTA:** Exite una propiedad que es *text-align-last* que es para justificar la ultima linea.

### 8.2.4 Line-height
Indica la altura de linea.

Sintaxis:`line-height: value`

Los valores pueden ser relativos(em [no hace falta colocar la unidad]) o cttes(px)

### 8.2.5 Alineacion vertical
Sintaxis: `vertical-align: value`

Posibles valores:
- baseline (por defecto)
- top
- middle
- bottom

## 8.3 Flujo del Texto
### 8.3.1 Letter spacing(Espaciado entre letras)
Sintaxis: `letter-spacing: Value`

El valor es relativo o ctte. Positivo o negativo
### 8.3.2 Word spacing(Espaciado entre palabras)
Sintaxis: `word-spacing: Value`

El valor es relativo o ctte. Positivo o negativo

## 8.4 Decoration
Nos permita dibujar lineas en el texto
### 8.4.1 line
Nos indica el donde se ubicara la linea. Su sintaxis es:
`text-decoration-line: value`

Posibles valores:
- underline
- overline
- line-through
- none

### 8.4.2 color
Nos indica el color de la inea a dibujar. Sintaxis:
`tect-decoration-color: value`

### 8.4.3 style
Nos indica el estilo de la linea(igual que en border). Sintaxis:
`text-decoration-style: value`

Posibes valores:
- none.
- hidden.
- solid.
- dotted.
- dashed.
- double.
- groove.
- ridge.
- inset.
- outset.

### 8.4.4 shorthand
Al igual que muschas propiedades en css existe un shorthand para decoration. Su sitaxis es: `text-decoration: value_line value_style value_color`

**NOTA:** pueden asignarse varios valores de linea(arria, abajo, tachado)

## 8.5 shadow

Ee muy simlar al shadow de las border. Sintaxis: `text-shadow: h-offset v-offset blur color`.

## 8.6 Espacios en blanco
Esta propiedad trata del espacio en blanco cuanto tipiamos el en el codigo. nos permite o no escapar los espacios en blanco y los saltos de linea.

Sintaxis: `white-space: value`

Posibles valores:
- normal (escapa saltos de linea y espacio en blanco)
- pre (no escapa nada)
- nowrap (escapa solo los espacios en blanco)
- pre-wrap (salta de linea y conserva espacios)
- pre-line(salta de linea y no conserva espacios)

## 8.7 Desbordamiento
Es util cuando los textos se 'desbordan' de las caja que los contiene

### 8.7.1 break
Divide la palabra y manda el resto a la siguiente linea. Sintaxis `wrop-break: value`

Posibles valores:
- normal
- break-all
- keep-all
### 8.7.2 wrap
Manda la palabra a la siguiente linea, sino cabe la pica. Sintaxis `wrop-wrap: value`

Posibles valores:
- normal
- break-word
### 8.7.3 overflow
Nos sirve para indicar que el texto continua pero no cabe en la caja(colocando 3 puntos). Sintaxis 
```css
div {
    overflow: hidden; // todo lo que se escapa de la caja se oculta
    text-overflow: ellipsis;
}
```

Posibles valores:
- normal
- break-word

## 8.8 Transformacion
Esta propiedad no sirve para pasar imprimir el texto en mayusculas o minusculas. Sintaxis: `text-transform: value`

Posibles valores:
- uppercase
- lowercase
- capitalize

## 8.9 Fuentes
### 8.9.1 Font-family
**Familias de fuentes genericas**
Las principales familias de fuentes son:

1. **serif**
2. **sans-serif**
3. **monospace**
4. **display**
5. **cursive**

Sintaxis: `font-family: option1, option2, option3, familia_generica;`

### 8.9.2 Tamaño
Sintaxis: `font-size: value;`

Posibles valores:
- porcentaje
- pixeles
- em
- rem
### 8.9.3 Grosor del trazo
Sintaxis `font-weight: value`

Posibles valores:
- bold
- normal
- lighter
- bolder

**NOTA:** No es recomendable utilizar las palabras como valores. Lo recomentado es utilizar multiplos de 100 comprendidos entre 100 y 900

# 9 Pseudoclases
Estilos especiales dependiendo del conexto, posicion o estado.

En su sintaxis vemos el nombre del elemento seguido por dos puntos (:) y luego el nombre de la seudoclase. Ejemplo: `article:hover {...}`
Algunas seudoclases son:

## 9.1 root
Es una seudoclase que es equivalente al nodo *html* es decir, es el nodo principal. Es muy parecido al selector *html*, execto que su nivel de especificidad es mayor. Sirve para declarar variables CSS.

## 9.2 hover
Se presenta cuando el usuario coloca el puntero sobre algun elemento, pero no necesariamente esta activo. En pantallas touch *:hover* es problematico.

## 9.3 active
Esta cubre el caso en el que un elemento esta siendo activado por el usuario. Cuando se interactua con el raton. Corresponde al momento en el que el usuario presiona el raton hasta el momento en que lo suelta. A menudo es usado en los elementos <a> y <button> de HTML.
El **orden** si **importa** al momento de declarar las siguientes Pseudo-clases:
1. :link{ ... }
2. :visited { ... }
3. :hover { ... }
4. active { ... }

## 9.4 target
Representa un elemento unico, si existe alguno.
El id del elemento debe conincidir con el identificador de fragmentos de la URI del documento(href="#idOfElement")

## 9.5 child
Hay 3 tipos de hijos y estos hacen referencia al enesimo, al primero y al ultimo respectivamente:

### 9.5.1 nth-child()
Selecciona al elemento indicado que sea el n-esimo hijo de su elemento padre.

**NOTA:** Si el atributo es (3n). los estilos indicados seran aplicados cada 3 hijos. Si es (odd) Sera aplicado a los elementos pares. Si es (even) Sera aplicado a los elementos impares.
### 9.5.2 first-child
Selecciona al elemento indicado que sea el primer hijo de su elemento padre
### 9.5.3 last-child
Selecciona al elemento indicado que sea el ultimo hijo de su elemento padre

## 9.5 of type
Hay 3 tipos de, funcionan muy similar a las pseudoclases hijas y estos hacen referencia al enesimo, al primero y al ultimo respectivamente:

Puedes visualizar mejor las diferencias en [esta web](https://css-tricks.com/examples/nth-child-tester/)

### 9.5.1 nth-of-type()
Selecciona al elemento indicado que sea el n-esimo hijo de su elemento padre y del mismo tipo al elemento indicado.

**NOTA:** Si el atributo es (3n). los estilos indicados seran aplicados cada 3 hijos. Si es (odd) Sera aplicado a los elementos pares. Si es (even) Sera aplicado a los elementos impares.
### 9.5.2 first-child
Selecciona al elemento indicado que sea el primer hijo de su elemento padre y del mismo tipo al elemento indicado.
### 9.5.3 last-child
Selecciona al elemento indicado que sea el ultimo hijo de su elemento padre y del mismo tipo al elemento indicado.

## 9.6 not
La pseudo-clase de negacion, es una notacion funcional que toma un selector simple X como argumento. Coincide con un elemento que no esta representado por el argumento. X no debe contener otro selector de negacion. 
Es dicer, le aplicara los estilos a todos los elementos menos a los que se les espeficique con la pseudo-clase :not.

## 9.7 empty
Corresponde a un elemento sin ningun nodo hijo. Solo cuando hay nodos de elementos o texto con uno o mas caracteres dectro del elemento ese se convierte en no vacio. 