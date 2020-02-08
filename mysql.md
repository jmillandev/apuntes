# Instalacion

Para realizar la instalación de MySQL en tu pc lo primero que debes tener en cuenta es que debes hacer la verificación de la versión que quieres instalar y la distribución para tu sistema operativo. En este enlace encuentras el listado de las plataformas soportadas.

## Windows

Si estas trabajando con Windows puedes hacer la descarga ingresando en el siguiente [enlace](https://dev.mysql.com/downloads/installer/). Este es el sitio oficial de MySQL por lo que puedes confiar en la descarga.

El instalador para Windows es muy similar a los que ya conocemos, nos pide algunas verificaciones y nos permite navegar a través de diferentes ventanas.

Inicialmente el instalador nos va a solicitar que aceptemos la los términos y acuerdos de la licencia. Revisalos y si estas de acuerdo continua.

En seguida te va a solicitar información relacionada con el tipo de instalación que vas a realizar, puedes elegir entre Developer Default, Client Only y Full. Cualquiera que sea la opción que elijas esto no implica que luego puedas actualizarla.

Si instalas la versión Full vas a tener acceso a todas las características y productos que MySQL ofrece.

Verifica que tengas disponibles todos los requerimientos que el instalador te presenta. En caso de no contar con ellos debes descargar e instalar el software solicitado.

Continua con la instalación de acuerdo a lo que te indica el ayudante.

## Mac

En nuestro caso vamos a estar trabajando con MySQL en Mac por lo que haremos la instalación en este sistema operativo.

Para instalar MySQL usando el instalador del paquete:

Descarga el archivo de imagen del disco ( .dmg ) que contiene el instalador del paquete MySQL. No es necesario tener una cuenta en Oracle para realizar la instalación pero es recomendable hacerlo.

Haz doble clic sobre el archivo para montar la imagen y ver su contenido.

Esto te va a mostrar el asistente de instalación de MySQL. El SO puede preguntarte si confías en el origen de este programa, puedes darle continuar hasta que llegues al installation type puedes hacer clic en Instalar para ejecutar el asistente de instalación utilizando todos los valores predeterminados, o puedes hacer clic en Personalizar para modificar qué componentes instalar (servidor MySQL, Prueba de MySQL, Panel de preferencias, Soporte inicializado; todas las pruebas excepto MySQL están habilitadas por defecto). En este caso esta bien que instalemos con los valores por defecto.

Selecciona el tipo de cifrado de contraseñas que vas a usar para tu base de datos.

Ingresa una contraseña que no se te vaya a perder u olvidar, porque es la contraseña de tu usuario root para la base de datos.

En este punto ya tienes instalado tu servidor de MySQL y puedes continuar con el curso.

## Linux Debian

Tutorial sencillo para los usuarios de Linux:

Se instala el servidor y cliente de mysql.
´$ sudo apt-get install mysql-server mysql-client´

Accedes a la base de datos de mysql.
´> usemysql;´

Creas un nuevo usuario.
´> create user 'tuNombreDeUsuario'@'localhost' identified by'tuContraseña';´

Modificas las siguientes configuraciones de tu usuario.
´´´
> grant allprivileges on *.* to  'tuNombreDeUsuario'@'localhost';
> update user set plugin="auth_socket" where User= 'tuNombreDeUsuario';
> flush privileges;
´´´
Listo, ya tienes los privilegios para acceder utilizando el comando 
´mysql -u ‘tuNombreDeUsuario’ -p´

# Conexcion a la BD
A traves de la terminal es la manera mas optima de acceder a la base de datos, esto lo hacemos atraves del siguiente comando.
´mysql -u root -h localhost -p´

Banderas:

- -u :Nombre del usuario
- -h :Nombre del host
- -p :Contraseña

# Comandos
**Importante:** Recordar colocar el punto y coma (;) al final de cada instruccion.

## Mostrar
Muestra o lista aquello que le indiquemos.

Ejemplo:
´´´
show databases;
show tables;
´´´

## Usar
Para seleccionar la base de datos donde trabajaremos usamos el comando use. Ejemplo:

´use nameDataBase;´

# Restricciones

## Tipos de datos
1. INTEGER
2. VARCHAR(LENGTH)
3. YEAR
4. Double(digitos,decimales)
5. TINYINT : Es un Byte
6. TEXT
7. DATETIME
8. TIMESTAMP
9. ENUM('option1', 'option2', 'optionN')


## Otros
- DEFAULT: asigna el valor por defecto del campo.
- PRYMARY KEY : indica que este campo contiene una llave primaria.
- AUTO_INCREMENT: Este campo tiene autoincremento.
- UNSIGNED: el numero es sin signo( >0 ) por lo que almacena numeros mayores(una potencia de 2 mas).
- NOT NULL: El campo no acepta nulos.
- UNIQUE
- CURRENT_TIMESTAMP: El valor retornado es la hora del sitema medida desde el 01/01/1970.
- ON UPDATE

