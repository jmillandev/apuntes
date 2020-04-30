# Imagenes
Haciendo una analogia con OPP. Las imagenes son clases, en esta estan todas la configuraciones deun contenerdor.

## Dockerfile
El dockerfile vendria siendo como la receta para la configuración de nuestra imagen.

Una vez creado el fichero *Dockerfile* debemos construir la imagen con ayuda de `docker imagen build --help`

### Directiva
A traves de una directiva nosotros definiremos el comportamiento de la imagen, se puede ver como un paso de la receta.

Nota: Estas deben estar en mayusculas.

Directivas:
- FROM: a traves de esta definimos la imagen base de nuestro contenedor. Ejemplo: `FROM ubuntu`

- RUN: Nos permite ejecutar un comando. Ejemplo: `RUN touch Example.txt`

- COPY: Nos permite copiar un fichero o nodo desde nuestro maquina a nuestra imagen. Ejemplo: `COPY host_path container_path`

- ADD:  Nos permite descomprimir/trasferir archivos desde nuestra maquina o  internet a nuestro imagen: `ADD from_path container_path`

- ENV: Define el valor de una variable de entorno. Ejemplo: `ENV var_name value`.

**NOTA:** Las variables de entorno pueden ser remplazadas en el instante que se crea el contenedor a traves del flat  *-e*.

- ARG: Define un valor que utilizaremos dentro de nuestro dockerfile, el mismo luego puede ser modificado en el momento de creacion de la imagen(con el flat *--build-arg*). Ejemplo: `ARG arg_name="value"`. Lo utilizamos atraves de interpolacion(`${arg_name}`)

- USER: Con esta directiva podremos hacer swich entre los usuarios existentes y declarar el usuario por defecto. Esto tambien nos sera util para que los ficheros creados/modificados a partir de ese punto le pertenezcan a un determinado usuario.. Ejemplo: `USER user_name`. Claro esta que el usuario user_name ya debe existir en el contenedor. Paracrear un usuario nos apoyamos de `RUN useradd -ms /bin/bash user_name`.

- WORKDIR: Nos crea una carpetra y os situa dentro de la misma al instanciar el contenedor. `WORKDIR /app`

- CMD: Nos permite ejecutar un comando o bien un script a la hora de instanciar nuestro contenedor. Ejemplo: `CMD ["echo", "Hola mundo", " con docker"]`. Esta instruccion usualmente es la ultima, ya que es la que conecta el punto de entrada de nuestro contenedor.
**NOTA:** No es recomendable el uso de esta directiva para ejecutar nuestra app, ya que la misma puede ser redefinida en el momento que instanciamos el contanedor.

- ENTRYPOINT: Es bastante similar a CMD. La diferencia mas notable es que esta directiva no puede ser reemplazada cuando instanciamos el container. Es la mas recomendada para ejecutar nuestra app(script o binario.)
**NOTA:** Todo los que pasemos en la directiva *CDM* ira directamente a la entrada del ENTRYPOINT, es decir, sera angumentos de este.
Ejemplo:
``` dockerfile
ENTRYPOINT ["echo", "Hola mundo!"]
# Esto sera lo mismo que
ENTRYPOINT ["echo"]
CDM ["Hola mundo!"]
```

## Dockerignore
En fichero *.dockerignore* fichere declararemos todos los path que no queremos excluir en la construccion de nuestra imagen

## Publicar
El proceso para publicar seguimos los siguientes pasos:

1. Debemos estar logueados. Esto lo hacemos con `docker login`.
2. Buscamos el nombre de la imagen a subir apoyandonos de `docker image ls`.
3. Renombramos con la siguiente estructura: `docker tag image_name username/image_name`
3. Subimos la imagen siguiendo la estructura `docker push image_name`.

# Contenedor
Es la instancia de una imagen

## Gestionar
- Ejecutar: `docker container run image_name`
- Eliminar: `docker ccontainer rm id_container_1 ... id_container_n`
- Crear: `docker container create image_name`
- Iniciar: `docker container start id_container`
- Detener: `docker container stop id_container`

## Puertos
Los puertos en docker nos permitiran exponer un servicio dentro de nuestro contanedor hacia nuestra maquina host.

Definiendo un puerto: `docker container run -p host_port:container_port image`

Definiendo un puerto aleatorio: `docker container run -P image`

## Commit
Basicamente un commit es tomar un contener con todos sus recursos y construir una imagen de el. `docker container commit  --help`

## Volumenes
A traves de los volumenes nosotros podremos compartir ficheros entre contenedores y la maquina host.

Crear volumen: `docker volume create volume_name`

Montar volumen en un contanedor: `docker container run -v volume_name:container_path image`

# Redes
Las redes en docker nos permitiran tener una conexion entre contenedores asi como con internet. En docker existen 3 tipos de redes:

1. Bridge: Hay un puente entre la red interna de docker y nuestro host. A traves de esta tenemos acceso a internet
2. Host: Es la red de nuestro host. Si agregamos un contendedor a esta nos aseguraremos que el contendedor tendra la ip de nuestra maquina. 
3. None: Con es red, definimos un contenedor sin red, es decir, un contenedor completamente aislado

Por default cada vez que creamos un nuevo contenedor docker lo agrega a una red Bridge asignandoles un ip dinamica.

# Compose
Es una herramienta para definir y correr aplicaciones multicontenedores.

**NOTA:** Es un binario aparte del de docker. Lo que significa que debemos instalarlo

## Fichero
Para trabajar con docker-compose lo primero que de bemos hacer es generar un fichero *docker-compose.yml*. Dentro de este declararemos toda la configuracion de nuestros contenedores. La primera linea sera algo asi: `version: "3.7"`.

Ejemplo
``` yml
version: "3.7"

services: #cada servicio es un contenedor
    nginx:
	image: nginx
	cotainer_name: nginx_example_container
	ports:
	    - "80:80"
 	networks:
	    - servers
	volumes:
	    - ./index.html:/var/share/nginx/html/index.html # Para este ejemplo existe un fichero index.html en una carpeta al mismo nivel que este fichero.

    mysql:
	image: mysql
	container_name: mysql
	ports:
	    - "3306:3306"
	environment: # Aqui definimos las variables que le pasaremos a la imagen del contenedor
	    MYSQL_ROOT_PASSWORD: $(MYSQL_ROOT_PASSWORD)
	networks:
	    - backend
	volumes:
	- mysql:/var/lib/mysql

networks: # Por default se crear una red con el nombre de la carpeta donde esta este fichero y se conectan alli todos los contenedores
    backend:
        driver: bridge

    servers: # Este es el nomkbre una red existente
	external: true #Esto indica que la red ya existe y docker no la debe crear

volumes:
    mysql: # Esto creara un nuevo volumen en nuestro docker
```

**NOTA:** El fichero *docker-compose.yml* recibe la variables de entorno de un fichero *.env* definido a su mismo nivel. Este fichero se veria algo asi:

```
MYSQL_ROOT_PASSWORD=root
`
