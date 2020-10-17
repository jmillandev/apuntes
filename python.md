# ¿Qué es Python?
Python es un lenguaje de programación creado por [Guido Van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum), con una sintaxis muy limpia, ideado para enseñar a la gente a programar bien. Se trata de un lenguaje interpretado o de script.

## Ventajas
* Legible: sintaxis intuitiva y estricta.
* Productivo: ahorra mucho código.
* Portable: para todo sistema operativo.
* Recargado: viene con muchas librerías por defecto.

Editor recomendado: Atom o Sublime Text.

## Instalación
Existen dos versiones de Python que tienen gran uso actualmente, Python 2.x y Python 3.x.

Es **recomentado utilizar la versión 3.x** dado a que la versión 2.x dejara de tener soporte a partir del 2019.

Para instalar Python solo debes seguir los pasos dependiendo del sistema operativo que tengas instalado.

### Windows
Para instalar Python en Windows ve al [sitio](URL "https://www.python.org/downloads/") y presiona sobre el botón Download Python 3.7.3

Se descargará un archivo de instalación con el nombre python-3.7.3.exe , ejecútalo. Y sigue los pasos de instalación.

Al finalizar la instalación haz lo siguiente para corroborar una instalación correcta

Presiona las teclas ***Windows + R*** para abrir la ventana de Ejecutar.
Una vez abierta la ventana Ejecutar escribe el comando cmd y presiona ***ctrl+shift+enter*** para ejecutar una línea de comandos con permisos de administrador.
Windows te preguntará si quieres abrir el Procesador de comandos de Windows con permisos de administrador, presiona sí.
En la línea de comandos escribe ***python***
Tu consola se mostrará así.
![captura de pantalla win cmd](URL "./img/python/win.jpg")

¡Ya estás listo para continuar con el curso!

### MacOS

La forma sencilla es tener instalado [homebrew](URL "https://brew.sh/") y usar el comando:

**Para instalar la Versión 2.7**

`brew install python`

**Para instalar la Versión 3.x**

`brew install python3`

### Linux

Generalmente Linux ya lo trae instalado, para comprobarlo puedes ejecutar en la terminal el comando

**Versión 2.7**

`python -v`

**Versión 3.x**

`python3 -v`

Si el comando arroja un error quiere decir que no lo tienes instalado, en ese caso los pasos para instalarlo cambian un poco de acuerdo con la distribución de linux que estés usando. Generalmente el gestor de paquetes de la distribución de Linux tiene el paquete de Python

**Si eres usuario de Ubuntu o Debian por ejemplo puedes usar este comando para instalar la versión 3.1:**

 `$ sudo apt-get install python3.1`

**Si eres usuario de Red Hat o Centos por ejemplo puedes usar este comando para instalar python**

 `$ sudo yum install python`

Si usas otra distribución o no has podido instalar python en tu sistema Linux dejame un comentario y vemos tu caso específico.

Si eres usuario habitual de linux también puedes [descargar los archivos](URL "https://www.python.org/downloads/source/") para instalarlo manualmente.

## Antes de empezar:

Para usar Python debemos tener un editor de texto abierto y una terminal o cmd (línea de comandos en Windows) como administrador.

Para ejecutar Python abre la terminal y escribimos:

 `python`

Te abrirá una consola de Python, lo notarás porque el *prompt* cambia y ahora te muestra tres simbolos de mayor que “ >>> “ y el puntero adelante indicando que puedes empezar a ingresar comandos de python.

 `>>>`

En éste modo puedes usar todos los comandos de Python o escribir código directamente.

*Si deseas ejecutar código de un archivo sólo debes guardarlo con extension.py y luego ejecutar en la terminal:

 `$ python archivo.py`

Ten en cuenta que para ejecutar el archivo con extensión “.py” debes estar ubicado en el directorio donde tienes guardado el archivo.

**Para salir de Python** y regresar a la terminal debes usar el comando `exit()`

Cuando usamos Python debemos atender ciertas reglas de la comunidad para definir su estructura. Las encuentras en el libro [PEP8](URL "https://www.python.org/dev/peps/pep-0008/").

# Consola

## Interaccion

* **Output**: print('Hello world')

* **Input**: var = input('message of input')

## Main
Cada ves que ejecutamos un script esta presente la variable **__name__**, esta retornara el nombre del modulo en el caso de que este se importado desde otro script. Y retornara el valor '__main__' en el caso de que nos encontremos en el modulo que fue ejecutados desde la CLI. Es decir, Cuando ejecutamos un script desde la terminal, la variable **__name__** obtiene el valor de "__main__". De esta manera cuando deseemos ejecutar un codigo SOLO si el modulo es ejecutado(no importado). Lo estructuraremos de la siguiente manera:

 ```python
 # Todas las funciones y codigo necesario para el programa.

 if __name__ == '__main__':
     #esto es lo que se ejecutara en el programa por defecto, algo asi como el index en la web.
 ```

# Sintaxis y Nomenclaura


## Indentacion
 a diferencia de otros lenguajes de programacion no se utilizan {} para escribir un bloque de codigo. Los bloque de codigo son tabulados con una sangria de 4 

## Comentarios

### Lineal
 para comentar una linea utilizamos el caracter '#'.
 Ej:
 `#Esto es un comentario`

## Buenas Practicas

### Entre linea
Dejar dos lineas de espacio entre declaracion de funciones

### Variables

* Son escritas en "snake-case".
 Ej:
  `my_var = 5`

* Visibilidad
En python *todas* las variables son visibles, aunque existe una sintaxis para diferencias, las variables, publicas, privadas y mega privada(estas jamas deben tocarse, de modificarse pueden comprometer el usu del software).

 **public**: `my_var`

 **private**: `_my_var_private`

 **do_not_touch**: `__my_var_special`

### Constantes 
 Se escriben en UpperCase.
 Ej:
 `PI = 3.14`

# Operadores

## Matematicos

* **+**: Suma.
* **-**: Resta.
* **/**: Division.
* **//**: Division entera.
* **%**: Modulo o residuo.
* **\***: Multiplicacion.
* **\*\***: Potencia.


## Asignacion

Son utilizados para hacer asignaciones a las variables:

* **=**: Asignar. Ej: 
```python
 >>> a = 10
 >>> a
 10
```
* **+=**: Sumar y asignar. Ej:
```python
 >>> a = 10
 >>> a += 5
 >>> a
 15
``` 
* **-=**: Restar y asignar. Ej:
```python
 >>> a = 10
 >>> a -= 5
 >>> a
 5 
```
* **/=**: Dividir y asignar. Ej:
 ```python
 >>> a = 10
 >>> a /= 3
 >>> a
 3.333 
 ```
* **//=**: Division Entera y asignar. Ej:

 ```python
 >>> a = 10
 >>> a //= 3
 >>> a
 3
 ```

* **%=**: Modulo y asignar. Ej:
 ```python
 >>> a = 10
 >>> a %= 3
 >>> a
 1
 ```
* **\*=**: Multiplicar y asignar. Ej:
 ```python
 >>> a = 10
 >>> a *= 3
 >>> a
 30
 ```
* **\*\*=**: Sacar potencia y asignar. Ej:
 ```python
 >>> a = 2
 >>> a **= 8
 >>> a
 256
 ```
* **or**: si el valor a la izquierda es (nulo, falso o vacio) asigna el valor a la derecha. Ej: 

```python
 >>> a = False
 >>> b = a or 50
 >>> b
 50 
```
## Comparacion

Nos sirven para comparar valores:

* **==**: Igual.
* **!=**: Distinto.
* **>**: Mayor que.
* **<**: Menor que.
* **>=**: Mayor o igual que.
* **<=**: Menor o igual que.

## Logicos

Junto con los operadores de comparacion nos sirver para hacer preguntas logicas.

* **and**: Y.
* **or**: O.
* **not**: No o Negacion.


# Tipos de datos en Python

1. **Enteros (int)**: en este grupo están todos los números, enteros y *long*:

 *ejemplo*: 1, 2121, 2192, -123

2. **Flotantes (float)**: en este grupo están todos los números con coma flotante o decimales:

 *ejemplo*: 1.0,  -12.3

3. **Booleanos (bool)**: Son los valores *falso* o *verdadero*, compatibles con todas las operaciones booleanas ( and, not, or ):
 *ejemplo*: True, False

4. **Cadenas (str)**: Son una cadena de texto :
 *ejemplos*: “Hola”, “¿Cómo estas?”

5. **Listas**: Son un grupo o array de datos, puede contener cualquiera de los datos anteriores:
 *ejemplos*: [1,2,3, ”hola” , [1,2,3] ], [1,“Hola”,True ]

6. **Diccionarios**: Son un grupo de datos que se acceden a partir de una *clave*:
 *ejemplo*: {“clave”:”valor”}, {“nombre”:”Fernando”}

7. **Tuplas**: también son un grupo de datos igual que una lista con la diferencia que una tupla después de creada no se puede modificar(Son inmutables).
 *ejemplos*: [1,2,3, ”hola” , [1,2,3] ], [1,“Hola”,True ] ***(Pero jamás podremos cambiar los elementos dentro de esa Tupla)***

En Python trabajas con **módulos** y **ficheros** que usas para importar las librerías.


# Funciones
En el contexto de la programación, una función es una secuencia enunciados (statements) con un nombre que realizan un cómputo. Una función tiene un nombre, parámetros (opcional) y valor de regreso(return value)(opcional).

Las funciones las defines con **def** junto a un nombre y unos paréntesis que reciben los parámetros a usar. Terminas con dos puntos.

`def nombre_de_la_función(parametros):`

Después por indentación colocas los datos que se ejecutarán desde la función:

```python
 >>> def my_first_function():
 ...	return “Hello World!” 
 ...    
 >>> my_first_function()
Hello World!
```

Python incluye varias built-in functions en su librería estándar(recuerda que puedes utilizar la funcion "**help(func)**" para examinar el comportamiento de dicha function o visitar el [sitio web oficial](URL "https://docs.python.org/3/library/functions.html") :

## Built-in funtions (Funciones integradas)
1. abs()
2. delattr()
3. hash()
4. memoryview()
5. set()
6. all()
7. dict()
8. help()
9. min()
10. setattr()
11. any()
12. dir()
13. hex()
14. next()
15. slice()
16. ascii()
17. divmod()
18. id()
19. object()
20. sorted()
21. bin()
22. enumerate()
23. input()
24. oct()
25. staticmethod()
26. bool()
27. eval()
28. int()
29. open()
30. str()
31. breakpoint()
32. exec()
33. isinstance()
34. ord()
35. sum()
36. bytearray()
37. filter()
38. issubclass()
39. pow()
40. super()
41. bytes()
42. float()
43. iter()
44. print()
45. tuple()
46. callable()
47. format()
48. len()
49. property()
50. type()
51. chr()
52. frozenset()
53. list()
54. range()
55. vars()
56. classmethod()
57. getattr()
58. locals()
59. repr()
60. zip()
61. compile()
62. globals()
63. map()
64. reversed()
65. __import__()
66. complex()
67. hasattr()
68. max()
69. round()

# Constantes
 Las constantes en **python** en realidad son variables con un nomenclatura distinta(ver la seccion de **Sintaxis y Nomenclatura**).

# Variables

Las variables, a diferencia de los demás lenguajes de programación, no debes definirlas, ni tampoco su tipo de dato, ya que al momento de iterarlas se identificará su tipo. Recuerda que en Python todo es un objeto.

```python
 A = 3 
 B = A
```

## Cadenas
Los String son declaradas entre comillas simples('') o doble(""). Son inmutables.

### Metodos

* **upper()**: Convierte todo a mayusculas.
* **lower()**: Convierte todo la cadena a minusculas.
* **find('patron')**: Encuentra el indice con empieza el 'patron' que definimos, retorna un entero.
* **startswich('patron')**: Que empieza con 'patron', retorna un booleano.
* **endtswich('patron')**: Que termina con 'patron', retorna un booleano.
* **capitalize()**: Regresa la cadena con el primer caracter en mayusculas y el resto en minusculas.

* **slice**: regresa una "rebanada" de la cadena, la sintaxis es:

`var[inicio:fin:pasos]`

## Estructuras de Datos

### Listas
Las listas las declaras con corchetes. Estas pueden tener una lista dentro o cualquier tipo de dato.
```python
 >>> L = [22, True, ”una lista”, [1, 2]]
 >>> L_none = list() 
 >>> L[0] 
 22
``` 
#### Metodos

* **L.append(elemento)**: agrega un elemento a lista.
* **L.pop(uid)**: retorna el elemento con el id = uid y lo elimina de la lista, por defecto uid es el del ultimo elemento.
* **L.sort**: Ordena la lista.

* **remove**: Si sabes qué elemento quieres eliminar, pero no su índice, puedes utilizar este metodo.
* **del lista\[elemento]**: Para eliminar elementos. También lo podemos utilizar con slices. 
* **sorted()**:

### Diccionarios
En los diccionarios tienes un grupo de datos con un formato:
la primera es una **cadena o número** que  será la clave para acceder al segundo dato, el segundo dato será el **valor** al cual accederás con la llave. Recuerda que los diccionarios son listas de llave:valor.

*Los diccionarios se inicializan con {} o con la función dict*

```python
 >>> D = {"Kill Bill": "Tamarino", "Amelie": "Jean-Pierre Jeunet"} 
 >>> D["Kill Bill"]
 "Tamarino"
 ```
#### Metodos

#### Iterables

* **D.keys()**: genera un elemento iterable a traves de las llaves o keys
* **D.values()**: genera un elemento iterable a traves de los valores del diccionario.
* **D.items()**: genera un elemento iterable a traves de las claves : valores del diccionario.

### Tuplas
Las tuplas son similares a las listas. Estas se declaran con paréntesis, recuerda que no puedes editar los datos de una tupla después de que la has creado pues son inmutables.
```python
 >>> T = (22, True, "una tupla", (1, 2))
 >>> T_none = tuple() 
 >>> T[0] 
 22
``` 

### Set o Conjuntos
Los conjuntos son elementos sin orden y no permiten elementos repetidos.
```python
 >>> S = set()
 >>> s.add(5)
 {5}
```
#### Metodos
 * **add**: para agregar un nuevo elemento al conjunto.
 * **remove**: para eliminar un elemento del conjuntos. 



# Conversiones

* De flotante a entero:

```python
 >>> int(4.3)
 4
```

* De entero a flotante:

```python
 >>> float(4) 
 4.0
```
 
* De entero a string:

```python
 >>> str(4.3) 
 "4.3"
``` 

* De tupla a lista:

```python
 >>> list((4, 5, 2)) 
 [4, 5, 2]
```

# Operadores Comunes

## Longitud de una cadena, lista, tupla, etc.:

```python
 >>> len("key") 
 3
```

## Tipo de dato:

```python
 >>> type(4) 
 < type int >
```
 
## Aplicar una conversión a un conjunto como una lista:

```python
 >>> map(str, [1, 2, 3, 4])
 ['1', '2', '3', '4']
```
 
## Redondear un flotante con x número de decimales:

```python
>>> round(6.3243, 1)
 6.3
```
 
## Generar un rango en una lista (esto es mágico):

```python
 >>> range(5) 
 [0, 1, 2, 3, 4]
```
 
## Sumar un conjunto:

```python
 >>> sum([1, 2, 4]) 
 7
```

## Organizar un conjunto:

```python
 >>> sorted([5, 2, 1]) 
 [1, 2, 5]
```

## Operadores de Pertenencia:
Se utilizan para verificar si un valor esta dentro de un iterable, retornan un booleano:

* in
* not in

## Conocer los comandos que le puedes aplicar a x tipo de datos:

```python
 >>>Li = [5, 2, 1]
 >>>dir(Li)
 >>>['append', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

*‘append’, ‘count’, ‘extend’, ‘index’, ‘insert’, ‘pop’, ‘remove’, ‘reverse’, ‘sort’* son posibles comandos que puedes aplicar a una lista.

## Información sobre una función o librería:

```python
 >>> help(sorted) 
 (Aparecerá la documentación de la función sorted)
``` 

#Clases

Clases es uno de los conceptos con más definiciones en la programación, pero en resumen sólo son la representación de un objeto. Para definir la clase usas ***class*** y el nombre. En caso de tener parámetros los pones entre paréntesis.

Para crear un constructor haces una función dentro de la clase con el nombre ***__init__*** y de parámetros self (significa su clase misma), nombre_r y edad_r:

```python
 >>> class Estudiante(object): 
 ... 	def __init__(self,nombre_r,edad_r): 
 ... 		self.nombre = nombre_r 
 ... 		self.edad = edad_r 
 ...
 ... 	def hola(self): 
 ... 		return "Mi nombre es %s y tengo %i" % (self.nombre, self.edad) 
 ... 
 >>> e = Estudiante(“Arturo”, 21) 
 >>> print (e.hola())
 Mi nombre es Arturo y tengo 21
``` 

Lo que hicimos en las dos últimas líneas fue:

1. En la variable llamamos la clase Estudiante y le pasamos la cadena “Arturo” y el entero 21.

2. Imprimimos la función hola() dentro de la variable e (a la que anteriormente habíamos pasado la clase).

Y por eso se imprime la cadena “Mi nombre es Arturo y tengo 21”

# Métodos especiales

## cmp(self,otro)
Método llamado cuando utilizas los operadores de comparación para comprobar si tu objeto es menor, mayor o igual al objeto pasado como parámetro.

## len(self)
Método llamado para comprobar la longitud del objeto. Lo usas, por ejemplo, cuando llamas la función len(obj) sobre nuestro código. Como es de suponer el método te debe devolver la longitud del objeto.

## init(self,otro)
Es un constructor de nuestra clase, es decir, es un “método especial” que se llama automáticamente cuando creas un objeto.

# Iterators and generators

## Iterators

Un iterator es simplemente un objeto que cumple con los requisitos del Iteration Protocol (protocolo de iteración) y por lo tanto puede ser utilizado en ciclos. Por ejemplo,

```python
for i in range(10):
    print(i)
```
En este caso, la función range es un iterable que regresa un nuevo valor en cada ciclo. Para crear un objeto que sea un iterable, y por lo tanto, implemente el protocolo de iteración, debemos hacer tres cosas:

1. Crear una clase que implemente los métodos **iter** y **next**.

2. **iter** debe regresar el objeto sobre el cual se iterará.
3. **next** debe regresar el siguiente valor y *aventar la excepción StopIteration* cuando ya no hayan elementos sobre los cual iterar.

## Generators

Los generators son simplemente una forma rápida de crear iterables sin la necesidad de declarar una clase que implemente el protocolo de iteración. Para crear un generator simplemente declaramos una función y utilizamos el keyword **yield** en vez de return para regresar el siguiente valor en una iteración. Por ejemplo,

Los generadores pueden ser muy aparecidos a las listas. Una de las diferencias es que los generadores ocupan menos espacio en memoria, ya que van "llamando" un elemento a su vez.

```python
def fibonacci(max):
    a, b = 0, 1
    while a < max:
        yield a
        a, b = b, a+b
```

***Es importante*** recalcar que una vez que se ha agotado un generator ya no podemos utilizarlo y debemos crear una nueva instancia. Por ejemplo,

```python
fib1 = fibonacci(20)
fib_nums = [num for num in fib1]
...
double_fib_nums = [num * 2 for num in fib1] # no va a funcionar
double_fib_nums = [num * 2 for num in fibonacci(30)] # sí funciona
```

### Yield From

Una caracteristica de los generadores en python poco conocida/utilizada son los `yield from` Estos nos permiten "insertar" generadores dentro de otro.

```python
def frutas():
    for fruta in ('manzana','pera','limon','patilla'):
	yield fruta

def comestibles():
    for comestible in ('pan','arepa','tamal',pasta'):
	yield comestible

    yield from frutas()

    yield 'arroz'

list(comestible())
# ['pan','arepa','tamal',pasta','manzana','pera','limon','patilla','arroz']
```

# Comprehensions

Son constructos que nos permiten generar secuencias a partir de otras secuencias. Existen 3 tipos:

* List Comprehension

**[** element_to_add **for** element **in** element_list **if** element_meets_condition **]**

* Dictionary Comprehension

**{** key_to_element:element_to_add **for** element **in** element_list **if** element_meets_condition **}**

* Set Comprehension

**{** element_to_add **for** element **in** element_list **if** element_meets_condition **}**

# Condicionales IF
Los condicionales tienen la siguiente estructura. Ten en cuenta que lo que contiene los paréntesis es la comparación que debe cumplir para que los elementos se cumplan.

```python
 if ( a > b ):
 	elementos 
 elif ( a == b ): 
 	elementos 
 else:
 	elementos
```
	 
# Bucles

## FOR
El bucle de for lo puedes usar de la siguiente forma: recorres una cadena o lista a la cual va a tomar el elemento en cuestión con la siguiente estructura:

```python
 for i in ____:
 	elementos
```
	 
Ejemplo:

```python
 for i in range(10):
 	print i
```

En este caso recorrerá una lista de diez elementos, es decir el `print i` debe ejecutarse diez veces. Ahora i va a tomar cada valor de la lista, entonces este for imprimirá los números del 0 al 9 (recordar que en un range vas hasta el número puesto -1).

## WHILE
En este caso while tiene una condición que determina hasta cuándo se ejecutará. O sea que dejará de ejecutarse en el momento en que la condición deje de ser cierta. La estructura de un while es la siguiente:

```python
 while (condición):
 	elementos
```

Ejemplo:

```python
 >>> x = 0 
 >>> while x < 10: 
 ... 	print x 
 ... 	x += 1
```
 
En este ejemplo preguntará si es menor que diez. Dado que es menor imprimirá x y luego sumará una unidad a x. Luego x es 1 y como sigue siendo menor a diez se seguirá ejecutando, y así sucesivamente hasta que x llegue a ser mayor o igual a 10.

## Operadores
 * **continue**: se usa para saltarse los *statements* restantes y pasar a la siguiente iteracion.

 * **break**: se sale del bucle.

# Manipulacion de Archivos
La función **open** nos permite leer archivos

`f = open(‘some_file’)`

**Es importante** siempre cerrar el archivo con la función **close** para que se
escriban los datos y no se desperdicie memoria.

`f.close()``

Una mejor manera de manipular archivos  y una buena practica es utilizando context managers,
porque garantizan que el archivo se cierre, Ej.

```python
with open(filename) as f:
# do something with the file
```
## Modos para abrir un archivo

Existen varios modos de abrir un archivo. Los más importantes son r (read),
w (write), a (append).

```python
with open(filename, mode=’w’) as f:
# do something with the file
```

## CSV

El modulo **csv** nos permite manipular archivos con extension *.csv*.

Para utilizarlo lo importamos con la declarcion:

`import csv``

Existen dos **Reader** y dos **Writer** que viene con el modulo que nos seran muy utilies.

1. **csv.Reander and csv.Writer**:
Nos permite manipular los valores a traves de listas que representan filas.

2. **csv.DictReader and cdv.DictWriter**:
Nos permite manipular los valores a traves de diccionarios que representan filas.

# Decoradores
Los decoradores permiten extender y modificar el funcionamiento de las
funciones. Estas envuelven a otra función y permiten ejecutar código antes y
después de que es llamada
Ejemplo de definicion de un decorador:

```python
def lower_case(func):
	def wrapper():
		# execute code before
		result = func()
		# execute code after
		return result
	
	return wrapper
```
**Importante**, la funcion donde vayamos a ejecutar el decorador debera estar predecedida por la llamada a el decorador ejemplo:

```python
@lower_case()
def my_function (arg)
	pass
```

**Nota**: Cuando declaramos la function aux wraper es comun pasarle como parametros (*arg,**kwargs). Ejemplo:

```python
def lower_case(func):
	def wrapper(*arg,**kwargs):
		# execute code before
		result = func(*arg,**kwargs)
		# execute code after
		return result
	
	return wrapper
```

# OOP (Object Oriented Programming)

La programación orientada a objetos es un paradigma de programación que
otorga los medios para estructurar programas de tal manera que las
propiedades y comportamientos estén envueltos en objetos individuales. En pocas palabras, es un enfoque que nos permite modelar objetos concretos, del mundo real y las relaciones entre ellos

**Principios básicos de OOP**:
* Encapsulation
* Abstraction
* Inheritance
* Polyphormism

Todos los objetos son una instancia de una clase

Ejemplo:

```python
class Airplane:
	def __init__(self, passengers, seats, pilots=[]):
		self.passengers = passengers
		self.seats = seats
		self._pilots = pilots
	def takeoff(self):
		pass


airplane = Airplane(passengers=20, seats=30, pilots=['Tom', 'Billy'])
airplane.passengers = 31
airplane.takeoff()
```

El metodo **__init__** es el constructur de la clase. El metodo constructor es aque que se ejecuta al crear una nueva instancia de la clase.

El parametro **self** es pasado como primer parametro en *TODOS* los metodos de las clases, este representa a la clase misma.

# Collections (Colecciones)

El módulo collections nos brinda un conjunto de objetos primitivos que nos permiten **extender** el comportamiento de las **built-in** collections que poseé Python y nos otorga estructuras de datos adicionales. 
Por ejemplo, 
* Si queremos extender el comportamiento de un diccionario, podemos extender la clase *UserDict*.
* Si queremos extender de una lista, extendemos *UserList*.
* Para el caso de strings, utilizamos *UserString*.

Por ejemplo, si queremos tener el comportamiento de un diccionario podemos escribir el siguiente código:

```python
class SecretDict(collections.UserDict):

   def _password_is_valid(self, password):
        …

    def _get_item(self, key):
        … 

    def __getitem__(self, key):
         password, key = key.split(‘:’)
         
         if self._password_is_valid(password):
              return self._get_item(key)
         
         return None

my_secret_dict = SecretDict(...)
my_secret_dict[‘some_password:some_key’] # si el password es válido, regresa el valor
```

Otra estructura de datos que vale la pena analizar, es **namedtuple**. Usualmente utilizamos tuples que permiten acceder a sus valores a través de índices. Sin embargo, en ocasiones es importante poder nombrar elementos (en vez de utilizar posiciones) para acceder a valores y no queremos crear una clase ya que únicamente necesitamos un contenedor de valores y no comportamiento.

```python
Coffee = collections.NamedTuple(‘Coffee’, (‘size’, ‘bean’, ‘price’))
def get_coffee(coffee_type):
     If coffee_type == ‘houseblend’:
         return Coffee(‘large’, ‘premium’, 10)
```

El módulo collections también nos ofrece otros primitivos que tienen la labor de facilitarnos la creación y manipulación de colecciones en Python. Por ejemplo,

**Counter**: nos permite contar de manera eficiente ocurrencias en cualquier iterable. **OrderedDict**: nos permite crear diccionarios que poseen un orden explícito.
**deque** nos permite crear filas (para pilas podemos utilizar la lista).

***En conclusión***, el módulo collections es una gran fuente de utilerías que nos permiten escribir código más “pythonico” y más eficiente.

# Modulos
Si sales del intérprete de Python y entrás de nuevo, las definiciones que hiciste (funciones y variables) se pierden. Por lo tanto, si querés escribir un programa más o menos largo. Es mejor crear un script que el interprete luego ejecutara.

A medida que el progama va creciendo es comun ir separandolo en varios archivos para hacerlo mas practico y facil a la hora de mantenerlo.

Para soportar esto, Python tiene una manera de poner *definiciones* en un archivo y usarlos en un script o en una instancia interactiva del intérprete. Tal archivo es llamado **módulo**; las definiciones de un módulo pueden ser *importadas* a otros módulos o al módulo principal (la colección de variables a las que tienes acceso en un script ejecutadolo en el nivel superior y en el modo calculadora).

El *nombre del archivo es el nombre del módulo* con el sufijo `.py` agregado. Dentro de un módulo, el nombre del mismo (como una cadena) está disponible en el valor de la variable global __name__.

Para utilizar cualquier modulo deberemos importarlo con la siguiente linea de codigo(puede ser directamente desde la consola o en un script):

`import model_name`

Una vez importado el modulo para hacer referencia a las funciones, objetos, variables definidos en dicho modulo deberemos hacer referencia de la siguiente manera:

```python
model_name.variable_name
model_name.function_name
model_name.class_name
```

Si requerimos solamente el uso de ciertos metodos, del modulo podriamos importar exclusivamente esa definicion de la siguiente manera:

```python
from model_name import function

hola = funtion()
```

# Librerias Externas
Son codigos de 3eros que nos facilitan el trabajo al no "reinvertar la rueda"
Alguanas librerias son:

## OS

El modulo **OS** nos sera de mucha utilidad en la manupulacion de archivos ya que nos permite manipular el sistema operativo.

alguno de sus metodos son:

* os.remove('name_file'): Nos permite borrar un archivo del disco duro.

* os.rename('old_name_fiel','new_name_file').

## openpyxl
Esta libreria nos permite la manipulacion de archivos en formato xls (hojas de calculo).
 
 Codigo de interes:
1. Lectura de archivos: 
```python
from openpyxl import load_workbook

FILE_PATH = 'test.xlsx'
SHEET = 'Hoja 1'

workbook = load_workbook(FILE_PATH, read_only = True)
sheet = workbook[SHEET]


for row in sheetiter_rows(min_row=2)
    print(row[0].value)
    print(row[1].value)
    print(row[2].value)
```
***NOTA:*** El atributo min_row no es obligatorio, este indica a partir de cual fila comenzara al iteracion, para el ejemplo es la segunda fila. Por defecto es la primera

# Scopes and NameSpace

En Python, un **name**, también conocido como **identifier**, es simplemente una forma de otorgarle un nombre a un objeto. Mediante el nombre, podemos acceder al objeto. Vamos a ver un ejemplo:

```python
my_var = 5

id(my_var) # 4561204416
id(5) # 4561204416
```

En este caso, el **identifier** my_var es simplemente una forma de acceder a un objeto en memoria (en este caso el espacio identificado por el número 4561204416). Es importante recordar que un name puede referirse a cualquier tipo de objeto (incluso a funciones).

```python
def echo(value):
    return value

a = echo

a(‘Billy’) # 3
```
## Namespace (espacio de nombres)

Para ponerlo en palabras llanas, un namespace es simplemente un conjunto de names.

En Python, te puedes imaginar que existe una relación que liga a los nombres definidos con sus respectivos objetos (como un diccionario). Pueden coexistir varios namespaces en un momento dado, pero se encuentran completamente aislados. Por ejemplo, existe un namespace específico que agrupa todas las variables globales (por eso puedes utilizar varias funciones sin tener que importar los módulos correspondientes) y cada vez que declaramos una módulo o una función, dicho módulo o función tiene asignado otro namespace.

A pesar de existir una multiplicidad de namespaces, no siempre tenemos acceso a todos ellos desde un punto específico en nuestro programa. Es aquí donde el concepto de scope (campo de aplicación o alcance) entra en juego.

## Scope (alcance)

Es la parte del programa en el que podemos tener acceso a un namespace sin necesidad de prefijos.

En cualquier momento determinado, el programa tiene acceso a tres scopes:

* El scope dentro de una función (que tiene nombres locales)
* El scope del módulo (que tiene nombres globales)
* El scope raíz (que tiene los built-in names)

Cuando se solicita un objeto, Python busca primero el nombre en el scope local, luego en el global, y por último, en el raíz. Cuando anidamos una función dentro de otra función, su scope también queda anidado dentro del scope de la función padre.

```python
def outer_function(some_local_name):
    def inner_function(other_local_name):
         # Tiene acceso a la built-in function print y al nombre local some_local_name
         print(some_local_name) 
        
         # También tiene acceso a su scope local
         print(other_local_name)
```

Para poder manipular una variable que se encuentra fuera del scope local podemos utilizar los keywords global y nonlocal.

```python
some_var_in_other_scope = 10

def some_function():
     global some_var_in_other_scope
     
     Some_var_in_other_scope += 1
```

# Errors (Errores)

Un programa de Python termina en cuanto encuentra un error. Es diferente a un error de sintaxis(pues en el error de sintaxis el codigo no llega a compilar).

Por lo tanto es una buena practicar que manejemos los posibles errores que puedan llegar a suceder en nuestro codigo. Esto lo hacemos "aventando" excepciones o errores.

Para “aventar” un error utilizamos el keyword raise.
Ej.

```python
def divide(numerator, denominator):

If denominator == 0:
raise ZeroDivisionError
```

También podemos generar nuestros propios error, si extendemos *BaseException*
Ej.

`class TakeOffError(BaseException)`

Si queremos evitar que termine el programa y tenemos una estrategia para responder al error podemos utilizar los keyword **try** / **except**
Ej.
```python
try:
	airplane.takeoff()
except TakeOffError as error:
	airplane.land()
```
El esqueleto de una estructura **try** es:

```python
try:
	#run this code
except
	#execute this code when there is an exception
else:
	#no exception? run this code
finally:
	#allways run this code			
```
Si desea conoces mas acerca de los errores y como manejarlos visita el [web site oficial](URL "https://docs.python.org/3/tutorial/errors.html")

# Context Managers

Son objetos de Python que proveen información contextual adicional al bloque de código. Esta información consiste en correr una función (o cualquier callable) cuando se inicia el contexto con el keyword with; al igual que correr otra función cuando el código dentro del bloque with concluye. Por ejemplo:

```python
with open(‘some_file.txt’) as f:
    lines = f.readlines()
```
	
Si estás familiarizado con este patrón, sabes que llamar la función open de esta manera, garantiza que el archivo se cierre con posterioridad. Esto disminuye la cantidad de información que el programador debe manejar directamente y facilita la lectura del código.

Existen dos formas de *implementar* un context manager:

* Con una clase.
* Con un generador.

Vamos a implementar la funcionalidad anterior para ilustrar el punto:

```python
class CustomOpen(object):
    def __init__(self, filename):
        self.file = open(filename)

    def __enter__(self):
        return self.file

    def __exit__(self, ctx_type, ctx_value, ctx_traceback):
        self.file.close()

with CustomOpen('file') as f:
    contents = f.read()
```

Esta es simplemente una clase de Python con **dos métodos** adicionales: ***enter y exit***. Estos métodos son utilizados por el keyword with para determinar las acciones de inicialización, entrada y salida del contexto.

El mismo código puede implementarse utilizando el módulo **contextlib** que forma parte de la librería estándar de Python.

```python
from contextlib import contextmanager

@contextmanager
def custom_open(filename):
    f = open(filename)
    try:
        yield f
    finally:
        f.close()

with custom_open('file') as f:
    contents = f.read()
```
	
El código anterior funciona exactamente igual que cuando lo escribimos con una clase. La diferencia es que el código se ejecuta al inicializarse el contexto y retorna el control cuando el keyword yield regresa un valor. Una vez que termina el bloque with, el context manager toma de nueva cuenta el control y ejecuta el código de limpieza.

# PyPi (Python Package Index)
Es un repositorio de paquetes de 3º. Para instalar un nuevo paquete es necesario utilizar la herramienta **PIP** ejecutando el comando:

`Pip install package_name`

Tambien se puede agrupar la instalacion de varios paquetes en requerements.txt(como una especia de receta, como el DockerFile.yml de docker o el composer.json de PHP) de la siguiente manera:

```
Package_name_1 == Version
Package_name_2 == Version
Package_name_3 == Version
```
Para la instalacion de pip descarga el siguiente [script](URL "https://bootstrap.pypa.io/get-pip.py"), y ejecutalo. Para mayor informacion puedes visitar el [web site oficial](URL "https://pypi.org/project/pip/") de pip

# Ambientes Virtuales
Son como una especie de "contenedores" en los cuales podemos trabajar sin interactuar con el interprete global de python.

Es una buena pracitca crear ambientes virtuales para cada proyecto de python en el que estamos trabajando. Esto nos evitara posibles conflictos en paquetes.

los pasos para crear un ambiente virtual son :

1. Tener instalado virtualenv: 
Esto lo realizamos con **pip** desde nuestro interprete global.
`pip install virtualenv`

2. crear el entorno virtual:
`virtualenv venv`

3. Activar el entorno virtual:
`source venv/bin/active`

Para desactivar el entorno virtual solo utilizamos:
`desactive`

# PEPs (Python Enhancement Proposals)
Describen cambios al lenguaje o a los estándares alrededor

Pueden ser de tres tipos:
* **Standards**: Describen un nuevo feature o comportamiento.

* **Informational**: Describen un problema de diseño, una guía general, o información
para la comunidad.

* **Process**: Describen un proceso relacionado con Python, pero no al código
fuente de Python.
Ej. cambios en los procesos de toma de decisiones

**PEPs**

* **PEP8**: Python style guide.
* **PEP257**: Python docstrings.
* **PEP20**: import this.

https://www.python.org/dev/peps/

# Unit Testing

## Doctest
Las pruebas unitarias son un conjunto de pruebas que le ofrecen a nuestra aplicacion ser mas robusta.

En el stack de python viene incluido el modulo de doctest. Este nos permitira realizar pruebas unitarias de una manera muy sencilla. Para ello en un archivo tipeamos nuestras operaciones de la siguiente manera:
```python
>>> 2 + 2
4

>>> 3*3 != 10
True
```

Suponiendo que el archivo se llama *test.txt* lo ejecutamos de la siguiente manera: `python3 -m doctest test.txt`. De esta manera ejecutamos las pruebas en nestro archivo.

Tambien podemos realizar nuestros tests directamente en el DocString de nuestras funciones o metodos.

```python
"""
from functools import lru_cache

@lru_cache()
def fibonacci(number):
    """
    Retorn el numero n de la serie de fibonacci dado un n number
        >>> fibonacci(5)
        5

        >>> fibonacci(11)
        89

    """
    if number <= 1:
        return number, number
    return (fibonacci(number-1)[0] + fibonacci(number-2)[0]), number
if __name__ == '__main__':
    fibonacci(200)
    print('Informacion del cache: ', fibonacci.cache_info())
    # Para limpiar la cache en caso de que lo deseemos aplicamos el metodo fibonacci.cache_clear()
```
Para testearlo aplicamos el mismo comando. `python3 -m doctest fibonacci.py`

Podemos realizar tarea bastante complejas y que requieran varias instrucciones. Para ellos nos podemos apoyar de un fichero como el del primer ejemplo.

## Asserts
Este es un feature de python que nos permite validar y testear nuestro codigo de una manera sencilla. Aca, evaluaremos una expresion y siempre que esta nos retorne False se le vantara una Exception de tipo AssertionError. Ejemplo:

```python
assert True
assert False, 'Este es el mensaje de la Exception'
AssertionError: Este es el mensaje de la Exception
```

## Otros

Adicionalmente existe la libreria [pytest](https://docs.pytest.org/en/latest) y el framework [unittest](https://docs.python.org/3/library/unittest.html). Se recomienda la utlizacion del segundo, ya que es mas robusto.

## Covertura
La covertura es utilizada para ver que porcentaje de nuestro codigo se esta ejecutando, con nuestras Pruebas unitarias. Si se esta ejecutando el 100%. Esto indica que nuestro codigo no deberia tener fallas(Logicamente si paso todos los test).

Para realizar esto nos vamos a apoyar de la libreria [coverage](https://coverage.readthedocs.io/en/coverage-5.0.4/)

Una vez intalada. Ejecutamos las siguiente lineas de codigo
```zsh
coverage run test.py #Suponiendo que el fichero test.py se encuentran nuestras pruebas unitarias de nuestro script.py

coverage report -m script.py #Esto nos mostrara un reporte con: Lineas totales, Lineas no ejecutadas, Porcentaje de lineas no ejecutadas, Numero de las lineas que no fueron ejecutas.

coverage html script.py # Esto nos  creara un reporte en un archivo html
```
PD: Los reportes creados en archivos html deben observarse desde un servidor web. El comando `python3 -m http.server` nos ayudara con esto.

# Manejo de imagenes
Una libreria muy conocida en python para el manejo de imagenes es [PIL](https://pypi.org/project/Pillow/)

# Cómo seguir

Python tiene muchas aplicaciones:

En las ciencias tiene muchas librerías que puedes utilizar como analisis de las estrellas y astrofisica; si te interesa la medicina puedes utilizar **Tomopy** para analizar tomografías. También están las librerías más fuertes para la ciencia de datos **numpy, Pandas y Matplotlib**

En **CLI** por si te gusta trabajar en la nube y con datacenters, para sincronizar miles de computadoras:

* aws
* gocloud
* rebound
* geeknote

**Aplicaciones Web**:

* Django
* Flask
* Bottle
* Chalice
* Webapp2
* Gunicorn
* Tornado

# ZEN de Python

Beautiful is better than ugly.  
Explicit is better than implicit.  
Simple is better than complex.  
Complex is better than complicated.  
Flat is better than nested.  
Sparse is better than dense.  
Readability counts.  
Special cases aren't special enough to break the rules.  
Although practicality beats purity.  
Errors should never pass silently.  
Unless explicitly silenced.  
In the face of ambiguity, refuse the temptation to guess.  
There should be one-- and preferably only one --obvious way to do it.  
Although that way may not be obvious at first unless you're Dutch.  
Now is better than never.  
Although never is often better than *right* now.  
If the implementation is hard to explain, it's a bad idea.  
If the implementation is easy to explain, it may be a good idea.  
Namespaces are one honking great idea -- let's do more of those!  
