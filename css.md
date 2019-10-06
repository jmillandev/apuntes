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