---
title: "Bases de Datos"
slug: "bases-de-datos"
description: "🗄"
keywords: [programacion, desarrollo, software, sql, bases de datos, relacional, mysql]
draft: true
tags: []
math: false
toc: false
---
# Importante
La gran parte de esta notas asi como la mayoria de sus ejemplo estan en español. 

Esto en proyectos reales, no es una buena practica. 

Estan de esta manera para que le sea de mayor ayuda a los nuevos miembros de la comunidad hispana de programadores. 

# MYSQL

## Instalacion

Para realizar la instalación de MySQL en tu pc lo primero que debes tener en cuenta es que debes hacer la verificación de la versión que quieres instalar y la distribución para tu sistema operativo. En este enlace encuentras el listado de las plataformas soportadas. 

### Windows

Si estas trabajando con Windows puedes hacer la descarga ingresando en el siguiente [enlace](https://dev.mysql.com/downloads/installer/). Este es el sitio oficial de MySQL por lo que puedes confiar en la descarga. 

El instalador para Windows es muy similar a los que ya conocemos, nos pide algunas verificaciones y nos permite navegar a través de diferentes ventanas. 

Inicialmente el instalador nos va a solicitar que aceptemos la los términos y acuerdos de la licencia. Revisalos y si estas de acuerdo continua. 

En seguida te va a solicitar información relacionada con el tipo de instalación que vas a realizar, puedes elegir entre Developer Default, Client Only y Full. Cualquiera que sea la opción que elijas esto no implica que luego puedas actualizarla. 

Si instalas la versión Full vas a tener acceso a todas las características y productos que MySQL ofrece. 

Verifica que tengas disponibles todos los requerimientos que el instalador te presenta. En caso de no contar con ellos debes descargar e instalar el software solicitado. 

Continua con la instalación de acuerdo a lo que te indica el ayudante. 

### Mac

En nuestro caso vamos a estar trabajando con MySQL en Mac por lo que haremos la instalación en este sistema operativo. 

Para instalar MySQL usando el instalador del paquete:

Descarga el archivo de imagen del disco ( . dmg ) que contiene el instalador del paquete MySQL. No es necesario tener una cuenta en Oracle para realizar la instalación pero es recomendable hacerlo. 

Haz doble clic sobre el archivo para montar la imagen y ver su contenido. 

Esto te va a mostrar el asistente de instalación de MySQL. El SO puede preguntarte si confías en el origen de este programa, puedes darle continuar hasta que llegues al installation type puedes hacer clic en Instalar para ejecutar el asistente de instalación utilizando todos los valores predeterminados, o puedes hacer clic en Personalizar para modificar qué componentes instalar (servidor MySQL, Prueba de MySQL, Panel de preferencias, Soporte inicializado; todas las pruebas excepto MySQL están habilitadas por defecto). En este caso esta bien que instalemos con los valores por defecto. 

Selecciona el tipo de cifrado de contraseñas que vas a usar para tu base de datos. 

Ingresa una contraseña que no se te vaya a perder u olvidar, porque es la contraseña de tu usuario root para la base de datos. 

En este punto ya tienes instalado tu servidor de MySQL y puedes continuar con el curso. 

### Linux Debian

Tutorial sencillo para los usuarios de Linux:

Se instala el servidor y cliente de mysql. 
`sudo apt-get install mysql-server mysql-client` 

Accedes a la base de datos de mysql. 
`> usemysql;` 

Creas un nuevo usuario. 
`create user 'tuNombreDeUsuario'@'localhost' identified by'tuContraseña';` 

Modificas las siguientes configuraciones de tu usuario. 

``` SQL
GRANT allprivileges ON *.* TO  'tuNombreDeUsuario'@'localhost'; 
UPDATE user SET plugin="auth_socket" WHERE User= 'tuNombreDeUsuario'; 
FLUSH PRIVILEGES; 
```

Listo, ya tienes los privilegios para acceder. 

## Conexcion a la BD

A traves de la terminal es la manera mas optima de acceder a la base de datos, esto lo hacemos atraves del siguiente comando: `mysql -u root -h localhost -p` 

Banderas:

* -u : Nombre del usuario
* -h : Nombre del host
* -p : Contraseña

## Algunos datos de interes:

* **Comentarios:**

``` SQL
/* 
Esta es la formam en que creamos
un comentario de bloque
 */

-- Y asi podemos crear un comenteario de una sola linea
```

* **Ejecutar ficheros**

Para ejecutar ficheros con la extension *. sql*, seguimos la siguiente estructura. 

``` shell

# Si no estamos autenticados

mysql -u user -p < fichero.sql

# Si estamos autenticados(dentro de la consola de mysql)

SOURCE fichero.sql; 
```

* **Ejecutar sentencias fuera deslogueados:**

``` shell
mysql -u root -p libreria -e "SELECT * FROM autores; "
```

* **Condicionales:**

A menudo tenemos que crear o eliminar tablas y bases de datos que no estamos totalmente seguro si ya estaban creadas, para solucionar estoy y evitar un posible error en nuestros scripts, utilizamos las siguientes estruturas

``` SQL
DROP DATABASE IF EXISTS libreria;
CREATE DATABASE IF NOT EXISTS libreria;
```

Como vimos solo tenemos que agregar `IF NOT EXISTS` o `IF EXISTS` antes del nombre de la tabla o base de datos. 

### Restablecer contraseña de root MySQL

En el caso de que hayamos perdido la contraseña del usurio root, la podemos recuperar siguiendo los siguiente pasos

Lo primero que devmos hacer es detener el servidor, con cualquiera de los siguiente comandos:

``` shell

> mysql.server top
> service mysqls stop
> mysql stop

```

Una vez el servidor se encuentre detenido, debemos de reiniciarlo en un modo seguro. 

``` shell
sudo mysqld_safe --skip-grant-tables --skip-networkin
```

**--skip-grant-tables** Permite conectarnos al servidor sin la necesidad de un password, además de otrogar todos los privilegios a la sesión. 

**--skip-networkin** Detiene la escucha de peticiones TCP/IP 

Ahora, en una nueva pestaña, debemos de conectarnos al servidor utilizando el usuario root:

``` shell
mysql -u root
```

Una vez dentro del servidor, debemos de trabajar con la base de datos **MySQL**

``` shell
USE mysql;
```

Con el cambio de base de datos haremos la actualización. 

``` shell
UPDATE user SET password=PASSWORD('tu_password') WHERE user='root'; 
```

Si la actualización fue exitosa debemos de salir del servidor

``` shell
FLUSH PRIVILEGES;
exit
```

El paso final es detener el servidor en modo seguro. Iniciamos el servidor como te costumbre y nos autenticamos, la contraseña ya estará funcionando. 

``` shell
mysql -u root -p 
```

## Declaracion de Variables

Una vez iniciada la sesion en el cliente de base de datos. La sintaxis para declarar una variable es la siguiente

``` SQL
SET @nombre = "Valor";

SET @nombre2 := "Valor2"

SET @curso = "Data Bases", @gestor = "Mysql";
```

Nosotros podemos declarar variables en practicamente cualquier lugar: En funciones, Procedimientos, En sentias, etc. 

*NOTA:* Como pudiste notar, existen dos operadores validos para declarar una variable, el *=* y el *:=*. 

**IMPORTANTE:** Las variables declaradas dentro de una sesion, perteneceran solo al scope de la misma. Es decir, no podran ser accedidas por otros usuario, e incluso ya no estaran diponibles en el instante que cerremos nuestra sesion. 

## Obtencion de datos

Para obtener datos de nuestro servidor es muy sencillos. Para esto utilizamos la palabra reservada. *SELECT*

``` SQL
SET @nombre = "Valor", @curso = "Data Bases";

SELECT @nombre, @curso;
```

## Base de Datos

### Crear
La estructura para crear una base de datos es la siguiente:

``` SQL
CREATE DATABASE libreria;
```

**NOTA:** Con MySQL nosotros podemos establecer el charset que usará la base de datos desde su creación `CREATE DATABASE nombre character set utf8;` 

### Listar

Para listar las bases de datos disponibles en nuestro servidor, ejecutaremos:

``` SQL
SHOW DATABASES;
```

### Eliminar

Para Eliminar una base de datos de nuestro servidor ejecutaremos:

``` SQL
DROP DATABASE libreria;
```

Esto eliminara por completo nuestra base de datos(Datos y estructura)

## Tipos de datos

En general, la mayoría de los servidores de base de datos nos permiten almacenar los mismo tipo de datos, como strings, fechas y número. 

### Alfanuméricos

* CHAR
* VARCHAR

En ambos casos nosotros debemos de especificar la longitud máxima que podrá almacenar el campo. Opcionalmente podemos definir el charset que almacenará. 
`VARCHAR(20) character set utf8` 

### Números enteros

| Tipo      | Rango     |
| --        | --        |
| Tinyint   | -128 a 127 |
| Smallint  | -32, 768 a 32, 767 |
| Mediumint | −8, 388, 608 a 8, 388, 607 |
| Int       | −2, 147, 483, 648 a 2, 147, 483, 647 |
| Bigint    | −9, 223, 372, 036, 854, 775, 808 a 9, 223, 372, 036, 854, 775, 807 |

### Números flotantes

Para los flotantes encontraremos dos tipos

* Float
* Double

En ambos casos nosotros debemos de especificar la cantidad de dígitos que almacenará la columna antes y después del punto (p, s). 

`precio FLOAT(3, 2)` 

En este caso la columna podrá almacenar hasta tres dígitos como enteros y dos después del punto decimal. Ejemplo: *Ejemplo 999. 99*

### Tiempo

| Tipo      | Formato default   |
| --        | --                |
| Date      | YYY-MM-DD         |
| Datetime  | YYY-MM-DD HH: MI: SS|
| Timestamp | YYY-MM-DD HH: HI: SS|
| Time      | HHH: MI: SS         |

## Tablas

Es importante tomar en cuenta que para manupular cualquiera de nuestras tablas, primero debemos indicar que Base de datos esteremos utilizando. Esto los hacemos a traves de la sentencia: `USE libreria;` . 

*NOTA:* Si queremos saber en que base de datos estamos trabajando utilizaremos la sentencia `SELECT DATABASE(); ` 

### Crear

``` SQL
CREATE TABLE autores (

    /* columna y tipo de dato */
    autor_id INT, 
    nombre VARCHAR(25), 
    apellido VARCHAR(25), 
    genero CHAR(1), 
    fecha_nacimiento DATE, 
    pais_origen VARCHAR(40)

); 
```

### Listar

``` SQL
SHOW TABLES;
```

### Elimiar

``` SQL
DROP TABLES autores;
```

### Editar

#### Renombrar tabla

``` SQL
-- Estructura:
-- ALTER TABLE old_name RENAME new_name;
ALTER TABLE usuarios RENAME users;
```

#### Agregar columnas

``` SQL
-- Estructura:
-- ALTER TABLE table_name ADD new_column TYPE [CONSTRAINTS] [DEFAULT value]; 
ALTER TABLE libros ADD ventas INT UNSIGNED NOT NULL; 
```

#### Modificar el tipo de dato de una columna

``` SQL
-- Estructura:
-- ALTER TABLE table_name MODIFY name_colum NEW_TYPE; 
ALTER TABLE usuarios MODIFY telefono VARCHAR(50); 
```

#### Eliminar columnas

``` SQL
-- Estructura:
-- ALTER TABLE table_name DROP column_name;
ALTER TABLE libros DROP ventas;
```

#### Agregar llave foránea

``` SQL
-- Estructura
-- ALTER TABLE table_name ADD FOREIGN KEY(column_name) REFERENCES table_reference(primary_key); 
ALTER TABLE usuarios ADD FOREIGN KEY(grupo_id) REFERENCES grupos(grupo_id); 
```

#### Eliminar llaves foraneas

``` SQL
-- Estructura
-- ALTER TABLE table_name DROP FOREIGN KEY column_name;
ALTER TABLE usuarios DROP FOREIGN KEY grupo_id;
```

### Información

Si deseamos obtener informacion sobre la estructura(definicion) de una tabla, ejecutaremos la sentencia

``` SQL
DESC autores; 
-- Tambien podemos utilizar la sentencia:
SHOW COLUMNS FROM autores; 
-- Ambas sentencia nos arrojan el mismo output.
```

---

### Crear tablas a partir de otras

``` SQL
CREATE TABLE usuarios LIKE autores;
```

### Restricciones

Las restrincciones son una especie de "banderas" que le podemos colocar a los campos de nuestra tablas siguiendo la siguiente estructura `nombre VARCHAR(25) RESTRICCION1 RESTRICCION2` 

Algunas restricciones:

* NOT NULL -> El campo no puede ser nulo
* UNSIGNED -> El campo solo puede almacenar numero positivos
* ENUM(OPT1, OPT2, ... , OPTn) -> El campo solo puede almacenar uno de los valores descriptos, Este pueder ser: numerico o de tipo texto. Este tipo de restriccion No es sensible a mayusculas y minisculas. 

### Insertar Datos

``` SQL
INSERT INTO autores (autor_id, nombre, apellido, genero, fecha_nacimiento, pais_origen)
VALUES (1, "Jesus", "Millan", "M", "1996-12-30", "Venezuela"); 

/* La linea anterior puede resumirse tambien como  */
INSERT INTO autores VALUES (2, "Jose", "Marcano", "M", "1970-10-20", "Venezuela"); 

/* SI se desean insertar solo algunos campos, Se puede hacer con */
INSERT INTO autores (autor_id, apellido, nombre)
VALUES (3, "Martinez", "Maria"); 

-- Si deseamos insertar varias tuplas o registros en una sola sentencia
INSERT INTO autores (autor_id, nombre, genero, fecha_nacimiento, pais_origen)
VALUES (1, "Code", "M", "1996-12-30", "Venezuela"), 

    (2, "Code", "M", "1996-12-30", "Venezuela"), 
    (3, "Code", "M", "1996-12-30", "Venezuela"), 
    (4, "Code", "M", "1996-12-30", "Venezuela"), 
    (5, "Code", "M", "1996-12-30", "Venezuela"), 
    (6, "Code", "M", "1996-12-30", "Venezuela"); 

```

### Llaves

Las llaves son muy importantes en las tablas, principalmente esta nos permitiran realizar busqueda muy mas rapidas. 

#### Primarias

Son la llave principal de la tabla

A tener en cuenta:

* Se recomiendan que sean de tipo un tipo entero
* Se recomientda que solo haya una por tabla
* Colocar la opcion AUTO_INCREMENT

Estructua:
`col_id TYPE PRIMARY KEY [AUTO_INCREMENT]` 

Ejemplos:

``` SQL
CREATE TABLE usuarios( 
  usuario_id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT
); 
-- ó --
CREATE TABLE usuarios( 
  usuario_id INT UNSIGNED AUTO_INCREMENT, 
  PRIMARY KEY(usuario_id)
); 

```

#### Foraneas

Las llaves foraneas nos permiten crear relaciones entre tablas de una forma rapida. La forma en la que funciona es que hacen referencia a un campo de otra tabla(generalmente al campo de la llave primaria), es importante mencionar que estos campo deben ser del mismo tipo. 
Estructura:
`FOREIGN KEY (columna) REFERENCES tabla_referencia(llave_primaria)` 

Ejemplo:

``` SQL
CREATE TABLE autores (

    autor_id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT, 
    nombre VARCHAR(25) NOT NULL, 
    apellido VARCHAR(25) NOT NULL, 
    genero ENUM('M'.'F'), 
    fecha_nacimiento DATE NOT NULL, 
    pais_origen VARCHAR(40) NOT NULL

); 

CREATE TABLE libros (

    libro_id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT, 
    autor_id INT UNSIGNED NOT NULL, -- Esta es la llave foranea
    titulo VARCHAR(60) NOT NULL, 
    fecha_publicacion DATE NOT NULL, 
    descripcion VARCHAR(255)

    --Aqui declaramo que el campo autor_id es una llave forenea.
    FOREIGN KEY (autor_id) REFERENCES autores(autor_id) 

); 

/*
NOTA: fijese que primero fue declarada la tabla autores para luego hacer
referencia a ella desde la tabla libros
*/
```

#### Unicos

Nos permite hacer referencia de que un campo tendra un valor unico en nuestra tabla. 

Estructura:
`field TYPE UNIQUE` 
Ejemplos:

``` SQL
CREATE TABLE usuarios( 
  usuario_id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT, 
  nombre VARCHAR(50) UNIQUE
); 
-- otra opcion es: --
CREATE TABLE usuarios( 
  usuario_id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT, 
  nombre VARCHAR(50), 
  CONSTRAINT UNIQUE (nombre)
); 
```

NOTA: La palabra **CONSTRAINT** es opcional, sin embargo, por temas de legibilidad recomiendo colocarla. 

**COMBINACION** de valores unicos:
Si necesitamos validar el valor único de una combinación de columnas lo haremos de la siguiente manera. 
En este caso queremos validar que la combinación de nombre, apellido y matricula sean unicas en la tabla. 

``` SQL
CREATE TABLE usuarios( 
  usuario_id INT UNSIGNED NOT NULL AUTO_INCREMENT, 
  nombre VARCHAR(50), 
  apellido VARCHAR(50), 
  matricula VARCHAR(10), 
  CONSTRAINT unique_combinacion UNIQUE (nombre, apellido, matricula), 
  PRIMARY KEY (usuario_id)
); 
```

## Variables y funciones predefinidas de MYSQL

### Variables

* current_timestamp -> Contene el valor de la fecha y hora actuales

### Fuciones

* IF (10 > 90, , "10 es mayor que 90", "Diez no es mayor que noventa")
* IFNULL(field, 'El campo es nulo')

#### Para Strings

* CONTAC('HOLA', ' ', 'MUNDO') : Recibe n argumentos, estos pueden ser, Datos duros, variables o columnas. Retorna la concatenacion de los n valores, en este caso ->'HOLA MUNDO'. 
* LENGTH("hola mundo") : recibe un string y retorna la cantidad de caracteres en el mismo. 
* UPPER('hola') : Retorna -> 'HOLA'
* UPPER('HOLA') : Retorna -> 'hola'
* TRIM('    hola  mundo  '): Elimina los prefijos y sufijos de de una cadena de caracteres, por defecto. eliminara los espacio(' '). Esta ejemplo retorna -> 'hola mundo'
* LEFT('cadena', n) : Nos retorna los primeros n caracteres de la cadena comenzado de izquierda a derecha. 
* RIGHT('cadena', n) : Nos retorna los primeros n caracteres de la cadena comenzado de derecha a izquierda. 

#### Para numéros

* RAND() : Obtenemos un numero flotante entre 0 y 1
* ROUND( n ) : Esta funcion nos retorna n redondeado
* TRUNCATE(f, i) : Esta funcion nos retorna f que es de tipo flotante truncado con i decimales(i es un entero)
* POWER(b, e) o POW(b, e) : Nos retorna b elevado a la e. 

#### Para Fechas

* NOW() : Retorna un datetime con la fecha y hora actuales. 
* CURDATE(): Retorna un date con la fecha actual. 
* SECOND(datetime) : Recibe un valor de tipo datetime y retorna el segundo de este. 
* MINUTE(datetime) : Recibe un valor de tipo datetime y retorna el minuto de este. 
* HOUR(datetime) : Recibe un valor de tipo datetime y retorna la hora de este. 
* DAY(datetime) : Recibe un valor de tipo date ó datetime y retorna el dia de este. 
* MOUNTH(datetime) : Recibe un valor de tipo date ó datetime y retorna el mes de este. 
* YEAR(datetime) : Recibe un valor de tipo date ó datetime y retorna el año de este. 
* DAYOFWEEK(datetime) : Recibe un valor de tipo date ó datetime y retorna el dia de la semana en entero de este. 
* DAYOFMONTH(datetime) : Recibe un valor de tipo date ó datetime y retorna el dia del mes en entero de este. 
* DAYOFYEAR(datetime) : Recibe un valor de tipo date ó datetime y retorna el dia del año en entero de este. 
* DATE(datetime) : Recibe un valor de tipo datetime y retorna un date. 

**NOTA:** Nosotros podemos sumar o restar intervalos de tiempo a nuestros valores, esto lo asemos apoyandonos de la clausula *INTERVAL*. siguiendo la siguiente estructura: `fecha [+-] INTERVAL valor [SECOND MINUTE HOUR DAY WEEK MONTH YEAR]` . 
Ejemplo:

``` SQL
SELECT NOW() + INTERVAL 25 DAY; 
```

## Sentencias

A grandes rasgos las sentencias SQL se ejecutan de la siguiente manera. 

**NOTA:** Para este ejemplo se presume que el cliente ya esta autenticado. 

1. Se toma la sentencia(hasta el "; ") y se envia al servidor.
2. El servidor valida que el cliente tiene los permisos necesarios para ejecutar dicha sentencia.
3. El servidor valida que el cliente tiene los permisos necesarios para acceder a los datos solicitados.
4. El servidor valida la sintaxis de la sentencia
5. El servidor determina la forma mas optima de ejecutar el query(se ordenan tablas, se busca por indices, se trabaja con FK, etc.)
6. El resultado es eviado al cliente()

### Busqueda

La busqueda es de la sentencia mas comunes en SQL, esa en su estructura mas basica es asi: `SELECT field1, ...,fieldn FROM table_name;` . 

Ejemplo:

``` SQL
-- obtener una lista del pais de origen de los autores:
SELECT autor_id, pais_originen FROM autores;
-- obtener una lista con todos los datos de los autores:
SELECT * FROM autores;
```

**NOTA:** El caracter \* es para indicar que extraeremos todos los campos ó columnas. 

#### Alias

En ocaciones estaremos trabajaremos con columnas o trabajas con nombre bastante complejos, en cualquier coso podremos apoyarnos del keyword *AS* para crear un alias de las mias. Ejemplo:

``` SQL
SELECT fecha_publicacion AS fecha FROM libros AS lb; 
SELECT 9 * 10 AS resultado; 
```

**NOTA:** los alias de las tablas seran muy utiles cuando se hagan JOINS y setencias complejas. 

**NOTA:** Podemos crear alias sin la necesidad de escribir la palabra *AS* de la siguiente manera: `SELECT 9*10 resultado; ` . Sin embargo por cuestiones de legibilidad esto no es recomendado. 

#### Salida

El output por default de una consulta SQL es en forma de tabla. Nosotros podemos editar este y obtener nuestra respuesta en formato de carta si efectuamos el query de la siguiente manera:

``` SQL
SELECT * FROM autores; -- Formato de tabla
SELECT * FROM autores\G; -- Formato de carta o lista.
```

Este estilo de output(en carta) usualmente es utilixado cuando el resultado nos arroja muchas columnas, ya que de la otra manera el texte se saldra un poco del formato(Por el tamaño de nuestra consola). 

#### Clausula WHERE

Esta nos sirve para condicionar los resultados obtenidos de nuestra consulta, espeficicando el valor esperado en una de las columnas. Ejemplo:

``` SQL
SELECT nombre, apellido FROM autores WHERE autor_id = 1;
```

Los **signos de igual** que podemos utilizar son:

* Menor(<)
* Mayor(>)
* Menor igual(<=)
* Mayor igual(=>)
* Igual(=)
* Diferente(!= ó <>)
* <=> Seguridad(Es algo parecido al =)

**Operadores logicos**:

* AND -> Todas la condiciones deben ser verdaderas
* OR -> Basta con que se cumpla una de las condiciones
* NOT -> Negación

**IMPORTANTE** los campos nulos deben tratarse una maresa especial, ya que estos mas que como un valor se comportan como un tipo de de dato. Si quiereos obneter los registros con una determinada columna nula, deberemos ejecutar una setnencia como esta:

``` SQL
SELECT * FROM autores WHERE seudonimo IS NULL; 
-- ó
SELECT * FROM autores WHERE seudonimo <=> NULL; 
-- O si queremos obtener aquellos que NO son nulos, la sentencia seria:
SELECT * FROM autores WHERE seudonimo IS NOT NULL; 
```

##### Rangos

Cuando deseamos obtener registros entre un rango de valores, deberemos utilizar la clausula *BETWEEN AND*, siguiendo la siguiente estructura

``` SQL
SELECT titulo FROM libros WHERE fecha_publicacion BETWEEN "1995-01-01" AND '2015-12-31';
```

##### Listas

Cuando deseamos obtener registros entre una lista de valores, deberemos utilizar la clausula *IN*, siguiendo la siguiente estructura

``` SQL
SELECT titulo FROM libros WHERE id IN (1, 32, 33, 41, 53, 61); 
```

##### Busqueda en strings con LIKE

En caso de que necesitemos buscar un substring y no sabemos en que posicion exacta se encuentra de nuestra cadena, nos apoyaremos de la clausula *LIKE*, del comodin de multicaracteres *%* y el monocaracter *_*. Ejemplo:

``` SQL
-- Titulos que contienen la palabra 'potter'
SELECT * FROM libros WHERE titulo LIKE '%potter%';

-- Titulos que contengan 5 caracteres y el 3er caracter sea una 'b'
SELECT * FROM libros WHERE titulo LIKE '__b__';

-- Titulos que su segundo caracter sea la letra 'a'
SELECT * FROM libros WHERE titulo LIKE '_a%';

```

##### Expresiones regulares

Para utilizar regex en nuestras sentencias sql nos apoyaremos de la *REGEXP*, la complejita de la regex dependera de nuestras necesitades. Ejemplo:

``` SQL
-- Titulos que comienzan con H,O,L ó A.
SELECT * FROM titulo WHERE titulo REGEXP '^[HOLA]'
```

#### Unicos

Se puede dar el caso de que estemos los registros que estemos obteniendo esten duplicado(como es el caso de los titulos de lagunos libros) y solo queremos obtener resultados unicos en nuestras consultas. Esto lo hacemos apoyandones de la clausula *DISTINCT*, siguiendo la siguiente estructura:

``` SQL
SELECT DISTINCT titulo FROM libros;
```

#### Orden

Si queremos ordenar la salida de nuestra consulta utilizares la clausula *ORDER BY*. Ejemplo:

``` SQL
SELECT titulo FROM libros ORDER BY titulo;
```

**NOTA:** Por defecto el ordenamiento se hace de forma acendente, si queremos hacerlo de forma descendente o bien expresarlo de forma explicita nos apoyaremos de *ASC* y *DESC*, ejemplo: `SELECT titulo FROM libros ORDER BY titulo DESC;` 

**NOTA:** Si nosotros asi lo deseamos podemos ordenar nuestra salida por mas de un campo. Ejemplo: `SELECT * FROM libros ORDER BY libro_id AND titulo ASC;` 

#### Limitar salida

En la mayoria de los casos nosotros solo necesitaremos motrar un rango de nuestra consulta, eso lo haremos apoyandonos de la clausula *LIMIT*, esta recibe uno o dos parametros:

1. El offset: Indica el inicio del rango. **Si solo pasamos un valor, este por defecto sera 0(cero).**
2. El limite: No indica cuando registros vamos a extraer despues de offset.

Estructura:

``` SQL
SELECT * FROM table_name LIMIT offset, limit;
SELECT * FROM table_name LIMIT limit;
```

Ejemplo:

``` SQL
SELECT titulo FROM libros WHERE autor_id = 2 LIMIT 10;
```

#### Funciones de agregacion

La funciones de agregacion son ejecutadas a un conjunto de datos, es decir al resultado de una sentencia o consulta sql. 

Algunas funciones de agregacion son:

##### Contar

``` SQL
-- Cuenta todos los registros de nuestra tabla autores;
SELECT COUNT(*) FROM autores;

-- Cuenta todos los autores de USA:
SELECT COUNT(*) FROM autores WHERE pais_origen = "USA";
```

##### Sumar

``` SQL
-- Suma el total de venta de todos los libros:
SELECT SUM(ventas) FROM libros;
```

##### Maximo y minimo

``` SQL
-- Retorna el valor de ventas del libro con mas ventas
SELECT MAX(ventas) FROM libros;

-- Retorna el valor de ventas del libro con menos ventas
SELECT MIN(ventas) FROM libros;
```

##### Promedio

``` SQL
-- Retorna el promedio de ventas efectuadas
SELECT AVG(ventas) FROM libros;
```

#### Grupos

Habra ocaciones(como con las funciones de agregacion) que necesitaresmo trabajar con conjuntos de datos agrupados de alguna forma. Para esto nos apoyaremos de la clausula *GROUP BY* seguida del campo(o los campos) por el que deseamos agrupar los conjuntos. Ejemplo:

``` SQL
SELECT autor_id, SUM(ventas) AS total FROM libros GROUP BY autor_id ORDER BY total DESC LIMIT
```

#### Condicion bajo agrupamientos

Como las funciones de agregacion son ejecutadas una vez ya el servidor realizo la consulta, no podemos utilizar estas dentro de nuestra clausula *WHERE*, si necesitamos filtrar nuestros dados data una funcion de agregacion nos apoyaremos de la clausula *HAVING*. Ejemplo:

``` SQL
SELECT autor_id, SUM(ventas) AS total FROM libros GROUP BY autor_id HAVING SUM(ventas) > 100;
```

#### Unir resultados

Para unir resultados lo haremos de la siguiente manera:

``` SQL
SELECT CONTACT(nombre, " ", apellido) FROM autores
UNION
SELECT CONTACT(nombre, " ", apellidos) FROM usuarios;
```

**IMPORTANTE:** Todas las consultas deben retornar la misma cantidad de columnas. En caso que necesitemos realizar consultas con un numero columnas  diferentes podemos completar estas con columnas que contengan un string vacio(""). 
**NOTA:** Los encabezados mostrados seran los de la primera consulta

#### Subconsultas

Para realizar una consulta anidada o una subconsulta es tan sencillo como colocar esta dentro de parentesis, ejemplo:

``` SQL
SELECT
    autor_id
FROM libros
GROUP BY autor_id
HAVING SUM(ventas) > (SELECT AVG(ventas) FROM libros);
```

#### Uniones

A menudos necesitaremos obtener datos de dos tablas diferentes que comparten un dato en comun(FOREIGN KEY), la manera mas optima realizar estas consultas es a traves *JONIS*, existen 4 tipos principales: innner, left, right y outher que pueden ser extendidos a 7 como veremos a continuacion:

![Joins type](. /img/bases_de_datos/joins. jpg)


**NOTA:** en las sentencia siguientes podemos cambiar `ON libros.autor_id = autores.autor_id` por `USING(autor_id)`. Esto porque hemos seguido una buena normalizacion y estandar(o ese se supone) en nuestras tablas.
*USING* No es mas que un shortcut de la subclausula *ON*.

**NOTA:** Si asi lo deseamos con la subclausula *ON* podremos condicionar aun mmas la union de tablas, como por ejemplo:
``` SQL
SELECT *
  FROM libros
  INNER JOIN autores ON libros.autor_id = autores.autor_id
                        AND autores.seudonimo IS NOT NULL;

```


##### Izquierda

Si queremos obtener todos los elemenos de la tabla izquiera(incluyendo aquellos que no tenga un valor correspondiente en la tabla de la derecha). 

``` SQL
SELECT *
  FROM libros
  LEFT JOIN autores ON libros.autor_id = autores.autor_id
  -- Si queremos obtener solo los elementos que no estan incluidos en la tabla izquiera(libros) descomentamos la siguiente linea.
  -- WHERE autores.autor_id IS NULL
  ;
```

##### Derecha

Si queremos obtener todos los elemenos de la tabla derecha(incluyendo aquellos que no tenga un valor correspondiente en la tabla de la izquiera). 

``` SQL
SELECT *
  FROM libros
  RIGHT JOIN autores ON libros.autor_id = autores.autor_id
  -- Si queremos obtener solo los elementos que no estan incluidos en la tabla derecha(autores) descomentamos la siguiente linea.
  -- WHERE autores.autor_id IS NULL
  ;
```

##### Interno
Si queremos obtener solo los valores del conjunto que coincide entre las dos tablas:
``` SQL
SELECT *
  FROM libros
  INNER JOIN autores ON libros.autor_id = autores.autor_id;
```

##### Externo
Si queremos obtener todos los valores de la tabla nos apoyaremos del *LEFT JOIN*,*RIGHT JOIN* y de la clausula *UNION*.

##### Producto cartesiano
Para realizr un producto cartesiano entre dos tablas, lo haremos de la sigueitne manera:
``` SQL
SELECT usuarios.username, libros.titulo FROM usuarios CROSS JOIN libros;
-- ó
SELECT usuarios.username, libros.titulo FROM usuarios INNER  JOIN libros;
-- ó
SELECT usuarios.username, libros.titulo FROM usuarios, libros;
```

#### Validar si una consulta existe

``` SQL
SELECT IF(
    EXISTS(SELECT libro_id FROM libros WHERE titulo = 'El hobbit'),
    'Disponible',
    'No disponible'
) AS mensaje;
```

**NOTA:** Dentro de la consulta de la funcion EXISTS debemos ser muy cuidadosos del los campo a extraer, pues esto nos afectara en el rendimiento de la consulta. En este caso usamos una llave primaria(que es lo recomendado). 

### Actualizar

Si deseamos actualizar uno o varios registros seguiremos la siguiente estructura:
`UPDATE table_name SET field = Value, field2 = value WHERE ... ; ` 

``` SQL
UPDATE libros SET descripcion = "Nueva descripcion", ventas = 1502 WHERE libro_id = 41;
```

**NOTA:** Lo ideal es realizar las actualizacion utilizando la llave primaria, esto agilizara mucho el proceso de busqueda del registro. 

**NOTA:** Si no colocamos la clausula where se actualizaran todos los registros. 

### Eliminar

``` SQL
DELETE FROM libros WHERE libro_id = 43;
```

**NOTA:** Lo ideal es realizar sentencia utilizando la llave primaria, esto agilizara mucho el proceso de busqueda del registro. 

**NOTA:** Si no colocamos la clausula where se eliminaran todos los registros. 

#### Eliminacion en cascada

En ocaciones necesitremos eliminar registros que estan siendo referenciados por otras tablas(Como es el caso de la tabla autores que esta siendo referenciada en la tabla libros). Si nosotros queremos eliminar un autores, este no debe tener libros registrados, este es un proceso un poco tedioso en caso de que nos encontremos con varias tablas referenciadas. 

Es por ello que es recomendable colocarle un CASCADE al evento de DELETE( `ON DELETE CASCADE` ), esto lo hacemos en la definicion de la tabla de la siguiente manera

``` SQL
-- Cuando creamos la tabla
CREATE TABLE libros (

    libro_id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT, 
    autor_id INT UNSIGNED NOT NULL, 
    titulo VARCHAR(60) NOT NULL, 
    fecha_publicacion DATE NOT NULL, 
    descripcion VARCHAR(255)

    FOREIGN KEY (autor_id) REFERENCES autores(autor_id) ON DELETE CASCADE

); 

-- Si la tabla ya existe
ALTER TABLE libros ADD FOREIGN KEY (autor_id) REFERENCES autores(autor_id) ON DELETE CASCADE; 
```

### Restaurar

Si deseamos restaurar una tabla(borrar todos sus registros, dejandola como "nueva"). seguiremos la siguiente estructura: `TRUNCATE TABLE table_name;` . Ejemplo:

``` SQL
TRUNCATE TABLE libros;
```

-------------------------------------------------------------------------------

## Funciones

Al igual como si un lenguaje de programacion se tratase, en MYSQL podemos crear nuestras propias funciones. 

Algo interesante a tener en cuenta es que todas las funciones en MYSQL necesitan retornar un valor. 

### Crear

Para crear una nueva funcion debemos seguir la siguiente estructura:

``` SQL
DELIMITER caracter(es)

CREATE FUNCTION function_name(parameters1 type1, ..., parametersn type2) 
RETURNS return_type

BEGIN
  # CODE
  RETURN value
END caracter(es)

DELIMITER ;
```

Ejemplo:

``` SQL
DELIMITER //

CREATE FUNCTION agregar_dias(fecha DATE, dias INT)
RETURNS DATE
BEGIN
  RETURN fecha + INTERVAL dias DAY;
END//

-- Otra funcion, esta vez ejecutando sentencias dentro de ella:
CREATE FUNCTION obtener_paginas()
RETURNS INT
BEGIN
  SET @paginas = (SELECT (ROUND( RAND() * 100 ) * 4));
  RETURN @paginas;
END //

DELIMITER ;
```

### Listar

Para listar las funciones disponibles nos apoyaremos de la sentencia:

``` SQL
SELECT name FROM mysql.proc;
```

Si queremos listar solo las funciones declaradas en la base de datos que estamos usando actualmente, nos apoyaremos de la clausula *WHERE* de la siguiente manera: 

``` SQL
SELECT name FROM mysql.proc WHERE db = DATABASE() AND TYPE() = 'FUNCTION';
```

### Eliminar

Estructura:

``` SQL
DROP FUNCTION function_name;
```

Ejemplo:

``` SQL
DROP FUNCTION agregar_dias;
```

## Procedimientos
Los store procedure o procedimientos almanecedos son rutinas la cuales se ejucutan directamente en el motor de base de datos. En estas podemos realizar rutinas complejas asi como trabajar con grupos de datos y ciclos.

**IMPORTANTE:** CAda gestos de base de datos posee su propia forma de trabar con los Store procedure. Por lo que una vez creado los store procedure debemos seguir trabajando con el mismo gestor de base de datos.

### Crear
Para crear un procedimiento seguimos la siguiente estructura:
``` SQL
DELIMITER caracter(es)

CREATE PROCEDURE procedure_name(params_1 TYPE_1, ..., params_n TYPE_n)
BEGIN
    # CODE
END caracter(es)

DELIMITER ;
```

Ejemplo:

``` SQL
DELIMITER //

CREATE PROCEDURE prestamo(usuario_id INT,libro_id INT)
BEGIN
    INSERT INTO libros_usuarios(libro_id, usuarios_id) VALUES (libro_id, usuarios_id);
    UPDATE libros SET stock = stock -1 WHERE libros.libro_id = libro_id;
END//

DELIMITER ;
```

#### Retornar valores
Obtener valores de un procedimiento no es posible, pero si podemos editar una variable que recibimos como parametor, esto lo podemos hacer de la siguiente mantera:
``` SQL
DELIMITER //

CREATE PROCEDURE prestamo(usuario_id INT,libro_id INT, OUT cantidad INT)
BEGIN
    INSERT INTO libros_usuarios(libro_id, usuarios_id) VALUES (libro_id, usuarios_id);
    UPDATE libros SET stock = stock -1 WHERE libros.libro_id = libro_id;

    SET cantidad = (SELECT stock FROM libros WHERE libros.libro_id = libro_id);
END//

DELIMITER ;
```
**NOTA:** El argumento de "cantidad" debera ser una @variable, para posteriormente poderla consultar.
**NOTA:** Se parece mucho a los prodecimientos y su manera de setear valores en lenguajes de bajo nivel com Turbo Pascal. 

#### Condicionales
Para trabajar con condicionales en nuestros procedimientos lo haremos de la siguiente manera:
``` SQL
DELIMITER caracter(es)

CREATE PROCEDURE procedure_name(params_1 TYPE_1, ..., params_n TYPE_n)
BEGIN
    IF condicion_1 THEN
	# CODE_1
    ELSEIF condicion_2 THEN
	# CODE_2
    .
    .
    .
    ELSE
        # CODE_n
    END IF;

END caracter(es)

DELIMITER ;
```

Tambien podemos trabajar con *casos* en caso de que tengamos muchos opciones:
``` SQL
DELIMITER caracter(es)

CREATE PROCEDURE procedure_name(params_1 TYPE_1, ..., params_n TYPE_n)
BEGIN
    CASE
	WHEN condition_1 THEN
	    # CODE_1
	.
	.
	.
	WHE condition_n THEN
	    # CODE_n

    END CASE
END caracter(es)

DELIMITER ;
```

#### Ciclos
Para trabajar con ciclos en los procedimientos los haremos de la siguiente manera:
``` SQL
DELIMITER caracter(es)

CREATE PROCEDURE procedure_name(params_1 TYPE_1, ..., params_n TYPE_n)
BEGIN

-- Ciclo While
    WHILE condition DO
	#CODE of while
    END WHILE;
-- Ciclo Repeat
    REPEAT
	#CODE of repeat
        UNTIL condition
    END REPEAT;
END caracter(es)

DELIMITER ;
```

**NOTA:** Seguramente las variable sera algo que te sirva mucho en este modulo

**NOTA** poco relevante: Me llama un poco la atencion la similitud que hay entre SQL y Pascal.

### Errores
Dentro de los store procedure podemos declarar un modulo para realizar ciertas acciones en caso de que ocurra un error dentro del procedimiento. Esto lo hacemos de la siguiente manera:

``` SQL
DELIMITER caracter(es)

CREATE PROCEDURE procedure_name(params_1 TYPE_1, ..., params_n TYPE_n)
BEGIN
    DECLARE EXIT HANDLER FOR SQLEXCEPTION -- Si ocurre un error
    BEGIN
	# CODE
    END;
    # SQL CODE
END caracter(es)

DELIMITER ;
```

### Ejecutar
Para ejecutar un procedimiento es tan sencillo como `CALL procedure_name(arg_1, ..., arg_n);`. Los argumentos son en caso de que el procedimiento tenga parametros definidos.

### Listar
Para listar los procedimientos asociados a nuestra base de datos ejecutaremos:  
``` SQL
SELECT name FROM mysql.proc WHERE db = DATABASE() AND type = "PROCEDURE";
```

### Eliminar
Eliminar un procedimiento basta con ejecutar `DROP PROCEDURE procedure_name;`

### Editar
Lamentablemente no es posible editar un procedimiento, debemos eliminarlo y volverlo a crear con los nuevos ajustes. 

## Vistas
Podemos ver a las vista como una consulta definica por el admin que sera usuda periodicamente. Este luego de creada se comporta de manera muy similar a una tabla(Al menos en el sentido de como hacer consultas sobre ella).

### Crear
Para crear una vista es muy sencillo, solo deberemos seguir la siguiente estructura `CREATE VIEW view_name AS consulta`. Siendo "consulta" del tipo `SELECT ...;`

**NOTA:** Es importante crear y mantener un estandar en los nombres de nuestras vista(por ejemplo colocarle view o vw al inicio o al final, ya que estas se listan como tablas, pero en realidad no lo son. Son vistas)

### Editar
Para editar una vista seguimos la estructura: `CREATE OR REPLACE VIEW view_name AS consulta;`

### Eliminar
Para eliminarla ejecutamos `DROP VIEW view_name;`

## Transacciones
Una transaccion explicada de una forma sencilla se puede ver como envolver varias sentencias en una sola. Dicho de otra manera, o todas las sentencias se ejecutan de forma correcta o ninguna se ejecutara, ya que podremos regresar al estado de la tabla al comenzar la transaccion. Para crear una trasaccion seguimos la siguiente estructura:
``` SQL
START TRANSACTION;
    # SQL CODE
-- Si todo va bien
COMMIT; -- Cofirmamos cambios y finalizamos la transaccion

-- Si algo falla
ROLLBACK; -- Finalizamos la transaccion sin confirmar los cambios.
```  

**NOTA:** Un uso muy comun de las transacciones es dentro de Store Procedures, de esta manera podemos colocar un *rollback* dentro del majeno de errores del procedimiento.

## Motores
Un motor de almacenamiento se el encargado de almacenar, gestionar y recuperar toda la información de una tabla.

MySQL nos permite trabajar con diferentes motores de almacenamiento, entre los que destacan *MyISAM* e *InnoDB*.

Para que nosotros conozcamos que motor de almacenamiento podemos utilizar basta con ejecutar la siguiente sentencia en nuestra terminal. `SHOW ENGINES;`

Obtendremos un listado
- InnoDB
- MRG_MYISAM
- MOMORY
- BLACKHOLE
- MyISAM
- CSV
- ARCHIVE
- PERFORMANCE_SCHEMA
- FEDERATED

### Gestion

Si nosotros así lo deseamos podemos cambiar el motor de almacenamiento. Existen dos formas de hacer esto. La primera, es modificar el archivo my.cnf.

``` CNF
[mysqld]
default-storage-engine = innodb
```

La segunda forma es hacerlo directamente desde nuestra sección, basta con ejecutar la siguiente sentencia. `SET storage_engine=INNODB;`.

En ambos casos para este ejemplo modificamos el motor de almacenamiento de MyISAM a InnoDB.

---
Si nosotros deseamos conocer qué motor de almacenamiento utiliza una tabla en particular, podemos hacerlo ejecutando la siguiente sentencia.

``` SQL
SHOW TABLE STATUS WHERE `Name` = 'tabla' \G;
```

Si deseamos crear una tabla utilizando un motor en particular, debemos seguir la siguiente estructura.
``` SQL
CREATE TABLE tabla_innodb (id int, value int) ENGINE=INNODB;
CREATE TABLE tabla_myisam (id int, value int) ENGINE=MYISAM;
CREATE TABLE tabla_default (id int, value int);
```

### MyISAM
Es el motor por default de MySQL. Una de las principales ventajas de este motor es la velocidad al momento de recuperar información. MyISAM es una excelente opción cuando las sentencias predominantes en nuestra aplicación sean de consultas, debido a que este no hace un bloqueo de tablas cuando consultamos registros. Esta es una de las razones por las cuales MyISAM es tan popular en aplicaciones web.

Si tu aplicación necesita realizar búsquedas full-text MyISAM es un mejor opcion.

La principal desventajas de *MyISAM* recae en la ausencia de atomocidad, ya que no se comprueba la integridad referencial de los datos. Se gana tiempo en la inserción, sí, pero perdemos confiabilidad en los datos.

### InnoDB
La principal ventaja de este motor recae en la seguridad de las operaciones. InnoDB permite la ejecución de transacciones, esto nos garantiza que los datos se persisten de forma correcta y si existe algún error podamos revertir todos los cambios realizados.

Algo interesante a mencionar sobre InnoDB es que este motor realiza un bloqueo total sobre un tabla cuando es ejecutada una se las siguientes sentencias: Select, Insert, Update y Delete.

Si deseamos trabajar con transacción y la integridad de los datos sea crucial nuestra mejor opción será InnoDB.

# Formas normales en DB relacionales

La normalización en las bases de datos relacionales es uno de esos temas que, por un lado es sumamente importante porque nos apoya no tener datos duplicados ni compuestos en nuestra DB y por el otro suena algo esotérico. Vamos a ver las formas normales (FN) de una manera simple para aplicarlas futuros proyectos. 

## Primera Forma Normal (1FN)

Esta FN nos ayuda a eliminar los valores repetidos y no atómicos dentro de una base de datos. 

Formalmente, una tabla está en primera forma normal si:

* Todos los atributos son atómicos. Un atributo es atómico si los elementos del dominio son simples e indivisibles. 
* No debe existir variación en el número de columnas. 
* Los campos no clave deben identificarse por la clave (dependencia funcional). 
* Debe existir una independencia del orden tanto de las filas como de las columnas; es decir, si los datos cambian de orden no deben cambiar sus significados. 

Se traduce básicamente a que si tenemos campos compuestos como por ejemplo “nombre_completo” que en realidad contiene varios datos distintos, en este caso podría ser “nombre”, “apellido_paterno”, “apellido_materno”, etc. 

También debemos asegurarnos que las columnas son las mismas para todos los registros, que no haya registros con columnas de más o de menos. 

Todos los campos que no se consideran clave deben depender de manera única por el o los campos que si son clave. 

Los campos deben ser tales que si reordenamos los registros o reordenamos las columnas, cada dato no pierda el significado. 

## Segunda Forma Normal (2FN)

Esta FN nos ayuda a diferenciar los datos en diversas entidades. 

Formalmente, una tabla está en segunda forma normal si:

* Ésta en 1FN. 
* Sí los atributos que no forman parte de ninguna clave dependen de forma completa de la clave principal. Es decir, que no existen dependencias parciales. 
* Todos los atributos que no son clave principal deben depender únicamente de la clave principal. 

Lo anterior quiere decir que sí tenemos datos que pertenecen a diversas entidades, cada entidad debe tener un campo clave separado. Por ejemplo:
