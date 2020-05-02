Es un editor desarrolado para CLI, es decir que solo podemos interactuar con el por medio del teclado. O al menos ese es el objetivo.

**NOTA:** Cuando hacemos referencia a algo como [i]. Nos referimos a que debe teclear la letra i desde el modo comando.

# Modos

## Normal
Aca podemos utilizar conbinaciones de teclas y cambiarnos a cualquiera de los otros modos. Este es el modo central siempre podemo volver a el pulsando [ESP]

## Insercion:

Es el modo en el que podemos introducir texto. Se puede entrar a este modo desde el modo normal. utilizando alguno de los siguientes atajos.

- Antes del cursor: [i].
- Delante del cursor: [a].
- Al comienzo de una nueva linea(crea la nueva linea): [o].
- Final de la linea: [A].
- Modo Reemplazar: desde el modo normal tecleamos: [R]
- Reemplazar un caracter: situados sobre el caracter en modo normal [r]
- Reemplazar caracter y seguir en modo inserción: [s]

## Comando
A este modo se accede pulsando [:], se escriben comandos, y se ejecutan pulsando [ENTER]. 
También podremos personalizar aspectos de Vim para esa sesión, ya que no quedarán guardados los cambios permanentemente.

## Algunos comandos
: **informacion detallada de cada comando**

- `:[rango]d[elete]`: **borra** el rango de lineas.
- `:[rango]y[ank]`: **copia** el rango de lineas.
- `:[linea]put`: **pega** el texto en la linea descrita.
- `:[rango]co[py] {dirección}`: **copia** las líneas especificadas debajo de la dirección tambien se el invoca pulsando `:t`.
- `:[rango]m[ove] {dirección}`: **mueve** líneas espeficicadas **a la dirección** elegida.
- `:[rango]j[join]`: **junta** lineas.
- `:[rango]norm[al] {comando}`: **ejecuta comando de modo normal** en las lineas espeficicadas.
- `:[rango]s[ubstitute]/{pattern}/{string}/[flags]` **Reemplaza las ocurrencias** de {pattern} con {string} en cada línea espeficicada.
- `:[rango]g[lobal]/{pattern}/[comando]`: **ejecuta un comando** en cada línea espeficicada que coincidan con el **patrón de búsqueda** {pattern}.
- `:[rango]p[rint]`: nos **muestra** el rango.
- `:h`: **informacion detallada de cada comando**

**Lineas en VIM**:
Como Vim nombra algunas lineas:
- `1`: **Primera línea del archivo**-
- `$`: Última linea del archivo.
- `0`: No existe la linea 0. Se utiliza para mover o pegar texto encia de la primera linea.
- `.`: Es la linea donde esta ubicado el cursor.
- `'m`: **La linea que contiene la marca** m
- `'<`: Inicio de la **seleccion visual**, `'>`: final de la **selección visual**. Si seleccionamos unas lineas en modo visual y seguido pulsamos `:` ** se creará el siguiente rango automaticamente. `:'<'>`.
- `%`: **Todo el archivo**, un atajo para el rango `:1,$`
- `+n`: **N lineas por debajo** del cursor.
- `-n`: **N lineas por arriba** del cursor.


## Visual
Es como seleccionar texto con el cursor en otros editores, solo que podremos escribir comandos para manipularlo.

Existen tres variantes del modo visual:
1. Por caracteres y palabras: Ingresamos mediante [v].
2. Por lineas: Ingresamos mediante [V]
3. Por bloques restangulares: Ingresamos mediante [^v].

### Subcomandos
Esta acciones tendran efecto solo en el texto que tengamos seleccionado.
- Eliminar e insertar: [c].
- Pasar a mayusculas: [U].
- Pasar a minisculas: [u].
- Alternar entre mayusculas y minusculas: [~]
- Identar: [>] o [<]

## Selección
Se entra desde el modo visual pulsando [^g]. Tiene un comportamiento similar al modo visual solo que al escribir no realizaremos comandos sino que reemplazaremos el texto, como en un editor de texto normal.

## Ex
 Este modo se asemeja al modo de comandos, con la diferencia de que tras la ejecución de una orden no se vuelve al modo normal. Se entra pulsando [Q] y se sale con `vi`.

# Cambios en un fichero
- Salir(e ignorar cambios): Ejecute el comando `:q!`
- Escribir: Ejecute el comando `:w`
- Escribir y salir: Ejecute el comando `:x` o [ZZ]

# Hacer y deshacer:

- Deshacer(Undo): [u] ó ejecutamos el comando `u`.
- Rehacer(Redo): [^r].
- Temprano(Earlier): `:ea n` donde n es el numero de pasos que deseamos deshacer. Si queremos regresar en el tiempo basta com pasarle las unidades de tiempo, ya sean *s, h, d*. Ejemplo: para regresarnos dos hora serian `:ea 2h`.
- Tarde(later): `:lat n` donde n es el numero de pasas que deseamos rehacer. Si queremos adelantar en el tiempo basta com pasarle las unidades, ya sean *s, h, d*. Ejemplo: para adelantar dos hora serian `:lat 2h`.

# Moverse en un archivo

- Arriba(Up): [k] ó [<Up>]
- Abajo(Down): [j] ó [<Down>]
- Izquierda(Left): [h] ó [<Left>]
- Derecha(Right): [l] ó [<Right>]

- Final de la palabra actual(End): [e]
- Final de la palabra actual delimitada por espacios(End): [E]
- Inicio de una palabra(Begin): [b]
- Inicio de una palabra delimita por espacios(Begin): [B]
- Inicio de la siguiente palabra: [w]
- Inicio de la siguiente palabra delimitada por espacios: [W]

- Inicio de un parrafo: [{]
- Final de un parrafo: [}]

- Final de la linea: [$]
- Inicio de la linea: [0]

- Inicio del documento, primera linea: [gg].
- Final del documento, ultima linea: [G]

- Primera linea de la pantalla o linea alta(high): [H]
- Linea del medio de la pantalla(medium): [M]
- Ultima linea de la pantalla o linea baja(Low): [L]

- Saltar a la linea n, donde n es un numero entero: `:n`

# Portapapeles

- Pegar en la linea despues del cursor: [p]
- Pegar en la linea antes del cursos: [P]

- Copia una linea completa: [Y].
- Eliminar hasta el final de la linea: [D].
- Corta un caracter: [x].

# Lenguaje
El lenguaje en vim se utilza una sintaxis del tipo **verbo-modificador-objeto**.

## Verbos
Algunos verbos de vim:
- [v]: visual
- [d]: delete ó borrar
- [y]: yank ó copiar
- [a]: change ó cambiar.

## Modificador
- [i]: inside ó dentro.
- [a]: around ó alrededor.
- [t]: till ó hasta que encuentre el caracter.
- [f]: find ó hasta que encuentra el caracter incluyendolo.
- [/]: search ó buscar.

## Objeto
- [w]: word ó palabra.
- [s]: sentence ó frase.
- [p]: paragraph ó párrafo.
- [t]: tag ó etiqueta(para *HTMl* o *XML*).

# Utilidades
- Repetir: La ultima accion que realizamos la podemos repetir utilizando [.]
- Indentar: Utilizando [>>] ó [<<] respectivamente.
- Saber el codigo ASCII del caracter actual: [ga]
- Insertar caracter ASCII: En el modo insert tecleamos [^v]{codigo}

# Paneles
Esto, que nosotros conocemos como paneles de emuladores de terminal como Terminator, Vim lo llama ventanas. Cuando abrimos Vim, tiene solo un panel pero podemos dividirlo tanto horizontalmente como verticalmente:

- `sp[lit] {archivo}`: divide el panel de forma horizontal
- `vsp[lit] {archivo}:` divide el panel de forma vertical.
**NOTA:** Estos comandos cargan el archivo si lo especificamos en el nuevo panel. Si no especificamos un archivo se divide el panel con el mismo archivo.

**NOTA:** Nótese que **un panel que se ha dividido con el mismo archivo no son dos instancias abiertas del archivo**. ¿Qué significa esto? Que los cambios en un panel serán reflejados en el otro automáticamente sin tener que recargar el archivo.

## Movernos entre paneles
Para movernos entre paneles utilizamos los siguientes atajos:
- `:[^c+w][w]`: Movernos por los paneles.
- `:[^c+w][h]`: Ir al panel de la izquierda.
- `:[^c+w][j]`: Ir al panel de la abajo.
- `:[^c+w][k]`: Ir al panel de la arriba.
- `:[^c+w][l]`: Ir al panel de la derecha.
- `:[^c+w][l]`: Ir al panel de la derecha.

- `:[^c+w][c]`: Cerrar panel. Tambien funciona `:cl[ose]`.
- `:[^c+w][o]`: Mantener el panel activo, cerrando los demas. Tambien sirve `on[ly]`.

- `:[^c+w][=]`: Iguala la algura y anchura de los paneles.
- `:[^c+w][_]`: Maximiza la altura del panel activo.
- `:[^c+w][|]`: Maximiza el ancho del panel activo.
- `:[N][^c+w][_]`: La anchura sera de N filas.
- `:[N][^c+w][|]`: La altura sera de N filas.
- `:h window-moving`: El comando para inspeccionar la documentacion de vim. Echale un vistazo.

# Pestañas

- `:tabnew` abre una nueva pestaña.
- `:lcd {ruta}`: cambia la ruta(carpte) donde apunta el panel
- `:windo lcd {ruta}`: cambia la ruta donde apuntas todos los paneles de una pestaña.
- `:T` . Mueve todo el panel actual a una nueva pestaña
- `:tabe[dit] {archivo}`: abre un archivo en una nueva pestaña
- `:tabc[lose]`: cerrar una pestaña.
- `:tabo[nly]`: Cerrar todas la pestañas menos la activa.
- `:tabn[ext]`: Ir a la siguiente pestaña. [gt] hara lo mimo.
- `:tabn[ext] {N}`: Ir a la pestaña N. [Ngt]hara lo mimo.
- `:tabp[revious]`: Ir a la pestaña anterior. [gT] hara lo mimo.
- `:tabmove {N}`: Nos sirve para mover las pestañas.
- `:h tabpage`: El comando de ver la documentacion.

# Motions
Los motions son atajos que nos permitiran movernos mas rapido a traves de un documento

- [j]: Bajar un número de línea(Lineas separadas por un retorno de carro)
- [gj]: bajar una línea visible.
- [k]: sube una línea
- [gk]: sube una línea visible.
- [0]: va al inicio de la linea real.
- [g0]: Va al inicio de la linea visible en pantalla.
- [^]: va al primer caracter no blanco de la línea.
- [g^]: Va al primer caracter no blanco de la línea visible.
- [$]: Va al final de la linea real.
- [g$]: Va la final de la línea visible.
- [w]: va al principio de la siguiente palabra.
- [b]: Va hacia atras, al principio de la palabra actual o de la anterior.
- [e]: Val al final de la palabra actual y si estamos allí, de la siguiente.
- [ge]: Va al final de la palagra anterior.
- [/]{busqueda}: Muy útil para dirigirnos a palabras concretas del texto.
- [f]{caracter}: Va hacia delante hasta que encuentre el carácter.
- [F]{caracter}: va hacia atras hasta que encuentra el caracter.
- [t]{caracter} : va hacia adelante y se para una columna antes del caracter.
- [T]{caracter} : va hacia atras y se para una columna antes del caracter.
- [;]: Repite la ultima busqueda de caracter.
- [,]: da la vuelta a la última busqueda.
- [%]: Nos lleva de (,[,{ a ),],} y biseversa.

# Lugares relevantes
El comando [m{a-zA-Z}] crea una marca (o varias si definimos más) en el archivo a la que podremos saltar cuando queramos usando el acento grave más la letra del alfabeto que hayamos usado.


Lo bueno de las marcas es que hay algunas que se añaden solas, aquí tenéis unos cuantos comandos que se ejecutan desde el modo normal y sin los dos puntos:

- “ ir a la posición antes del último salto en el archivo actual.
- \`. ir a la posicion del ultimo cambio.
- \`^ ir a la posicion de la ultima insercion.
- \`[ Ir al a posicion inicial del último cambio o copia(yank).
- \`] Ir al a posicion final del último cambio o copia(yank).
- \`< Ir al a posicion inicial de la última selección visual.
- \`> Ir al a posicion final de la última selección visual.

**NOTA:** Si quieres saber mas de esta función puedesconsultar la ayuda con `:h m`.

# Registros
Un registro es un contenedor que guarda texto. De la misma forma que usamos el portapapeles del sistema para copiar, pegar y cortar texto aunque también se puede utilizar como macro, para guardar comandos.

Acceder a los registros de vim es sencillo, solamente hay que especificarlos con ["{registro}], donde {registro} puede ser cualquier caracter.

**NOTA:** Si no espeficicamos un registro a utilizar vim simplemente utilizara el registro son nombre

**IMPORTANTE:** el verbo yank tambien copia al registro 0.

**Ver el manual de registros:** `:h registers`.

## Registros predefinidos:
Algunos registros ya definidos por vim son:
- [""]: El registro sin nombre.
- ["\_]: El registro agujero negro.
- ["+] / ["-]: **El portapapeles del sistema**
