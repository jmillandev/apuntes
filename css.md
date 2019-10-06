# 1.0 Fundamentos

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

# 2.0 Selectores
Se dividen esencialmente en 3 tipos:

1. Sencillos.
2. Compuestos.

## 2.1 Sencillos
Son selectores de un solo elemento. Existen varios:

- **Selector de elemento o tipo:** Es el mas sencillo de todos que es basicamente el nombre de una etiqueta HTML o XML. Ejemplo:

`body { ... }`

*NOTA:* **NO** es recomendado modificar estos estilos a menos que estes muy claro de lo que estas haciendo.


- **Selectores de clases:** Son los mas recomentados y utiles al momento de escribir los estilos de un proyecto. Se escribe anteponiendo el nombre de la clases por un punto(.). Ejemplo:

`.nameClass { ... }`

- **Selectores de ID:**Se escribe anteponiendo el nombre de la clases por un  hash(#). Ejemplo:

`#nameID { ... }`

*NOTA:* Su uso no es para nada recomendado en css

- **Selector universal** : Se denota con el caracter *. Como su nombre lo indica le aplica los estilos a todos los elementos. Ejemplo:

`* { ... }`

**IMPORTANTE:** *NO* utilices este selector a menos que estes muy claro(pero extremadamente claro) de lo que estas haciendo y tienes ya tienes un nivel elevado en CSS. **Puede ocasionar bugs**.

## 2.2 Compuestos
Estos a su vez se dividen en varios tipos. Es importante aclarar que el nombre oficial no es 'selectores compuestos' este nombre es unicamente para objetivos didacticos.

1. **Selectores agrupados:** Nos permiten asignar estilos a varios selectores en un mismo bloque de codigo. Esto lo hacemos separando los selectores con comas(,). Ejemplo:
```CSS
/* El siguiete codigo coloca un fondo color rojo para los elementos de las clase
'nameClass1', el elemento de ID 'nameID' y los parrafos. */

.nameClass1,
#nameID,
p {
    background: red;
}
```

2. **Selectores desendientes:** Nos permiten asignar estilos a un elemento que sea *desendiente* (hijo, nieto, etc) de otro elemento. Esto lo hacemos dejando un escio en blanco(' ') entre los selectores. Ejemplo:

```css
/* El siguiente codgio le coloca un fondo blanco a los parrafos que sean hijo de la clase dashboard-dark*/

.dashboard-dark p {
    background: white;
}
```

**IMPORTANTE:** esta debe ser una de las *ULTIMAS* opciones que utilicemos. Esto nos puede traer o ocasionar bugs.

*NOTA:* Debes tener cuidado de dejar el espacio en blanco entre los selectores, de no ser asi estas indicando que quieres seleccionar un elemento que cumple con TODAS las caracteristicas descritas(para el caso del ejemplo anterior, un parrafo que pertenece a la clase dashboard-dark).