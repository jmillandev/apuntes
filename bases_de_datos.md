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

Descarga el archivo de imagen del disco ( .dmg ) que contiene el instalador del paquete MySQL. No es necesario tener una cuenta en Oracle para realizar la instalación pero es recomendable hacerlo.

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

Para ejecutar ficheros con la extension *.sql*, seguimos la siguiente estructura.

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

## Restablecer contraseña de root MySQL

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

Para obtener datos de nuestro servidor es muy sencillos. Para esto utilizamos la palabra reservada.*SELECT*

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

En este caso la columna podrá almacenar hasta tres dígitos como enteros y dos después del punto decimal. Ejemplo: *Ejemplo 999.99*

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

## Variables y funciones de MYSQL

### Variables

* current_timestamp -> Contene el valor de la fecha y hora actuales

### Fuciones

* NOW() -> Retorna la fecha y hora actuales.

## Sentencias

A grandes rasgos las sentencias SQL se ejecutan de la siguiente manera.

**NOTA:** Para este ejemplo se presume que el cliente ya esta autenticado.

1. Se toma la sentencia(hasta el "; ") y se envia al servidor.
2. El servidor valida que el cliente tiene los permisos necesarios para ejecutar dicha sentencia.
3. El servidor valida que el cliente tiene los permisos necesarios para acceder a los datos solicitados.
4. El servidor valida la sintaxis de la sentencia
5. El servidor determina la forma mas optima de ejecutar el query(se ordenan tablas, se busca por indices, se trabaja con FK, etc.)
6. El resultado es eviado al cliente()


### Alias
En ocaciones estaremos trabajaremos con columnas o trabajas con nombre bastante complejos, en cualquier coso podremos apoyarnos del keyword *AS* para crear un alias de las mias. Ejemplo:
``` SQL
SELECT fecha_publicacion AS fecha FROM libros AS lb;
SELECT 9 * 10 AS resultado;
```
**NOTA:** los alias de las tablas seran muy utiles cuando se hagan JOINS y setencias complejas.

**NOTA:** Podemos crear alias sin la necesidad de escribir la palabra *AS* de la siguiente manera: `SELECT 9*10 resultado;`. Sin embargo por cuestiones de legibilidad esto no es recomendado.


### Salida

El output por default de una consulta SQL es en forma de tabla. Nosotros podemos editar este y obtener nuestra respuesta een formato de carta si efectuamos el query de la siguiente manera:

``` SQL
SELECT * FROM autores; -- Formato de tabla
SELECT * FROM autores\G; -- Formato de carta o lista.
```

Este estilo de output(en carta) usualmente es utilixado cuando el resultado nos arroja muchas columnas, ya que de la otra manera el texte se saldra un poco del formato(Por el tamaño de nuestra consola).

### Clausula WHERE

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

#### Rangos

Cuando deseamos obtener registros entre un rango de valores, deberemos utilizar la clausula *BETWEEN AND*, siguiendo la siguiente estructura

``` SQL
SELECT titulo FROM libros WHERE fecha_publicacion BETWEEN "1995-01-01" AND '2015-12-31';
```

#### Listas

Cuando deseamos obtener registros entre una lista de valores, deberemos utilizar la clausula *IN*, siguiendo la siguiente estructura

``` SQL
SELECT titulo FROM libros WHERE id IN (1, 32, 33, 41, 53, 61); 
```

#### Unicos

Se puede dar el caso de que estemos los registros que estemos obteniendo esten duplicado(como es el caso de los titulos de lagunos libros) y solo queremos obtener resultados unicos en nuestras consultas. Esto lo hacemos apoyandones de la clausula *DISTINCT*, siguiendo la siguiente estructura:

``` SQL
SELECT DISTINCT titulo FROM libros;
```


### Actualizar
Si deseamos actualizar uno o varios registros seguiremos la siguiente estructura:
`UPDATE table_name SET field = Value, field2 = value WHERE ...;`
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

Es por ello que es recomendable colocarle un CASCADE al evento de DELETE(`ON DELETE CASCADE`), esto lo hacemos en la definicion de la tabla de la siguiente manera

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

-------------------------------------------------------------------------------

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

