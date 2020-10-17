---
title: "CSS - Response Desing"
slug: "css-response-desing"
description: "👨‍🎨"
keywords: [programacion, desarrollo, software, css, frontend, response desing]
draft: false
tags: []
math: false
toc: false
---
# 1 Conceptos de RWD
## 1.1 Viewport
Es toda la parte visible de nuestro navegador que podemos utilizar para mostral nuestra pagina(NO incluye al scroll).

Este es la base del response web design. es una etiqueta meta de *HTML* creada por apple en 2007. Si no esta declarado el viewport en la base del *HTML* no funcionara nada del response web design.

**NOTA:***La resolucion del hardware* de una pantalla y la *resolucion del viewport* en el navegador de la misma no son iguales. **La resolucion de la pantalla >= a la resolucion del viewport**

### 1.1.1 Sintaxis:
```html
<meta name="viewport" content="">
```
### 1.1.2 Contenidos
Son separados por coma:
- width=device-width
- user-scalable = no | yes (Permitir al usuario hacer zoom o no). La buena practica es tenerlo habilitado.
- initial-scale =1
- maximum-scale=2

## 1.2 Media queries
Como su nombre lo indica es una consulta de impresion, referente al medio donde impriremo el contenido(puede ser un dispositivo movil, portatiles, hoja impresa, etc).

puedes ver mas info [aca](https://developer.mozilla.org/es/docs/CSS/Media_queries)

Sintaxis:
`@media type_of_media [and queries]`

Tipos de medios:
- screen
- print

Consultas:
- min-width, maz-width
- orientation: landscape, portrait 
- min-aspect-ratio, max-aspect-ratio, device-aspect-ratio

## 1.3 Metodologias
Existen al menos 3 tipos:

- Mobile first (Es la mas utilizada)
- Desktop first
- Content first (Los expertos en UX lo recomiendan)

# 2 Unidades
## 2.1 Unidades relaticas
1. **Porcentajes(%)**: Hace referencia al tamaño del padre
2. **1em** = Hace referencias al 100% del tamaño de fuente del contexto. 
3. **1rem** = Hace referencias al 100% del tamaño de fuente del root (<\html>). Ideal para crear el layout.

# 2.2 Unidades del viewport
1. **1vw** = 1% del ancho del viewport.
2. **1vh** = 1% del alto del viewport.
3. **1vmin** = 1% del lado menor del viewport.
4. **1vmax** = 1% del lado mayor del viewport.

# 3 Multimedia
# 3.1 Video
Lo podemos hacer a traves de posicion y un padding-bottom. Estableciendole al contenedor padre un `position: relative;` y al video un `position:absolute; width:100%; height:100%;`.

# 3.2 Imagenes
`img {width:100%; height:auto; max-width:numero}`.

En esta caso es ideal utilizar la etiqueta HTML [<picture>](https://developer.mozilla.org/es/docs/Web/HTML/Elemento/picture) para mostrar distintasa imagenes dependiendo de la pantalla. Esto nos optimiza la carga para dispositivos mas pequeños

Otra opcion tambien es utilizar el atributo *srcset* de la etiqueta <img>. Ejemplo:
```html5
<img
    srcset="img1.png tamaño1w, img2.png tamaño2w, img3.png 800w"
    src="default.png"
    alt="imagenes adaptativas"
/>
```

# 4 JavaScript para rwd

## 4.1 CSSOM (CSS Object Model)
A traves del metodo `window.getComputedStyle(element)` donde *element* es un elemento del DOM. Esta funcion nos devuelve un objeto para la **lectura** de sus estilos. 

NOTA: Para leer las la propiedad *property* utilizamoes `object.getPropertyValue('property')`.

NOTA2: Este objeto que es retornado tiene los estilos computados por el navegador.

## 4.2 style
Todo elemento del DOM tiene una propiedad *style* donde podemos inspeccionar sus valores y modificar los mismos.

## 4.3 cambiar clase
Algunas veces requerimos hacer varias modificaciones en un elemento las forma mas recomendada de hacer es cambiarndo su clase o añadiendo una nueva. Esto lo podemos hacer a traves de los metodos de la propiedad **classList** del elemento del DOM al que vamos a manipuar.

## 4.4 template
Podemos reasignar estilo desde js declarando un template-string en una varialbe que luego sera asignada a atributo *style* desde el *setAttribute* del elemento

# 4.5 mediaQuery
Esto lo hacemos con ayuda de la funcion `mactMedia('mediaQueryCss')`. Esta funcion nos devuelve un objeto con el atributo *matches*, esta propiedad nos retorna un valor true o false.