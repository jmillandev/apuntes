---
title: "Buenas practicas en programación"
slug: "buenas-practicas"
description: "👍"
keywords: [programacion, desarrollo, software, buenas practicas]
draft: false
tags: []
math: false
toc: false
---
# ¿A quién beneficia contar con código bien escrito?
El código bien escrito beneficia a todos los involucrados en el proyecto.

* **A tí**: Cuando retomemos un proyecto después de un largo tiempo nos beneficiará ya que sabremos cómo está ordenado y cómo está escrito todo.
* **A cualquiera**: Cualquier persona que deba modificar el código después de tí.
* **A tu cliente**: Aunque nunca lo sabrá, su negocio estará mejor atendido.

# Elementos dotan de calidad al código:

* [Legibilidad](#legibilidad): qué tan fácil es interpretar lo que el código dice.
* [Mantenibilidad](#mantenibilidad): cuánto esfuerzo supondrá adaptar el código a nuevos requerimientos.
* Testeabilidad: cuánto esfuerzo supondrá realizar pruebas sobre este código.

<a name="legibilidad"></a>

## Legibilidad

El código fuente lo escribimos para personas como tú y yo, para las computadoras tenemos las versiones compiladas.

Debemos seguir un estándar de codificación, el cual nos ayuda a:

* Generar código claro y consistente.
* Evitar perder tiempo en decisiones triviales.

### Acoplate a un estandar

 Un estandar de codificacion es una seria de reglas que indica como debes escribir el codigo. Como por ejemplo ¿Donde deben inicar las lleves de un bloque de codigo?, ¿ cuantas lineas de separacion hay entre los bloques?, ¿Cual es la sintaxis para la creacion de variables?, etc.

1. **Define un estándar:**Piénsalo una vez y déjalo por escrito.

**NOTA:** Puede ser el del lenguaje que se esta manejando, normalmente esta documentado en la web del lenguaje de programacion.

2. **Respétalo:** Haz un esfuerzo por adherirte al estándar durante tu día a día.

3. **Apóyate en algún linter:** Esta sencilla herramienta te ayudará a incorporar buenas prácticas.

### Identificadores: mnemotécnicos, específicos y precisos

Los identificadores son variables, funciones, clases, módulos, componentes, etc. Elementos a los que nosotros debamos crearles un nombre propio.

Ejemplo sin un identificador mnemotécnico una función se vería así:

``` php
function f( int $b, int $a ) : float {
        return ( $b * $a ) / 2;
}
```

Al leer este código no sabemos para qué funciona y hasta podríamos borrarlo por equivocación.

Ahora utilizando un identificador mnemotécnico se vería así:

``` php
function areaTriangulo( int $base, int $altura ) : float {
        return ( $base * $altura ) / 2;
}
```

Ahora gracias a que el código es más legible sabemos para qué funciona esta función.

Atención a los identificadores que estableces: Un buen indicador es pedirle a alquien que trabaje contigo que lea el codigo y que te diga que hace.

<a name="mantenibilidad"></a>

## Mantenibilidad

### Código modular

El código modular son pedazos de códigos divididos(normalmente en funciones) que pueden ser utilizados en cualquier lugar para evitar tener un solo archivo con un bloque de código gigante.

Bloques de codigo potenciales para modularizar:

* Aquellos que estan dentro de un bucle.
* Los que estan dentro de un condicional.
* Codigo que realice calculos o metodos complejos.
* Codigo que se repita/realice con frecuencia.

### Codigo reutilizable

Escribir código reutilizable nos va a ayudar a que en lugar de copiar y pegar una misma línea de código pero con diferentes parámetros lo hagamos a través de una función que retorne los valores que necesitamos y luego la podremos llamar en cualquier lugar del código que necesitemos pasándole los parámetros que deseamos.

### Código organizado

El código organizado se refiere a cómo tenemos distribuido nuestros archivos en la raíz (root) del proyecto. A mayor organización, mayor entendimiento del código. 
Usualmente lo que haremos es agrupar los archivos que tengan contenido similar en directorios que tengan sentido. Ejemplo:

Convencion de distribucion de archivos en PHP moderno:

``` 
/public
/src
/tests
/vendor    
```

**Directorios**

* **public**: Contiene todos los documentos que son accesibles desde afuera del servidor.
* **src**: Contiene todos los archivos propios de nuestro codigo fuente(nuestro proyecto).
* **test**: Pruebas a realizar.
* **vendor**: dependencias/librerias de terceros.

# Libre de vicios

## Evitar el hardcoding

El hardcoding es la práctica de escribir *valores literales* en lugar de *identificadores*. **NO debe de usarse**, ya que si el día de mañana debemos cambiar los valores eso significa que debemos cambiar el código en los lugares que esté ese valor estático por completo y luego mandar a producción, cuándo podríamos hacer el cambio más orgánico en una variable que afecte a todos los lugares que es llamada. Para esto utilizamos variables de configuracion o variables de entorno, es decir variables que son exernas al codigo fuente de nuestro programa.

## Evitar efectos colaterales

Los efectos colaterales en este caso son aquellos que suceden mas alla del codigo que se esta leyendo. Debemos analizar muy bien nuestro código para evitar efectos colaterales y evitar que nuestro código deje de funcionar.
**Consejos:**

* **No** uses variables globales.

# Principios SOLID

**SOLID** son cinco principios básicos de la programación orientada a objetos que ayudan a crear software mantenible en el tiempo.

**SOLID** significa:

* [S](#single): Single Reponsibility Principle.
* [O](#open): Open/Closed Principle. 
* [L](#liskov): Liskov Substitution Principle. 
* [I](#interface): Interface Segregation Principle. 
* [D](#dependency): Dependency Inversion Principle. 

<a name="ingle"></a>

## Single Reponsibility Principle

A class should have one and only one reason to change. Meaning that a class should have only one job.

En español:
Una clase que debe tener sólo una razón para cambiar. Es decir, que cada clase debe tener una UNICA responsabilidad.

Veamos un Ejemplo:

``` java
package main;

public class Rectangulo {
    private float base;
    private float altura;

    public Rectangulo(float base, float altura) {
        this.setBase(base);
        this.setAltura(altura);
    }

    public float getBase() {
        return this.base;
    }

    public void setBase(float base) {
        this.base = base;
    }

    public float getAltura() {
        return this.altura;
    }

    public void setAltura(float altura) {
        this.altura = altura;
    }
    
    public String toString() {
        return "Base " + this.base + ", Altura " + this.altura;
    }

    public float area() {
        return this.base * this.altura;
    }

    // Este metodo No cumple con el principio de responsabilidad unica
    public void imprimir() {
        System.out.println(this);
    }

}
```

En el ejemplo anterio, a excepción del metodo 'imprimir', toda la clase cumple con el principio de responsabilidad unica. Debido a que sus metodos estan fuertemente relacionado(tienen una alta cohesión), donde la pregunta principal podria ser: ¿que se tiene que mostrar?.

Pero si nos centramos en el metodo 'imprimir', este se podria decir que pertenece a otra capa en la logica. La capa de presentación(donde la pregunta seria ¿como mostrar la información?), ya que si en un futuro, queremos mostrar el contenido de esta clase en un formato Json en un servicio WEB, no deberiamos modificar la clase. Entoces, aplicando el principio de responsabilidad unica creariamos otra clase que se veria asi:

``` java
package main;

public class Presentacion {
    public void imprimir(Rectangulo rectangulo) {
        System.out.println(restantgulo);
    }

    public void area(Rectangulo rectangulo) {
        System.out.println(restantgulo.area());
    }
}
```

<a name="open"></a>

## Open/Closed Principle

Objects or entities should be open for extension, but closed for modification.

En español:
Establece que una entidad de software debe quedarse abierta para su extensión, pero cerrada para su modificación.

Es decir, las entidades, clases, metodos deben quedar abierta al posibilidad de extension, de esta forma la clase puede adaptarse a nuevos ecenarios sin la necesidad de modificar o añadir codigo. Este principio suele resolverse delegando las funcionalidades( usualmente mediante la herencia y/o interfaces).

Ejemplo:

**Violacion_O/C**: Aqui vemos como la funcion valida el tipo de documento que se desea procesar, de esta manera seria imposible agregar un nuevo estilo de documento sin modificar el archivo

``` php
<?php

class DocProcessor
{
        public function process( array $docs )
        {
                foreach ( $docs as $doc ) {
                        if ( $doc instanceof Invoice ) {
                                $doc->sendToClient();
                        } elseif ( $doc instanceof Receipt ) {
                                $doc->archive();
                        } elseif ( $doc instanceof Memo ) {
                                $doc->markAsRead();
                        }
                }
        }
}
```

**O/C_Respetado**: En este cado el metodo se encarga de procesar directamente el archivo, delegando la responsabilidad de validar el archivo a otra clase.

``` php
<?php

class DocProcessor
{
        public function process( array $docs )
        {
                foreach ( $docs as $doc ) {
                        $doc->process(); 
                }
        }
}
```

Otro ejemplo:
Volamos un instante con el codigo de ejemplo en [Open/Closed Principle](#open) y regresemos aca.
Supongamos que creamos otra clase llamado Triangulo, que hace algo muy similar a la clase Rectangulo, esta calcula el area de dicha figura.

Pero, ¿que pasa si ahora queremos imprimir el area del triangulo?. Deberiamos hacer algo asi en la clase 'Presentación'

``` java
package main;

public class Presentacion {
    public void imprimir(Rectangulo rectangulo) {
        System.out.println(rectantgulo);
    }

    public void area(Rectangulo rectangulo) {
        System.out.println(rectantgulo.area());
    }

    public void imprimir(Triangulo triangulo) {
        System.out.println(triangulo);
    }

    public void area(Triangulo triangulo) {
        System.out.println(triangulo.area());
    }

}
```

Este codigo funciona perfectamente, pero supone una violación al princio O/C. Ya qeu tendiramos que crear N*2 metodos por cada n figuras que tengamos. Para solucionar esto podemos crear la siguiente interfaz.

``` java
package main;

public class IFigura {

    float area();

}
```

Luego de aplicar dicha interfaz a nuestras dos clases(Triangulo y Rectangulo). Podriamos hacer un refactor a nuestra clase 'Presentacion' y quedaria así:

``` java
public class Presentacion {
    public void imprimir(IFigura figura) {
        System.out.println(figura);
    }

    public void area(IFigura figura) {
        System.out.println(figura.area());
    }

}
```

De esta forma dejamos nuestro codigo abiarto a la extension pero cerrado a la modificación.

<a name="liskov"></a>

## Liskov Substitution Principle

Let q(x) be a property provable about objects of x of tiye T. Then q(y) should provable for objects y of type S where  S is a subtype of T.

Es decir:
Establece que cada clase que hereda de otra puede usarse como su padre sin necesidad de conocer las diferencias entre ellas. Para que pueda darse este principio debe cumplir con dos puntos:

* El cliente debe usar métodos de la clase padre únicamente.
* La clase hija no debe alterar el comportamiento de los métodos de la clase padre.

**Consejos**
En el caso de que una clase hija requiera modificar el codigo de un metodo de la clase padre, vale la pena preguntarse ¿Estas clases deben estar relacionados hereditariamente?, lo mas seguro es que la respuesta sea no, y mantengan otro tipo de relacion.

<a name="interface"></a>

## Interface Segregation Principle.

Establece que los clientes de un programa cuando implementan una interface sólo deberían conocer de éste los métodos que realmente usan. Es decir, no deben implementar interfaces con metodo que no utilizan en su codigo fuente.

**Consejos**
A client should never be forced to implement an inaterface that it doesn't use or client shouln't be forced to depend on methods they do not use.

En el caso de que tengas un metodo implementando interfaces con metodos que este no utilizara(o seria estupido que los utilizara), debemos "partir" la interfaz en varias interfaces(posiblemente que vayan heredando unas de otras). Tambien recordemos que una misma clase puede implementar varias interfaces.

<a name="dependency"></a>

## Dependency Inversion Principle.

Entities must depend on abstractions not on concretions. It states that the high level madule must not depend on the low level module, but they should depend on abtractions.

Detalla que los módulos de alto nivel no deben depender de los de bajo nivel, ambos deben depender de abstracciones. Es decir, los objetos no deben ser creados dentro de las clases sino pasados como parametro. Y a su vez estos parametros no deben ser de un tipo de clase en especial, sino que deberan depender de un interfaz.

Las abstracciones no deben depender de los detalles, los detalles deben depender de las abstracciones.

Para entender lo antes dicho definamos las clases de alto y bajo nivel:

1. **Clases de alto nivel:**

Son aquellas que tienen que ver con la logica de negocio. Con la aplicacion especifica que se esta desarrollando.

2. *Clases de bajo nivel:*

Son aquellas que existen con el proposito de ayudar a las clases de alto nivel a cumplir su cometido.

# Patrones de Diseño

Los patrones de diseño son soluciones de arquitectura de software aplicables a diferentes problemas. Estos son soluciones conceptuales que se pueden aplicar a la hora de pensar como diseñar las clases.

Basicamente existen 3 tipos:

1. [**Creacionales:**](#creacionales) Nos hablan de como se crean nuevas instancias de los objetos.

Entre ellos encontramos:

* [*Abstract Factory*](#abstract_factory): Provee una interfaz para la creacion de familias de objetos sin espeficicar una clase en concreto.
* [*Builder*](#builder): Separa la construccion de objectos complejos.
* [*Factory Method*](#factory_method): Define un interfaz para la creacion de un objecto pero deja qu la subclase decida que clase instanciar.
* [*Prototype*](#prototype): especifica que tipo de objectos crear usando una instancia prototipo y crea nuevos objecos copiando este prototipo.
* [*Singleton*](#singleton): Nos aseguramos que una clase solo puede ser instanciada una vez, ademas de proveer un punto de acceso a esta.

2. [**Estructurales:**](#estructurales) Nos hablan de como debemos estructurar nuestras clases para crear estructuras flexibles y eficientes.

Entre ellos encontramos:

* [*Adapter*](#adapter): Convierte la interaz de una clase en otro interfaz quee cliente espera.
* [*Bridge*](#bridge): Nos permite desacoplar un a abstracción de su implementacion, de manera que ambas puedan ser modificadas indepedientemente sin necesdad de alterar por ello la otra.
* [*Composite*](#composite): sirve para construir objetos complejos a partir de otros más simples y similares entre sí, gracias a la composición recursiva y a una estructura en forma de árbol.
* [*Decorator*](#decorator): Agrega responsabilidades adicionales a un objeto de forma dinámica.
* [*Facade*](#facade): Nos permite utilizar módulos complejos de una forma sencilla y con bajos costos para el cliente.
* [*Flyweight*](#flyweight): Nos permite eliminar o reducir redundancia cuando trabajamos con una gran cantidad de objetos.
* [*Proxy*](#proxy): Permite controlar el acceso a diferentes áreas de módulos.

3. [**De Comportamiento:**](#comportamiento) Hablan sobre como deben comportarse nuestros objetos. Gestionando algoritmos y responsabilidades entre ellos.

Entre ellos encontramos:

* [*Chain of Responsibility*](#chain_of_responsability): Evita acoplar el emisor de una petición a su receptor dando a más de un objeto la posibilidad de responder a una petición. Para ello, se encadenan los receptores y pasa la petición a través de la cadena hasta que es procesada por algún objeto.
* [*Command*](#command): Permite solicitar una operación a un objeto sin conocer realmente el contenido de esta operación, ni el receptor real de la misma. Para ello se encapsula la petición como un objeto, con lo que además facilita la parametrización de los métodos.
* [*Interpreter*](#interpreter): Dado un idioma, define una representación para su gramática junto con un intérprete que use la representación para interpretar oraciones en el lenguaje.
* [*Iterator*](#iterator): Define una interfaz que declara los métodos necesarios para acceder secuencialmente a un grupo de objetos de una colección.
* [*Mediator*](#mediator): Define un objeto que encapsula cómo un conjunto de objetos interactúan.
* [*Memento*](#memento): Permite almacenar el estado de un objeto (o del sistema completo) en un momento dado de manera que se pueda restaurar en ese punto de manera sencilla. Para ello se mantiene almacenado el estado del objeto para un instante de tiempo en una clase independiente de aquella a la que pertenece el objeto (pero sin romper la encapsulación), de forma que ese recuerdo permita que el objeto sea modificado y pueda volver a su estado anterior.
* [*Observer*](#observer): Define una dependencia del tipo uno a muchos entre objetos, de manera que cuando uno de los objetos cambia su estado, notifica este cambio a todos los dependientes.
* [*State*]: Se utiliza cuando el comportamiento de un objeto cambia dependiendo del estado del mismo.
* [*Template Method*](#template_method): Define el esqueleto de programa de un algoritmo en un método, llamado método de plantilla, el cual difiere algunos pasos a las subclases.
* [*Visitor*](#visitor): Representa una operación que se realiza sobre los elementos que conforman la estructura de un objeto.

***IMPORTANTE:*** Es importante recalcar que los patrones de diseño son para darte una idea de como diseñar tu aplicacion, no son un "copia y pega" pues no siempre son la mejor solucion que se adapta a tu problema en algunas cosos puede ponerte las cosas mas dificiles.

## Creacionales

### Simple Factory

Este metodo perse, no es catalogado como un patron de diseño, sin embargo es necesario hablar de el para comprender mejor patrones como abstract factory o  factory method.

La idea de este, es poder crear objetos complejos de una forma sencilla.

Por Ejemplo:
Supongamos que tenemos la siguiente clase:

``` python
class Pizza:

    def __init__(self, cantidad_rebanadas: int):
        self.cantidad_rebanadas = cantidad_rebanadas

    @property
    def cantidad_rebanadas(self):
        return self.cantidad_rebanadas

    def __str__(self):
        return f"Cantidad de rebanadas: {self.cantidad_rebanadas}"


class Pizzeria:
    """
    Esta Clase nos ayudara con el proceso de crear una nueva pizza,
    por si tenemos que leer algo de la base de datos, Conectarnos con un
    API, o cualquier otro requerimiento en logica del negocio.
    """
    small = 6
    medium = 8
    large = 12

    def create_small_pizza(self):
        return Pizza(self.small)

    def create_medium_pizza(self):
        return Pizza(self.medium)

    def create_large_pizza(self):
        return Pizza(self.large)


if __name__ == "__main__":
# Si no implementamos Simple Factory, la instancia de la clase se veria como:
    pizzaMargarita = Pizza(8)

    print(pizzaMargarita)

# Implementando Simple Factory, la instancia de la clase se veria como:
    pizzeria = Pizzeria()
    pizzaPeperoni = pizzeria.create_medium_pizza()

    print(pizzaPeperoni)
```

### Factory Method
Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

En español:
Define una interfaz para la creación de un objecto, pero deja que la subclase, es decir la clase que implementa la interfaz, decida que clase instanciar.

Esta patron nos permitira mediante una clase generar objectos complejos controlados. La diferencia con el Simple Factory es que aqui necesitaremos de una interfaz para poder crear dichos objectos.

Ejemplo:
``` java
public class Pizza {

	private int cantidadRebanadas;
	private String especialidad;
	
	public Pizza(int cantidadRebanadas, String especialidad) {
		this.cantidadRebanadas = cantidadRebanadas;
		this.especialidad = especialidad;
	}
	
	public String toString() {
		return "Cantidad rebanadas : " + this.cantidadRebanadas + " Especilidad : " + this.especialidad;
	}
	
}


public interface IPizzeria {

	Pizza crearPizza(String tipo);
	
}

public class PizzaOrillaRellena extends Pizza {

	public PizzaOrillaRellena(int cantidadRebanadas, String especialidad) {
		super(cantidadRebanadas, especialidad);
	}
	
}

public class PizzeriaCF implements IPizzeria {

	public Pizza crearPizza(String tipo) {
		
		if (tipo.equals("Peperoni")) {
			return new Pizza(8, "Peperoni");
		}
		
		if (tipo.equals("Hawaiana")) {
			return new Pizza(8, "Hawaiana");
		}
		
		if (tipo.equals("Peperoni orilla rellena")) {
			return new PizzaOrillaRellena(12, "Peperoni"); //
		}
		
		return null;
	}
	
}

public class Main {

	public static void main(String[] args) {
		
		PizzeriaCF cf = new PizzeriaCF();
		
		Pizza peperoni = cf.crearPizza("Peperoni");
		Pizza hawaiana = cf.crearPizza("Hawaiana");
		Pizza orillaRellena = cf.crearPizza("Peperoni orilla rellena");
		
		
		System.out.println(peperoni);
		System.out.println(hawaiana);
		
		System.out.println(orillaRellena);
		
	}

}
```

Como vemos en el ejemplo anterior es la clase *PizzeriaCF* mediando la interfaz *IPizzeria* la encargada de crear la instancia del tipo de Pizza requerida

### Abstract Factory
Provide an interface for creating families of related or dependent objects without specifying their concrete classes.


Una de las principales direfencia entre este patron y el Factory Method, es que acá nuestra intererfaz contendra N cantidad de metodos(Factories) para crear distintos objectos tipo de objectos(Con cierta relación entre si). Ejemplo:

``` java
public interface IAbstractFactory {

	IComputadora crearComputadora();
	
	ITablet crearTablet();
	
}

public interface IComputadora {

}

public interface ITablet {

}



public class MacbookPro implements IComputadora {

}

public class IPad implements ITablet {

}

public class AppleStore implements IAbstractFactory {

	public IComputadora crearComputadora() {
		return new MacbookPro();
	}
	
	public ITablet crearTablet() {
		return new IPad();
	}
	
}


public class QX410 implements IComputadora {

}

public class TabS3 implements ITablet {

}

public class SamsungStore implements IAbstractFactory {

	public IComputadora crearComputadora() {
		return new QX410();
	}
	
	public ITablet crearTablet() {
		return new TabS3();
	}
	
}



public class Main {

	public static void main(String[] args) {
		
		SamsungStore samsung = new SamsungStore();
		AppleStore apple = new AppleStore();
		
		IComputadora mac = apple.crearComputadora();
		ITablet ipad = apple.crearTablet();
		
		IComputadora qx = samsung.crearComputadora();
		ITablet s3 = samsung.crearTablet();
		
	}

}
```

En este caso nuestro AbstractFactory, Es la abtraccion de una tienda electronica, Donde solo espeficicamos los distintos FactoryMethod que alli se crean. Luego la subclase es la encargada de crear los distintos tipo de objectos.

### Singleton 
Ensure a class only has one instance, and provide a global point of access to it.

Permite restringir la creación de objetos pertenecientes a una clase o al valor de un tipo a un único objeto. Dicho de otra manera la idea es tener **una sola instancia** de la clase a lo largo de toda nuestra aplicacion.
Ejemplo:

``` php
class Singleton
{
    private static $theInstance = null;
    public statis function getInstance(){
        if ( self::$theInstance === null ) {
            self::$theInstance = new sefl();
        }
        return self::$theInstance
    }
    privade function __contruct() {
        // code..
    }
}
```

Como acabamos de ver solo puede existir una instancia de esta clase durante la vida de esta aplicacion ya que esta puede ser creada solo desde dentro de ella misma, Y esta configurada para que al crearse por primera vez, no se vuelva a cronstruir.

La creación de este patron la podriamos resumir en los siguiente pasos.
- Hacer privado el metodo constructor de la clase, de esta manera solo desde la clase perse podra se ejecutado dicho metodo.
- Crear un nuevo metodo **estatico** desde donde obtendermos la instancia de nuestra clase.
- Validar desde nuestro nuevo metodo si ya existe o no una instancia creada(generarmente con un atributo privado), Si no existe, se crea y se retorna. Si existe, simplemente se retorna.

Un ejemplo de creacion por el patron Singleton son los *log de errores* de las aplicaciones. Otro ejemplo muy comun, es el acceso a la base de datos.

### Builder
Separate the construction of a complex object from its representation so that the same construction process can create diferent representations.
This provides solution to Telescopic constructors and constructor overload.

Este metodo es muy util a la hora de crear objectos con atributos variables, como puede ser:

``` java

package main;

public class Usuario {
	
	private String nombre;
	private String apellido;
	
	private boolean medioContacto; 
	
	private String email;
	private String telefono;
	private String direccion;
	
    //3. step: All setters modify it so that it returns the class object..
    // only Optional attributes have setters
	public BuilderUsuario setMedioContacto(boolean medioContacto) {
		
		if(!medioContacto) {
			throw new IllegalArgumentException("No es posible asiganar un valor falso a medio de contacto");
		}
		
		this.medioContacto = medioContacto;
		return new BuilderUsuario(this);
	}
    
    // 1 step: Constructor private!	
	private Usuario(String nombre, String apellido) {
		this.nombre = nombre;
		this.apellido = apellido;
		
		this.medioContacto = false;
		
		this.email = "";
		this.telefono = "";
		this.direccion = "";
		
	}
	// 2 step: Generate a public and static method that allows us to return a new class object
	public static Usuario Make(String nombre, String apellido) {
		return new Usuario(nombre, apellido);
	}
	
    // 4 step: Method that returns the final object, the method is instance
	public Usuario Build() {
		return this;
	}
	
	public String toString() {
		return " " + this.nombre + " " + this.apellido + " " + this.email + " " + this.telefono + " " + this.direccion;
	}
	
	
	public static class BuilderUsuario{
		
		private Usuario usuario;
		
		public BuilderUsuario(Usuario usuario) {
			this.usuario = usuario;
		}
		
		public BuilderUsuario setDireccion(String direccion) {
			usuario.direccion = direccion;
			return this;
		}

		public BuilderUsuario setEmail(String email) {
			usuario.email = email;
			return this;
		}

		public BuilderUsuario setTelefono(String telefono) {
			usuario.telefono = telefono;
			return this;
		}
		
		public Usuario Build() {
			return usuario;
		}
	}
	
}

public class Main {

	public static void main(String[] args) {

		Usuario codi = Usuario.Make("Codi", "Facilito")
							.setMedioContacto(false)
							.setDireccion("México").Build();
							
		System.out.println(codi);
	}

}

```

Veamos que hace este codigo:

- El metodo **Make**: crea el objeto mas basico(Este resive los parametros obligatorios).
- El Metodo **Build**: Se encarga simplemente de retornar el objeto perse.
- Setters: Se encargan de setear los valores opcionales y a su vez retornar un objeto. De tal forma que podemos seguir llamando a los metodos del objeto.
- A su ves el setter setMedioContacto retorna un objecto del tipo **BuilderUsuario**, que es el que contiene los setter. Es metodo es totalmente customizado(No pertenece al patron perse). Se creo con la finalidad de que la unica manera de que le podamos seterar; El email, la direccion o el telefono a un usuario es que antes hayamos pasado por este "Setter" *setMedioCotacto*.

Como vimos con este patron podemos ir creando objetos complejos, mediante "partes", de esta manera podemos ir crear objetos con las partes que necesitemos y todo de una manera muy legible.

### Prototype
Specify the kinds of objects to create using a prototypical instance, and createnew objects by copying this prototype.

Es principalmente util cuando debemos crear varias instancias de un objeto pero con ligeras modificaciones. Ejemplo, los fantasmas en Pac-Man.
 Otro caso donde es recomendable utilizar en la creacion de objectos donde uno o varios atributos tienen un costo significando(Como consultar a la DB o a una API).

 Ejemplo en codigo:
 ``` java
 package main;

public class Enemigo {

	private String imagen; 
	private int posX;
	private int posY;
	private int cantidadVida;
	
	public Enemigo(String imagen, int posX, int posY, int cantidadVida) {
		this.setImagen(imagen);
		this.setPosX(posX);
		this.setPosX(posX);
		this.setCantidadVida(cantidadVida);
	}
	
	public Enemigo(Enemigo enemigo) {
		this.setImagen(enemigo.getImagen());
		this.setPosX(enemigo.getPosX());
		this.setPosX(enemigo.getPosY());
		this.setCantidadVida(enemigo.getCantidadVida());
	}
	
	public Enemigo clone() {
		//return new Enemigo(this);
		return new Enemigo(this.imagen, this.posX, this.posY, this.cantidadVida);
	}
	
	public String getImagen() {
		return imagen;
	}
	
	public void setImagen(String imagen) {
		this.imagen = imagen;
	}
	
	public int getPosX() {
		return posX;
	}
	
	public void setPosX(int posX) {
		this.posX = posX;
	}
	
	public int getPosY() {
		return posY;
	}
	
	public void setPosY(int posY) {
		this.posY = posY;
	}
	
	public int getCantidadVida() {
		return cantidadVida;
	}

	public void setCantidadVida(int cantidadVida) {
		this.cantidadVida = cantidadVida;
	}
}

public class Main {

	public static void main(String[] args) {
		
		Enemigo enemigoBase = new Enemigo("Imagen1.png", 0, 100, 2);
		
		Enemigo enemigo1 = new Enemigo(enemigoBase);
		Enemigo enemigo2 = new Enemigo(enemigoBase);
		Enemigo enemigo3 = new Enemigo(enemigoBase);
		
		enemigo1.setPosX(100);
		enemigo2.setPosX(150);
		enemigo3.setPosX(200);
		
		Enemigo enemigoBase2 = new Enemigo("Imagen1.png", 0, 200, 2);
		
		Enemigo enemigo4 = enemigoBase2.clone();
		Enemigo enemigo5 = enemigoBase2.clone();
		Enemigo enemigo6 = enemigoBase2.clone();
		
		enemigo4.setPosX(100);
		enemigo5.setPosX(150);
		enemigo6.setPosX(200);
		
		
	}

}
 ```

## Estructurales

### Adapter
Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.

Ejemplo:
``` java
public interface IConexionSQL {
	
	void conexion();
	
	String runQuery();
	
}

public interface IConexionNoSQL {
	
	void conexion();
	
	String excecuteSentence();
	
}

public class ConexionMySQL implements IConexionSQL {

	public void conexion() {
		System.out.println("Conexión con MYSQL");
	}
	
	public String runQuery() {
		return "Consulta MYSQL";
	}
	
}

public class ConexionMongoDB implements IConexionNoSQL {
	
	public void conexion() {
		System.out.println("Conexión con MongoDB");
	}
	
	public String excecuteSentence() {
		return "Consulta MongoDB";
	}
	
}

public class AdaptadorDB implements IConexionSQL {

	private IConexionNoSQL noSQL;
	
	public AdaptadorDB(IConexionNoSQL noSQL) {
		this.noSQL = noSQL;
	}
	
	public void conexion() {
		this.noSQL.conexion();
	}
	
	public String runQuery() {
		return this.noSQL.excecuteSentence();
	}
}

public class Main {

	public static void main(String[] args) {
		
		IConexionSQL conexion = new ConexionMySQL();
		// IConexionSQL conexion = new AdaptadorDB( new ConexionMongoDB() );
		
		conexion.conexion();
		
		String resultado = conexion.runQuery();
		System.out.println(resultado);

	}

}
```

En el ejemplo podemos ver dos clases **IConexionNoSQL** y **IConexionSQL** que no son compatibles entre si.
Mediante un adaptador podemos hacer que estas clases sean compatibles para el cliente(en este caso la clase *Main*), y de esta manera pasar de usar ConexionMysql a ConexionMongoDB, sin mayores cambios mas alla de una linea de codigo(donde se instancia a la clase reponsable de la conexion).

### Composite
Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

``` java
public interface IMenu {
	
	boolean open();
	
	boolean close();
	
	
}


import java.util.ArrayList;

public class Menu implements IMenu{
	
	private ArrayList<IMenu> menus;
	
	public Menu() {
		this.menus = new ArrayList<IMenu>();
	}
	
	public boolean open() {
		System.out.println("Open!");
		return true;
	}
	
	public boolean close() {
		System.out.println("Close!");
		return true;
	}
	
	public void addMenu(IMenu menu) {
		this.menus.add(menu);
	}
	
	public IMenu getMenu(int pos) {
		return this.menus.get(pos);
	}
	
}

public class Main {

	public static void main(String[] args) {
		Menu menu = new Menu();
		
		Menu menu2 = new Menu();
		Menu menu3 = new Menu();
		
		Menu menu4 = new Menu();
		Menu menu5 = new Menu();
		
		menu3.addMenu(menu4);
		menu3.addMenu(menu5);
		
		menu.addMenu(menu2);
		menu.addMenu(menu3);
		
		menu.open();
		menu.close();

	}

}

```

### Decorador
Attach additional responsibilities to on objects dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

El patrón Decorator responde a la necesidad de añadir dinámicamente funcionalidad a un Objeto. Esto nos permite no tener que crear sucesivas clases que hereden de la primera incorporando la nueva funcionalidad, sino otras que la implementan y se asocian a la primera.

``` java
public interface IPizza {

	String descripcion();
	
	float precio();
}

public class PizzaHawaiana implements IPizza{
	
	public String descripcion() {
		return "Pizza hawaiana";
	}
	
	public float precio() {
		return 8;
	}
	
}

public class PizzaPeperoni implements IPizza {
	
	public String descripcion() {
		return "Pizza de peperoni";
	}
	
	public float precio() {
		return 8;
	}
}

public class OrillaRellena implements IPizza {

	private IPizza pizza;
	
	public OrillaRellena(IPizza pizza) {
		this.pizza = pizza;
	}
	
	public String descripcion() {
		return this.pizza.descripcion() + " con orilla rellena";
	}
	
	public float precio() {
		return this.pizza.precio() + 4;
	}
	
}

public class QuesoExtra implements IPizza {

	private IPizza pizza;
	
	public QuesoExtra(IPizza pizza) {
		this.pizza = pizza;
	}
	
	public String descripcion() {
		return this.pizza.descripcion() + " queso extra";
	}
	
	public float precio() {
		return this.pizza.precio() + 2;
	}
	
}

public class Main {
	
	public static void main(String[] args) {
		
		IPizza pizzaPeperoni = new QuesoExtra(new PizzaPeperoni());
		
		System.out.println(pizzaPeperoni.descripcion());
		System.out.println(pizzaPeperoni.precio());
		
		
		IPizza pizzaHawaiana = new QuesoExtra(new OrillaRellena(new PizzaHawaiana()));
		
		System.out.println(pizzaHawaiana.descripcion());
		System.out.println(pizzaHawaiana.precio());
		
	}

}
```

En el ejemplo pudimos extender nuestro catalogo de pizzas sin editar la herarquia o los tipos de pizza(Peperoni y Hawaiana) ya creadas.

Mediando los Decorators QuesoExtra y OrillaConQueso, pudimos extender las funcionabilidad del negocio. Si necesitaramos añadir mas caracteristicas, bastara con crear mas Decorartor que actuen como Wrapers.

### Facade
Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

Este patron es util. Para exponerle al cliente metodos sencillos con los cual el interactura. Ya que no es relevante para el la complegidad de alguna de nuestras operaciones. Ejemplo:

``` java
public class Fachada {

	private Computadora computadora;
	
	public Fachada() {
		
		ITeclado teclado = new Teclado();
		IMouse mouse = new Mouse();
		
		this.computadora = new Computadora(teclado, mouse);
	}
	
	public void encender() {
		//Complejas
		this.computadora.encender();
	}
	
}

public class Main {

	public static void main(String[] args) {
		
		Fachada fachaComputadora = new Fachada();
		
		fachaComputadora.encender();
	}

}
```

En el ejemplo vemos como para nuestro cliente(Main), es sencillo encender el computador por medio de una fachadad, donde dentro de esta se estan ejecutando tareas complejas como interactuar con tablas en a DB, conectarse a API, etc. Con la finalidad de llevar a cabo dicha tarea(encender el computador).

Pd: Para este Ejemplo se omitieron varias clases e interfaces porque distraerian al lector del patron principal.

## Proxy
Provide a surrogate or placeholder for another object to control access to it.

Este patron comunmente tiene como objectivo limitar funcinabilidades de nuestro sistema. Principalmente por temas de seguridad. Ejemplo:

``` java
public interface IServicio {
	
	void leer();
	
	void escribir();
	
	void actualizar();
	
	void eliminar();
	
}

public class Usuario {

	private int nivelPermiso;//1 -- 5 //5 == Admin

	public Usuario(int nivelPermiso) {
		this.nivelPermiso = nivelPermiso;
	}
	
	public int getNivelPermiso() {
		return nivelPermiso;
	}

	public void setNivelPermiso(int nivelPermiso) {
		this.nivelPermiso = nivelPermiso;
	}
	
	
	
}

public class Servicio implements IServicio{
	
	public void leer() {
		System.out.println("Leer!");
	}
	
	public void escribir() {
		System.out.println("Escribir!");
	}
	
	public void actualizar() {
		System.out.println("Actualizar!");
	}
	
	public void eliminar() {
		System.out.println("Eliminar!");
	}
	
}

public class ProxyServicio implements IServicio {

	private IServicio servicio;
	
	public ProxyServicio(Usuario usuario) {
		
	}
	
	public void leer() {
		this.obtenerServicio().leer();
	}
	
	public void escribir() {
		this.obtenerServicio().escribir();
	}
	
	public void actualizar() {
		this.obtenerServicio().actualizar();
	}
	
	public void eliminar() {
		this.obtenerServicio().eliminar();
	}
	
	private IServicio obtenerServicio() {
		if(this.servicio == null) {
			this.servicio = new Servicio();//
		}
		
		return this.servicio;
	}
}

public class Main {

	public static void main(String[] args) {
		
		Usuario usuario = new Usuario(5);
		IServicio servicio = new ProxyServicio(usuario);
		
		servicio.leer(); //<--- Unica accion libre
		servicio.escribir();
		servicio.actualizar();
		servicio.eliminar();
		
	}

}
```

Nuestro Proxy le dara permisos de lectura a todo tipo de usuarios. Sin embargo, solo les dara permisos al resto de operacion a los usuarios Admin(aquellos con un nivel de rol igual a cinco).

Adicionalmente nuestro proxy solo esta creando el objecto *Servicio* en caso de que sea requerido(Esta estructura es conocidad como **Virtual Proxy**). Esto suponiendo que el dicho objeto tiene un alto costo de creación, por tal motivo no queremos crearlo innecesariamente.

### Flyweight
User sharing to support large number of fine-grained objects efficiently.

Este patron nos permite reutilizar objectos de tal manera que podamos crear aplicaciones con la minima cantidad de recursos necesarios(Aplicaciones ligeras).

``` java
public enum TipoNube {
	Chica,
	Mediana,
	Grande
}


import java.util.HashMap;

public class NubeFactory {

	private HashMap<TipoNube, Nube> nubesMap;
	
	public NubeFactory() {
		this.nubesMap = new HashMap<TipoNube, Nube>();
	}
	
	public Nube getNube(TipoNube tipo) {
		
		Nube nube = (Nube)this.nubesMap.get(tipo);
		
		if(nube == null) {
			nube = new Nube(tipo, "nube.png", 100, 100);
			this.nubesMap.put(tipo, nube);
		}
		
		return nube;
	}
	
	public int countNubesMap() {
		return this.nubesMap.size();
	}
	
}


public class Nube {

	private TipoNube tipo;
	private String imagen;
	private int posX;
	private int posY;
	
	public Nube(TipoNube tipo, String imagen, int posX, int posY) {
		this.tipo = tipo;
		this.imagen = imagen;
		this.posX = posX;
		this.posY = posY;
	}

	public String getImagen() {
		return imagen;
	}

	public void setImagen(String imagen) {
		this.imagen = imagen;
	}

	public int getPosX() {
		return posX;
	}

	public void setPosX(int posX) {
		this.posX = posX;
	}

	public int getPosY() {
		return posY;
	}

	public void setPosY(int posY) {
		this.posY = posY;
	}

	public TipoNube getTipo() {
		return tipo;
	}

	public void setTipo(TipoNube tipo) {
		this.tipo = tipo;
	}
	
	
}

public class Main {

	public static void main(String[] args) {
	
		NubeFactory factory = new NubeFactory();
		
		for(int x = 0; x < 100; x ++) {
			Nube nube = factory.getNube(TipoNube.Chica);
			System.out.println(nube);
		}
		
		for(int x = 0; x < 200; x ++) {
			Nube nube = factory.getNube(TipoNube.Mediana);
			System.out.println(nube);
		}
		
		for(int x = 0; x < 300; x ++) {
			Nube nube = factory.getNube(TipoNube.Grande);
			System.out.println(nube);
		}
		
		System.out.println(factory.countNubesMap());
	}

}

```

## De Comportamiento

### Chain of responsibility
Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.

Example:
``` java
public enum TipoTransaccion {
	Deposito,
	Retiro,
	Reembolso,
	Cheques
}

public class Transaccion {
	
	private float cantidad;
	private float balance;
	private TipoTransaccion tipoTransaccion;
	
	public Transaccion(float cantidad, float balance, TipoTransaccion tipoTransaccion) {
		this.setCantidad(cantidad);
		this.setBalance(balance);
		this.setTipoTransaccion(tipoTransaccion);
	}

	public float getCantidad() {
		return cantidad;
	}

	public void setCantidad(float cantidad) {
		this.cantidad = cantidad;
	}

	public float getBalance() {
		return balance;
	}

	public void setBalance(float balance) {
		this.balance = balance;
	}

	public TipoTransaccion getTipoTransaccion() {
		return tipoTransaccion;
	}

	public void setTipoTransaccion(TipoTransaccion tipoTransaccion) {
		this.tipoTransaccion = tipoTransaccion;
	}
}

public interface IManejadorTransacciones {

	void setNextManejador(IManejadorTransacciones next);
	
	void ejecutarTransaccion(Transaccion transaccion);
	
}


public class Deposito implements IManejadorTransacciones {

	private IManejadorTransacciones next;
	
	public void setNextManejador(IManejadorTransacciones next) {
		this.next = next;
	}
	
	public void ejecutarTransaccion(Transaccion transaccion) {
		
		if(transaccion.getTipoTransaccion() == TipoTransaccion.Deposito) {
			float cantidad = transaccion.getCantidad() + transaccion.getBalance();
			System.out.println("El nuevo balances después de un deposito es : " + cantidad);
		}else {
			this.next.ejecutarTransaccion(transaccion);
		}
		
	}
	
}

public class Reembolso implements IManejadorTransacciones {

	private IManejadorTransacciones next;
	
	public void setNextManejador(IManejadorTransacciones next) {
		this.next = next;
	}
	
	public void ejecutarTransaccion(Transaccion transaccion) {
		
		if(transaccion.getTipoTransaccion() == TipoTransaccion.Reembolso) {
			float cantidad = transaccion.getCantidad() + transaccion.getBalance();
			System.out.println("El nuevo balances después de un reembolso es : " + cantidad);
		}else {
			System.out.println("Operación No Valida!");
		}
		
	}
}

public class Retiro implements IManejadorTransacciones {

	private IManejadorTransacciones next;
	
	public void setNextManejador(IManejadorTransacciones next) {
		this.next = next;
	}
	
	public void ejecutarTransaccion(Transaccion transaccion) {
		
		if(transaccion.getTipoTransaccion() == TipoTransaccion.Retiro) {
			float cantidad = transaccion.getCantidad() - transaccion.getBalance();
			System.out.println("El nuevo balances después de un retiro es : " + cantidad);
		}else {
			this.next.ejecutarTransaccion(transaccion);
		}
		
	}
}

public class Main {

	public static void main(String[] args) {
		
		Transaccion transaccion = new Transaccion(100, 200, TipoTransaccion.Cheques);
		
		IManejadorTransacciones deposito = new Deposito();
		IManejadorTransacciones retiro = new Retiro();
		IManejadorTransacciones reembolso = new Reembolso();
		deposito.setNextManejador(retiro);
		retiro.setNextManejador(reembolso);
		
		deposito.ejecutarTransaccion(transaccion);
		
	}

}

```
El ejemplo anterior trata de un sistemas de transacciones bancarias. No es muy aplicable a la vida real pero sirve para mostrar este patron de deseño.

En el ejemplo vemos como la transaccion creada es pasada de objecto en objeto(Deposito, Retiro, Reembolso). Hasta dar con el objecto capaz de procesar dicha transaccion.

Para este ejemplo, el codigo podria tener un mejor performance. Principalmente si aplicaramos el Patron de diseño Virtual Proxy. Ya que si tuvieramos 100 objetos en la cadena. Es muy probable que instanciemos objetos(eslabones) que nunca utilizaremos.


### Command
Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

Es un patron de comportamiento. Se utiliza cuando hay una operacion, especialmente compleja, que debe ser realizada desde diferentes puntos de entrada.
Tipicamente este sucede cuando realizando una app WEB se debe realizar la misma operacion desde consulta de algun visitante como desde la linea de comandos.
Permite solicitar una operación a un objeto sin conocer realmente el contenido de esta operación, ni el receptor real de la misma. Para ello se encapsula la petición como un objeto, con lo que además facilita la parametrización de los métodos. Ejemplo:

``` java
public interface ICommand {

	void operacion();
	
}

public interface IDevise {
	
	void on();
	
	void off();
}

public class OffDevise implements ICommand {

	private IDevise devise;
	
	public OffDivise(IDevise devise) {
		this.devise = devise;
	}
	
	public void operacion() {
		this.devise.off();
	}
	
}

public class OnDevise implements ICommand {

	private IDevise devise;
	
	public OnDevise(IDevise devise) {
		this.devise = devise;
	}
	
	public void operacion() {
		this.devise.on();
	}
	
}

public class TV implements IDevise {
	
	private boolean on;
	
	public TV() {
		this.on = false;
	}
	
	public void on() {
		this.on = true;
		System.out.println("TV encendida!");
	}
	
	public void off() {
		this.on = true;
		System.out.println("TV apagada!");
	}
	
}

public class Main {

	public static void main(String[] args) {
		IDevise tv = new TV();
		
		ICommand on = new OnDevise(tv);
		ICommand off = new OffDevise(tv);
		
		on.operacion();
		off.operacion();
		
	}

}
```

En el ejemplo anterior podemos ver como los metodos "on" y "off", quedaron completamente encapsulados desde una respectiva clase que implementa la interfaz ICommad. Como vimos en el ejemplo cada metodo debe poseer una clase por separado, es decir si tuvieramos 100 metodos, abrian 100 clases, una para cada metodo.


Usualmente la interfaz va de esta manera simple. ¿Que es lo que hara el 'operacion' en este caso?
Bueno eso dependera del comando en especifico. pero de esta manera nos permite implementar facilmente el principio Open/Closed por ejemplo; Teniendo una lista de comando, ejecutarlos todos bajo un mismo metodo.

### Iterator
Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

Este patron provee un metodo estandar para acceder, secuencialmente a los elementos de una collección. En este Patron nosotros creamos una interfaz, de tal manera que si un objeto quiere acceder a los elementos de una collección, debera hacerlo por medio de la interfaz. De esta manera nosotros no exponemos los attributos ni metodos de la collección. Ejemplo

``` java
public interface Iterador {

	String siguiente();
	
	boolean contieneSiguiente();
	
}

import java.util.ArrayList;

public class GuiaTelefonica {

	private ArrayList<String> numeros;
	
	public GuiaTelefonica() {
		this.numeros = new ArrayList<String>();
	}
	
	public void add(String numero) {
		this.numeros.add(numero);
	}
	
	public ArrayList<String> getNumeros() {
		return this.numeros;
	}
	
}

public class IteradorGuia implements Iterador {

	private GuiaTelefonica guia;
	private int posicion;
	
	public IteradorGuia(GuiaTelefonica guia) {
		this.guia = guia;
	}
	
	public String siguiente() {
		return this.guia.getNumeros().get(this.posicion++);
	}
	
	public boolean contieneSiguiente() {
		return this.posicion < this.guia.getNumeros().size()
				&& this.guia.getNumeros().get(this.posicion) != null;
	}
	
}

public class Main {

	public static void main(String[] args) {
		GuiaTelefonica guia = new GuiaTelefonica();
		
		guia.add("123");
		guia.add("124");
		guia.add("125");
		guia.add("126");
		guia.add("127");
		guia.add("128");
		
		Iterador iterador = new IteradorGuia(guia);
		
		while(iterador.contieneSiguiente()) {
			System.out.println(iterador.siguiente());
		}

	}

}
```

### Mediator

Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.

Ese patron lo usaremos cuando deseemos comunicar objectos. Una analogia podria ser la de una torre de control(El mediador). Ya que esta enconstante comunicacion con las areonaves, y permite que las areonaves puedan comunicarse entre ellas.

A diferencia de otros patros, en este no tenemos un conjunto de reglas a seguir. Nos tendremos que valer en gran parte de nuestra intuición como desarrolladores.

En el seguiente ejemplo veremos un pequeño sistema de chat.

``` java
public class Usuario {
	
	private String nombre;
	
	public Usuario(String nombre) {
		this.nombre = nombre;
	}
	
	public void recibirMensaje(String mensaje) {
		System.out.println(mensaje);
	}
	
	public String getNombre() {
		return this.nombre;
	}

}

import java.util.HashMap;

public class SalaChat {

	private HashMap<String, Usuario> usuarios;
	
	public SalaChat() {
		this.usuarios = new HashMap<String, Usuario>();
	}
	
	public void addParticipante(Usuario usuario) {
		this.usuarios.put(usuario.getNombre(), usuario);
	}
	
	public void enviarMensaje(Usuario remitente, Usuario receptor, String mensaje) {
		
		if(this.usuarios.get(remitente.getNombre()) != null &&
				this.usuarios.get(receptor.getNombre()) != null) {
			
			mensaje = "De :" + remitente.getNombre() + " mensaje :" + mensaje;
			receptor.recibirMensaje(mensaje);
			
		}
	}
}

public class Main {

	public static void main(String[] args) {
		
		Usuario eduardo = new Usuario("Eduardo");
		Usuario codi = new Usuario("Codi");
		
		SalaChat sala = new SalaChat();
		
		sala.addParticipante(eduardo);
		sala.addParticipante(codi);
		
		sala.enviarMensaje(eduardo, codi, "Hola desde el curso de patrones de diseño!");

	}
}
```
### Memento
Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.

Permite capturar y exportar el estado interno de un objeto, para que luego se pueda restaurar sin romper la enapsulación.
Con memento nosotros podremos crear una copia de seguridad de un objeto, y si necesitamos revertir los cambio, podremos hacerlos desde dicha copia. Es decir podremos hacer un "Control Z".

La copia de seguridad puede ser parcial o total.

Para implementar este patron unicamente necesitaremos dos clases. Veamoslo en el siguiente ejemplo:

``` java

public class Usuario {

	private String nombre;
	private int edad;
	
	public Usuario(String nombre, int edad) {
		this.setNombre(nombre);
		this.setEdad(edad);
	}
	
	public Usuario getMemento() {
		return new Usuario(this.getNombre(), this.getEdad());
	}
	
	public void restartMemento(Usuario usuario) {
		this.setNombre(usuario.getNombre());
		this.setEdad(usuario.getEdad());
	}
	
	public String getNombre() {
		return nombre;
	}

	public void setNombre(String nombre) {
		this.nombre = nombre;
	}

	public int getEdad() {
		return edad;
	}

	public void setEdad(int edad) {
		this.edad = edad;
	}
	
}

public class Main {

	public static void main(String[] args) {
		
		Usuario usuario = new Usuario("Codi", 6 );
		
		Usuario memento = usuario.getMemento();//Nuestra copia!
		
		usuario.setNombre("Cambio de nombre");
		usuario.setEdad(20);
		
		System.out.println(usuario.getNombre());
		System.out.println(usuario.getEdad());
		
		usuario.restartMemento(memento);
		
		System.out.println(usuario.getNombre());
		System.out.println(usuario.getEdad());
		
	}

}

```

### Observer
Define at one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

El patrón observer se compone de un sujeto que ofrece mecanismos de suscripción y desuscripción a múltiples observadores que quieren ser notificados de los cambios en dicho sujeto.

Es uno de los patrones más utilizados, algunos ejemplos típicos son:
Newsletter
Sockets
Listeners en páginas web

Crearemos una interfaz, y esta la vamos a implementar en los observadores, es decir en los objetos que esta interesado en el cambio. Dentro de esta interfaz nosotros colocaremos las direfentes acciones que un observador puede tener(Resurtir bodega, generar factura, etc).

Tendremos otra Interfaz *Observable*, esta debe posser al menos dos metodos; **addObserver** y **notify**.

Ejemplo:
``` java

public interface IObservable {

	void addObserver(IObserver o);
	
	void notificarObservadores();
	
	void removeObserver();
	
}

public interface IObserver {

	void notificacion(String mensaje);
	
}

import java.util.Set;
import java.util.LinkedHashSet;

public class Producto implements IObservable {
	
	private Set<IObserver> observadores;
	
	private int stock;
	
	public Producto(int stock) {
		this.stock = stock;
		this.observadores = new LinkedHashSet<>();
	}
	
	public void venta() {
		this.setStock(this.stock - 1);
		System.out.println("Producto vendido!");
		
		this.notificarObservadores();
	}

	public int getStock() {
		return stock;
	}

	public void setStock(int stock) {
		this.stock = stock;
	}
	
	public void addObserver(IObserver o) {
		this.observadores.add(o);
	}
	
	public void notificarObservadores() {
		for(IObserver observador : this.observadores)
			observador.notificacion("EL producto se vendio!");
	}
	
	public void removeObserver() {
		
	}
}

public class Usuario implements IObserver {

	public void notificacion(String mensaje){
		System.out.println(mensaje);
	}
	
}

public class Main {

	public static void main(String[] args) {
		
		Producto aguacate = new Producto(10);
		
		Usuario usuario1 = new Usuario();
		Usuario usuario2 = new Usuario();
		Usuario usuario3 = new Usuario(); //
		
		aguacate.addObserver(usuario1);
		aguacate.addObserver(usuario2);
		
		aguacate.venta();
	}
}
```
### State
Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.

Este patron lo utilizaremos cuando trabajemos con maquinas de estado

Utilizando el patron State, nosotros debemos crear una interfaz con todos nuestros estados y una nueva clase por cada estado de nuestro objeto.

Ejemplo:

``` java
public interface IEstadoAuto {

	void encender();
	
	void manejar();
	
	void apagar();
	
}

public class AutoApagar implements IEstadoAuto {
	
	private final Auto auto;
	
	public AutoApagar(Auto auto) {
		this.auto = auto;
	}
	
	public void encender() {
		System.out.println("El auto esta encendido!");
		auto.setEstadoActual(auto.getAutoEncendio());
	}
	
	public void manejar() {
		System.out.println("El auto no se puede manejar si esta apagado!");
	}
	
	public void apagar() {
		System.out.println("El auto ya esta apagado!");
	}
	
}

public class AutoEncender implements IEstadoAuto {
	
	private final Auto auto;
	
	public AutoEncender(Auto auto) {
		this.auto = auto;
	}
	
	public void encender() {
		System.out.println("El auto esta encendido!");
	}
	
	public void manejar() {
		System.out.println("El auto esta en movimiento!");
		auto.setEstadoActual(auto.getAutoMovimiento());
	}
	
	public void apagar() {
		System.out.println("El auto esta apagado!");
		auto.setEstadoActual(auto.getAutoApagado());
	}
	
}

public class AutoManejar implements IEstadoAuto {
	
	private final Auto auto;
	
	public AutoManejar(Auto auto) {
		this.auto = auto;
	}
	
	public void encender() {
		System.out.println("El auto ya esta encendido!");
	}
	
	public void manejar() {
		System.out.println("El auto ya se esta moviendo!");
	}
	
	public void apagar() {
		System.out.println("El auto esta apagado!");
		auto.setEstadoActual(auto.getAutoApagado());
	}
	
}

public class Auto implements IEstadoAuto {
  
  private IEstadoAuto autoEncendio;
  private IEstadoAuto autoMovimiento;
  private IEstadoAuto autoApagado;
  
  IEstadoAuto estadoActual;
  
  public Auto() {
    this.autoEncendio = new AutoEncender(this);
    this.autoApagado = new AutoApagar(this);
    this.autoMovimiento = new AutoManejar(this);
    
    this.estadoActual = this.autoApagado;
  }
  
  public void encender() {
    this.estadoActual.encender();
  }
  
  public void manejar() {
    this.estadoActual.manejar();
  }
  
  public void apagar() {
    this.estadoActual.apagar();
  }

  public IEstadoAuto getAutoEncendio() {
    return autoEncendio;
  }

  public void setAutoEncendio(IEstadoAuto autoEncendio) {
    this.autoEncendio = autoEncendio;
  }

  public IEstadoAuto getAutoMovimiento() {
    return autoMovimiento;
  }

  public void setAutoMovimiento(IEstadoAuto autoMovimiento) {
    this.autoMovimiento = autoMovimiento;
  }

  public IEstadoAuto getAutoApagado() {
    return autoApagado;
  }

  public void setAutoApagado(IEstadoAuto autoApagado) {
    this.autoApagado = autoApagado;
  }

  public IEstadoAuto getEstadoActual() {
    return estadoActual;
  }

  public void setEstadoActual(IEstadoAuto estadoActual) {
    this.estadoActual = estadoActual;
  }
  
}

public class Main {

	public static void main(String[] args) {
		Auto auto = new Auto();
	    
		auto.apagar();
		auto.encender();
		auto.manejar();
		
	    /*
	     * Encendido
	     * En Movimiento
	     * Apagado
	     * */
	}

}
```
### Strategy
Define a family of algorithms, encapsulate each one, and make then interchangeable. Strategy lets the algorithm vary independently from clients that use it.

Nos permite encapsular algoritmos en clases, de tal manera que nosotros podamos utilizar diferentes algoritmos en tiempo de ejecución, podemos verlo como una caja de lego, donde cada pieza es un algoritmo y dependiendo de nuestras necesidades en tiempo de ejecución nosotros podremos utiizar una pieza u otra.

Este patron es muy usado cuando nuestra aplicación tiene muchas varientes en los algoritmos. Como por ejemplo un sistema de comisiones.

Veamos un ejemplo con dos tipo de algoritmos(dos clases), deposito y retiro:

1. Se crea la interfaz base.
2. Se crean las clases por algoritmo.
3. Se crea una clase contexto.

``` java
public interface IEstrategia {

	float realizarOperacion(float balance, float cantidad);
	
}

public class Retiro implements IEstrategia {

	public float realizarOperacion(float balance, float cantidad) {
		return balance - cantidad;
	}
	
}

public class Deposito implements IEstrategia {

	public float realizarOperacion(float balance, float cantidad) {
		return balance + cantidad;
	}
	
}

public class Transaccion {

	private IEstrategia estrategia;//algoritmo
	
	public Transaccion(IEstrategia estrategia) {
		this.estrategia = estrategia;
	}
	
	public float ejecutarTransaccion(float balance, float cantidad) {
		return this.estrategia.realizarOperacion(balance, cantidad);
	}
	
	
}

public class Main {

	public static void main(String[] args) {

		Transaccion transaccion1 = new Transaccion( new Deposito() );
		System.out.println(transaccion1.ejecutarTransaccion(100, 20));
		
		
		Transaccion transaccion2 = new Transaccion( new Retiro() );
		System.out.println(transaccion2.ejecutarTransaccion(100, 20));
		
	}

}
```

### Template Method
Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

``` java
public abstract class Usuario {

	public void autenticacion() {
		System.out.println("TODOS los usuarios necesitan autenticarse!");
	}
	
	abstract void formaTrabajar();
	
}

public class Administrador extends Usuario {

	public void formaTrabajar() {
		System.out.println("La forma de trabajar de un Administrador!");
	}
	
}

public class Gerente extends Usuario {

	public void formaTrabajar() {
		System.out.println("La forma de trabajar de un Gerente!");
	}
	
}

public class Main {

	public static void main(String[] args) {
		
		Usuario gerente = new Gerente();
		Usuario administrador = new Administrador();
		
		gerente.autenticacion();
		gerente.formaTrabajar();
		
		administrador.autenticacion();
		administrador.formaTrabajar();

	}

}
```

Este patron basicamente trata en abstraer los metodos en comun de los objetos relacionados.

En este caso el tipo de usuario Admin y Manager, heredan de la clase abstracta User, que viene siendo el Template.

### Visitor
Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

Si un objeto es el responsable de mantener cierto tipo de información, entonces, es logico asignarle tambien todas las operaciones que manipulen esa información.

Para esto generaremos dos interfaces:
- una Visitor: Sera la encargada de gestionar los distintos tipo de algoritmos, esta interfaz tendra una sobre carga de metodos usualmente.
- una Visitable: Sera la encargada de llamar a algoritmo perse.

``` java
public interface IFruta {

	float getPrecio();

}

public interface ILineaBlanca {

	float getPrecio();
	
}

public interface IVisitor {

	float descuento(IFruta fruta);//descuento
	
	float descuento(ILineaBlanca lineaBlanca);
	
}

public interface IVisitable {

	float aplicarDescuento(IVisitor visitor);
	
}

public class Lavadora implements IFruta, IVisitable {

	public float getPrecio() {
		return 20f;
	}
	
	public float aplicarDescuento(IVisitor visitor) {
		return visitor.descuento(this);
	}
	
}

public class Manzana implements IFruta, IVisitable {

	public float getPrecio() {
		return 2f;
	}
	
	public float aplicarDescuento(IVisitor visitor) {
		return visitor.descuento(this);
	}
	
}

public class Main {
	
	public static void main(String[] args) {
		
		//Fruta 10% de descuento
		//LíneBlanca 5% de descuento
		
		
		Manzana manzana = new Manzana();
		Lavadora lavadora = new Lavadora();
		
		IVisitor descuento = new DescuentoComun();
		
		System.out.println(manzana.aplicarDescuento(  descuento ));
		System.out.println(lavadora.aplicarDescuento(  descuento));
		
	}
}
```

# Documentacion

Documentar es una de las mejores prácticas que podemos hacer cuando estamos en un equipo de trabajo.

* Dejar por escrito cómo hemos hecho algunas funcionalidades.¿Cual es la logica del negocio?
* Sobretodo debemos dejar comentarios en el código que ayuden a las personas a ubicarse en qué parte de la aplicación están y qué hacen esas líneas de código.

## ¿Que Documentar?

Es un poco complejo pero basicamente tienes que documentar pensando en la persona que tomara tu codigo cuando tu lo deje(esa persona que continuara tu trabajo), tienes que documentar pensando en que la persona que leera esas linea no tiene la menor idea de que hace tu aplicacion. Algunas preguntas utilies para documentar tu codigo son:

* ¿Como implementar una nueva funcionalidad en caso de querer hacerlo?
* ¿Cómo podría ser mejorando el código?.
* ¿Como se realizan las pruebas?
* ¿Quienes son los involucrados en el proyecto?
* ¿Como se puede llevar nuevo codigo a produccion?
* Etc. Toda aquella pregunta que nos lleve a ser mas claros en como manipular el codigo.

## ¿Como Documentar?

Esta depende de quienes son las personas que leeran este codigo.

* ¿Usan lenguaje tecnico?
* ¿tiene suficiente experiencia?
* ¿Tiene un conocimiento similar al tuyo?

Al hablar de Documentacion no hablamos solamente de texto, los graficos tambien son muy buenos para comprender las ideas como por ejemplo UML.

## ¿Donde documentar?

Basicamente existen dos lugar:

* **Dentro del propio codigo.**

``` php
<?php

/** 

* Retorna la suma de dos numeros enteros
* @param int $a
* @param int $b

*/
function add ( int $a, int $b ) {
   
    return $a +$b;
}
```

Documentacion clara, concisa y pequeña.

* **Algun otro repositorio:** una wiki, documentos compartidos, etc.

## ¿Cuando documentar?

* Lo ideal es ir escribiendo la documentacion a la par del codigo. A penas terminas de escribir el codigo, ir y escribir su documentacion.

* Cuando pudiste resolver un problema bastate complejo y notaste que te faltaba informacion.

# Testing Automatizado

Existen dos tipos de testing, es completamente recomendado(es lo correcto) realizar ambos tipos:

*NOTA:* En *PHP* podemos utilizar *phpUnit* para realizar nuestros test.

1. **Unit Testing:**

Evaluamos el funcionamiento de los componentes individualmente. Esto fomenta:

* el refactory(volver a escribir el codigo de una mejor manera).
* Facilita la integracion con otras piezas de codigo.
* Ayuda a dejar el codigo documentado.

Para **implementar el unit testing** requerimos de una herramienta que nos permita escribir el test y por otro lado mirar sus resultados.

2. **Integration Testing**: Validar la interacción entre los componentes y el sistema completo. En estas pruebas se evalua y hacen prueba ya del 'producto' final que debe arrojar el programa.

## Creacion de un entorno de pruebas en PHP

crearemos un entorno para poder ejecutar PHPUnit (El framework de pruebas unitarias más utilizado con PHP).

1. **Descargar el proyecto**

El primer paso es clonar el repositorio https://github.com/mchojrin/platzi-tdd

2. **Instalar PHP**

Si estás en un entorno Linux o Mac probablemente ya tendrás PHP instalado, con lo cual puedes saltar este paso.

Si estás en Windows deberás descargar PHP de aquí y probablemente también tengas que instalar el Runtime de Visual C++ que puedes descargar de aquí.

Para comprobar que la instalación haya sido exitosa debes abrir una terminal y ejecutar el comando php -v.

3. **Instalar Composer**

Una vez instalado PHP el siguiente paso es instalar composer, un manejador de dependencias para php (Puedes leer más de qué se trata [aquí](https://academy.leewayweb.com/que-es-composer/)).

La forma más simple de instalar composer es hacerlo a través del propio php siguiendo las instrucciones presentes [aquí](https://getcomposer.org/download/).

Si utilizas Windows puedes usar [este](https://getcomposer.org/Composer-Setup.exe) instalador.

4. **Instalar PHPUnit**

PHPUnit es una librería estándar para la ejecución de pruebas unitarias de PHP.

En general puedes descargarlo de [aquí](https://phpunit.de/getting-started/phpunit-8.html). En este caso, utilizaremos la versión de instalación por proyecto.

PHPUnit es la dependencia principal de nuestro proyecto, si tienes instalado composer, su instalación es muy simple.

Sólo debes abrir una terminal en el directorio donde descargaste el proyecto y ejecutar `composer install` .

El resultado debería verse similar a:

![phpUnit1](img/good-practices/phpUnit.jpg)

Para verificar la instalación ejecuta el comando `php vendor/phpunit/phpunit/phpunit` 

La salida debería verse así:

![phpUnit2](img/good-practices/phpUnit2.jpg)

5. **Configurar el entorno**

Durante este curso utilizamos Visual Studio Code. Si ya dispones de otro entorno y lo conoces bien puedes utilizarlo, si no tienes preferencia te recomiendo que utilices VS Code.

Puedes descargarlo de [aquí](https://code.visualstudio.com/Download)

Una vez instalado abre la carpeta donde descargaste el proyecto en Visual Studio. Deberas ver algo como:

![code](img/good-practices/code.jpg)

Escribe un primer test para verificar que todo está configurado correctamente:

![test1](img/good-practices/test1.jpg)

Y para ejecutarlo, abre un terminal dentro del Visual Studio Code:

![cmd](img/good-practices/cmd.jpg)

Una vez en la consola escribe el comando: `php vendor/phpunit/phpunit/phpunit tests` 

![test2](img/good-practices/test2.jpg)

Y deberás ver en la salida:

![test3](img/good-practices/test3.jpg)

Con esto tendrás todo lo necesario para avanzar al proximo punto(TDD)

## Test Driven Development

[TDD](https://www.youtube.com/watch?time_continue=44&v=EBtu4WyWHPc) o Test Driven Development es una metodología donde hacemos todo al revés(Esta propone: Primero escribir las pruebsa y luego el software). Por un momento vamos a dejar de programar para dedicarnos a escribir las pruebas.

Este tipo de prueba es del tipo *unit test* y Se trata de lo siguiente:

* Pensar en una funcionalidad que queremos implementar y preguntarnos ¿Como vamos a determinar que lo que vayamos a implementar efectivamente es correcto y hace lo que debe hacer?
* Escribimos el test
* Esperamos que falle.
* Escribimos el minimo codigo necesario para que funcione.
* Examinamos nuestro codigo en busca de mejoras.
* Repetir

Ejemplo:

``` php
<?php 

use PHPUnit\Framework\TestCase;

class CalculatorTest extends TestCase
{
    public function testAddWillReturnTheSumOfItsParameters()
    {
        $sut = new Calculator();
     
        $this->assertEquals(8, $sut->add(5,3));
        $this->assertEquals(5, $sut->add(5,0));
    }

    public function testAddWillReturnTheSubtractOfItsParameters()
    {
        $sut = new Calculator();
     
        $this->assertEquals(5, $sut->subtract(8,3));
        $this->assertEquals(8, $sut->subtract(10,2));
        $this->assertEquals(2, $sut->subtract(4,2));
    }
    
    public function testAddWillReturnTheMultiplyOfItsParameters()
    {
        $sut = new Calculator();
     
        $this->assertEquals(24, $sut->multiply(8,3));
        $this->assertEquals(20, $sut->multiply(10,2));
        $this->assertEquals(8, $sut->multiply(4,2));
    }

    public function testAddWillReturnTheDivideOfItsParameters()
    {
        $sut = new Calculator();
     
        $this->assertEquals(5, $sut->divide(10,2));
        $this->assertEquals(20, $sut->divide(40,2));
        $this->assertEquals(4, $sut->divide(8,2));
    }
}

<?php
class Calculator
{
    public function add(int $a, int $b): int
    {
        return $a + $b;
    }
    
    public function subtract(int $a, int $b): int
    {
        return $a - $b;
    }
    
    public function multiply(int $a, int $b): int
    {
        return $a * $b;
    }

    public function divide(int $a, int $b): float
    {
        if ($b ===0) {
            thrownew InvalidArgumentException('No se puede dividir entre 0');
        }
        return $a / $b;
    }
    
}

Resultados de pruebas:

root@debian:/var/www/html/platzi/platzi-tdd# vendor/phpunit/phpunit/phpunit --testdox  tests/CalculatorTest.php
PHPUnit 8.2.2 by Sebastian Bergmann and contributors.

Calculator
 ✔ Add will return the sum of its parameters
 ✔ Add will return the subtract of its parameters
 ✔ Add will return the multiply of its parameters
 ✔ Add will return the divide of its parameters

Time: 52 ms, Memory: 4.00 MB

OK (4 tests, 11 assertions)
```
