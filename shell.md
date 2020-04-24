# Lista de comandos más usados
## Conceptos
- PROMPT: Donde se encuentra el cursor, un lugar en el árbol de nodos que es la
representación del disco duro en el sistema operativo
## Comandos (y algunas banderas)
- **whoami**: Imprime en el output el identificador de usuario.

- **id**: Imprime en el output el identificador de usuario  grupos.

- **who/finger**: Quien esta registrado.

- **w**: Quien esta registrado y que hace.

- **date**: Fecha y hora.

- **cal**: Calendario del mes.

- **hostname**: nombre de la maquina.

- **ls**: lista los contenidos de un directorio
    - -l: lista los archivos con datos de cada nodo, ordenados alfabéticamente
    - -S: lista los contenidos ordenados por tamaño
    - -h: lista los contenidos mostrando los datos legibles fácilmente (tamaño)
    - -r: lista los archivos ordenados de forma inversa (sirve con las banderas S y t)
    - -a: lista los contenidos de un directorio incluyendo los archivos ocultos.
    - -i: Lista los contenidos de un directorio incluyendo el identificador del nodo i(nodo indice).
    - -t: Lista los contenidos por orden de hora/fecha de ultima modificacion. Primero el mas reciente.

- **tree**: lista recursivamente la estructura de árbol de un directorio incluyendo tanto archivos como directorios (**NOTA:** No viene pre-instalado así que hay que instalarlo primero con su administrador de paquetes preferido: para RHEL/CentOS/Fedora `yum install tree` para Debian/Mint/Ubuntu `apt-get install tree`, para OS X `brew install tree`)

    - -L 1: muestra recursivamente la estructura de árbol de un directorio pero sólo hasta el primer subnivel de directorios.
    - -a: muestra recursivamente la estructura de árbol de un directorio incluyendo tanto archivos como directorio ocultos.
    - -d: muestra recursivamente la estructura de árbol de un directorio tomando en cuenta sólo los directorios

- **rm** [FILE]: elimina un archivo
    - -r [DIRECTORY]: elimina un directorio recursivamente.
    - -f [FILE]: elimina un fichero sin preguntar.

- **mv** [FILE] [DIRECTORY]: mueve FILE a DIRECTORY. (**NOTA:** Sirve para renombrar archivos o directorios)

- **file** [FILE]: Muestra el tipo del fichero.

- **cd** [DIRECTORY]: lleva el PROMPT a DIRECTORY

- **touch** [FILE]: si FILE existe, modifica la hora de última modificación al momento de la ejecución del comando, si FILE no existe, lo crea

- **ln** -s [DIRECTORY] [NAME]: crea un _link_ simbólico llamado NAME hacia DIRECTORY, NAME se comporatará como DIRECTORY

- **tail** [FILE]: muestra las últimas 10 lineas de un archivo de texto
    - -f [FILE]: tail _forever_, en principio muestra las últimas 10 líneas de FILE, pero mantiene abierto el archivo e imprime los cambios que se vayan escribiendo (secuencialmente) en éste, muy útil para _logs_.

- **more** [FILE]: muestra el contenido de un archivo de texto de forma páginada

- **cat** [FILE]: imprime todo el contenido de un archivo en pantalla.

- **clear**:limpia la terminal.([CTRL] + L)

- **pwd**: imprime o muestra la ruta actual donde nos encontramos ubicados

- **man** [COMANDO]: muestra la documentacion de todos los comandos
    - -k [KEY_WORDS]: muestra las entradas del manual donde aparecen alunas de las entradas clave.

- **mkdir** [DIRECTORY]: crea un directorio en la ubicación actual
    - -p [RUTA]: crea un árbol de directorios completo que no existe

- **cp** [archivo/directorio origen] [archivo/directorio destino]: copia un archivo o directorio desde un origen a un destino.
    - -r [directorio origen] [directorio destino]: copia un directorio y todos sus directorios hijos de
forma recursiva

- **xdg-open** [-a APP] [ FILE | DIRECTORY ]: abre el (archivo o directorio) con la aplicación por defecto en el sistema operativo, si se manda la bandera -a usará la APP para abrirlo.

- **which** [COMAND]: Retorna el PATH absoluto de [COMAND].

- **find** [PATH] [OPTIONS]: Busca ficheros a partir de PATH.
    - -name: Nombre del fichero.
    - -mtime: Delta de la fecha de modificacion del fichero.

- **grep** [PATTERN] [PATH]: Busca segun un patron en un fichero o path.
    - -w: Busca una palabra aislada. 
    - -v: Retorna las lineas que no coinciden con el patron.
- **diff** [FILE1] [FILE2]: Muestra las diferencias entre dos ficheros linea a linea.

- **wc** < [FILE] : Word Count, Retorna el numero de lineas, de palabras y de caracteres contenidos en FILE.
    - -l :Retorna solo el numero de lineas.

# Composicion de comandos:
## Secuencia de comando
command_1; command_2

Ejem: `date; who`

## Encadenamientos de comandos (operador | (pipe))
command_1 | command_2
Manda el STDOUT de command_1 al STDIN de command_2

# Operadores para STDIN, STDOUT/STDERR
Los numero de dichos ficheros son:
- 0: STDIN
- 1: STDOUT
- 2: STDERR

## operador >
command_1 > FILE
Manda el STDOUT de command_1 al inicio de FILE. Si FILE no existe lo crea, si existe lo
sobreescribe.
## operador >>
command_1 >> FILE
Manda el STDOUT de command_1 al inicio de FILE. Si FILE no existe lo crea, si existe lo
concatena al fina (tras un _newline_).

**NOTA**: >>! Crea el fichero si este no existe.

## operador <
command_1 < FILE
Manda al STDIN de command_1 el contenido de FILE.
## redirección de salidas
1. command > FILE - manda el STDOUT a FILE
1. command 1> FILE 2>FILE_ERROR - manda el STDOUT a FILE y el STDERR a
FILE_ERROR
1. command > FILE 2>&1 - manda, tanto el STDOUT como el STDERR a FILE
1. command >> FILE 2>&1 - manda a concatenar las salidas de STDOUT y STDERR a FILE

# Variables:
Son **cadenas** de 0 o mas caracteres.

Un identificador de variabble puede ser cualquier palabra que comience con una lera y continúe con letras, dígitos, y el carácter '_'.

## Uso de Variable:
### Asignacion
En *sh* o *bash*:

`nombre=manu`

**NOTA:** La asignacion no debe contener caracteres en blanco(' ').

### Uso
```shell
echo $nombre
echo "${nombre} perez"
# manu perez
echo "${nombre}el perez"
# manuel perez
```

## Tipos de Variables

### Ordinarias
Variables locales de proposito general.

### Variables de entorno
Describe el context de ejecucion y se heredan.

Algunas variables de entorno son:

- TERM: Tipo de terminal.
- PATH: Lista de directorios por defecto para busqueda de comandos.
- HOSTNAME: Nombre de la maquina.
- USER: Nombre de usuario actual.
- SHELL: Shell por default.
- HOME: Directorio base de usuario.
- etc

#### Asignacion en variables de entorno
```shell
TERM=vt100; export TERM
PATH=$PATH:/home/jgmc3012; export PATH
export PATH=$PATH:/home/jgmc3012
```

#### Consulta de variables(sh y bash)
```shell
echo $PATH
printenv # Lista todas la variable del entorno
```

### Variables especiales de la shell
Configuran el entorno de la propia shell.
    - Variables para párametros en la invocacion de comandos.

#### Variables Posicionales
Albergan los parametros de entrada a los comandos

La estructura es la siguiente
<comando> <arg1>
$0 $1

```shell
ls -la ~/Downloads
# $0=ls
# $1=-la
# $2=Downloads
```

## Evaluacion de variables
```shell
var #Valor de la variable var si esta esta definida.
{var} #Lo mismo pero delimita el nombre de la variable cuando esta insertada en una cadena mayor.
{var-valor} #Valor de la variable var, si esta definida. Si no se usa valor.
{var=valor} #Valor de la variable var, si esta definida. Si no se usa valor y se asigna valor a var.
{var?mensaje} #Valor de lavariable var, si esta definida. Si no imprime un mensaje y espera un valor para la varaible proporcianado interactivamente.
{var+valor} #Usa valor si la variable var esta difinida.
```

# Metacaracteres
- *: Coincide con cualquier cadena.
- ?: Coincide con un caracter.
- [xyz]: Uno de los caracteres del conjunto.
- [a-z]: Uno de los caracteres del rango.
- \c: Coincide con c literalmente.
- 'cadena': Coincide con una cadena literalmente.
- "cadena": Coincide con una cadena literalmente salvo variables de shell que se susituyen por su valor.

**SOLO DE USO EN CASE:**
- patron1|patron2 : Coincide con uno(cualquiera) de los dos patrones.


# Inicializacion de la Shell
Cuando se ejecuta una shell interactiva esta ejecuta unos scripts de inicializacion que asignan valores predeterminados por el usuario para variables especiales y de entorno, y ejecutan comandos.

Estos ficheros siver para particularzar la session a los gustos y necesidades de cada usario.

## En bash
Algunos ficcheros para la particularizacion de inicio y fin de sesion.

- /etc/profile: Inicializacion global para login shells.

- /etc/basrc: Configuracion global.

- $HOME/bash_profile: Se ejecuta al comienzo de sesión.

- $HOME/.bashrc: Ejecuta al comienzo de una shell

- $HOME/.bash_logout: Particularizar el fin de sesión.

# Combinación de teclas como comandos

1. [ctrl]-C - este comando termina el proceso que se esté ejecutando en la terminal, haya o no
acabado de ejecutarse.
2. [ctrl]-D - el sistema lo interpreta como _EOF_ (End Of File) y cierra el _stream_ de entrada
(STDIN) para un archivo en donde se esté escribiendo desde la terminal.

# Programacion en Shell

## Estructura
Los shell scripts son script de alto nivel y permiten la utilizacion de una estructura bastante comun en lenguajes de programacion:

### Bucles.
### Interaciones.
### Bifurcacion.
Tenemos dos casos:
1. CASE:
**NOTAS:**
- El comando de cierre es 'case' al reves es decir esac.
- La lista de comando termina con un ';;'
- La lista de comando esta separada por  newline o ';'
- Los patrones especifican un conjunto de cadenas.
- valor, Suele ser del tipo $variable.
- El ultima patron suele ser *, para indicar una accion por defecto.

```shell
case valor in
    patron1) lista de comnados 1;;
    patron2) lista de comandos 2;;
    ....
    patronN) lista de comando n;;
esac
```

2. If
```shell
If condicion
then
    lista de comandos 1
elif
    lista de comando 2
...
else
    lista de comando n
fi
```
Las comprobaciones se realizan con el comando `test` de las siguiente manera

```shell
test condition
[ condition ]

# Ambas sentencias son analogas. Fijese en los dos espacios en blancos en ls lados internos de los [], Estos son de vital importancia.
```
#### Comprobaciones con test
Evalua una condicion devuelve un **cero** como un valor **verdadero**. En caso de una condicion falsa devuelve un valor distinto de 0.

1. Comprobaciones de ficheros:

- -d [FICHERO]: El fichero existe y es un directorio
- -f [FICHERO]: El fichero existe y es un fichero
- -r [FICHERO]: El fichero existe y tiene permisos de lectura
- -s [FICHERO]: El fichero existe y tiene una longitud mayor a cero
- -w [FICHERO]: El fichero existe y tiene permisos de escritura
- -x [FICHERO]: El fichero existe y tiene permisso de ejecucion

2. Comprobaciones para cadenas:

- cadena: cadena no nula
- -n cadena la cadena es de longitud mayor a 0.
- -z la cadena es de longitud 0.
- cadena 1 = cadena2:  Las dos cadenas son identicas
- cadena 1 != cadena2:  Las dos cadenas no son identicas

3. Comprobaciones con enteros.

- n1 -eq n2 : n1 es igual a n2
- n1 -neq n2 : n1 no es igual a n2
- n1 -gt n2 : n1 es mayor que n2
- n1 -lt n2 : n1 es menor que n2
- n1 -le n2 : n1 es menor o igual que n2

4. Expresiones:

- ! expr : Negacion de una exprecion
- (...) : Agrupacion de expresiones.
- e1 -a e2 : And logico
- e1 -o e2 : Or logico.

### Definicion de funciones.
### Evaluacion de expreciones.
### Manejo de I/O.
### Manejo de interrucciones y control de procesos.

## Pasos para hacer un shell script
1. Editar el fichero:
`vim script`

2. Dar permisos de ejecucion la fichero:
`chmod +x script`

3. Ejecutar y probar el script: el parametro -x es para hacer debug
`bash -x script [opciones] [argumentos]`

4. Usar el script:
`script [opciones] [argumentos]`

## Variables:
Ademas de las variables posiciones a las cuales podemos acceder haciendo uso de: $0 $1 $2 ... $n.

Podemos hacer uso de un grupo de variables especiales:
- $* : Une todos los argumentos en un unico string

- $? : El valor de retorno del ultimo comando ejecutado(Esto nos ayuda a saber si fue exitoso o tuve un problema)

- $# : Contine el numero de argumentos en decimal.

## Construccion del script:
La primera de las lineas del script es muy especial, esta contiene en path del interprete de dicho script precedido por los caracteres '#!'.

`#!/bin/bash`
