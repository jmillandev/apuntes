---
title: "Golang - Go"
slug: "golang"
description: "🐹"
keywords: [programacion, desarrollo, software, go, golang]
draft: false
tags: []
math: false
toc: false
---
# Caracteristicas pricipales

* Performant
* Núcleos-multiples
* Concurrente
* Compilado
* Tipado estatico
* Network
* Sintaxis Limpia
* Biblioteca estándar muy poderosa
* Limpieza automatica de memoria(garbage collected)
* Portable(compila en múltiple OS's)
* Es apoyado por Google
* Open Source

# Usos mas frecuente del lenguaje

* Web apps
* Servidores de Redes
* Machine learning
* Procesamiento de imagenes
* Balanceadores de carga
* Adminitracion de sistemas
* Hardware
* Scripts
* Criptografía
* Mobile Apps(Algunas veces)

# Estructura basica de un programa en go

* El paquete *main* es el paquete principal, este contine a la funcion *main*

* la funcion *main* es el punto entrada y de cierre del programa(Cuando esta finaliza, el progama finaliza)

``` golang
package main // Declaracion del paquete que estamos creando

import (

        // Aca importamos todos los paquetes que utlizaremos en nuestro programa

)

func main() (

        // Acá va el codigo de nuestro programa

)
```

# Operadores

## Asignación y declaracion

La palabra *var* es un *keyword* que podemos utilizar para declarar una nueva variable en nuestro codigo siguienndo la siguietne estructura:

``` golang
// var identificador tipo. Ejemplo:
var x int
// Si deseamos declarar e inicializar una variable en la misma sentencai. Haremos:
var x int = 50
```

**NOTA:** Por defecto si declaramos una variable y no le asignamos ninguna valor esta contendra el valor cero correspondinete a su tipo. Estos valores se muestran en la siguiente tabla

| tipo          | valor cero    |
| ---           | ---           |
| booleans      | false         |
| integers      | 0             |
| floats        | 0.0           |
| strings       | ""            |
| pointers      | nil           |
| functions     | nil           |
| interfaces    | nil           |
| slices        | nil           |
| channels      | nil           |
| maps          | nil           |

En go cuando declaramos una variable debemos expresar explicitamente el tipo de dato que almacenara esta variable, en caso de que no le indiquemos el tipo de dato, debemos utilizar el operador de **declaracion corta** *:=* siguiendo la siguiente estructura:

``` golang
// identificador := 50
x := 50
```

**NOTA:** Mantener las variables en es scope mas reducido posible e utilizar el operador corto tanto com se aposible

## Asignacion

El operador de asignacion sigue la siguiente estructura `identificador = valor` . Ejemplo:

``` golang
var x int
x = 50
```

# Tipos de datos

## Creando tipos
Si necesitamos crear un nuevo tipo seguimos la siguiente estructura:
```golang
type dinero int

// Declaramos una nueva variable con el tipo que creamos
var new_pay dinero
```