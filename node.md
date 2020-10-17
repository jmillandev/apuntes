---
title: "Node.js"
slug: "node"
description: "💚"
keywords: [programacion, desarrollo, software, javascript, node, backend]
draft: false
tags: []
math: false
toc: false
---
# 1 Instalaciones Recomendadas

1. [Postman](https://link): Para inspeccionar las peticiones al servidor.

2. [VScode](https://link): No es obligatorio. Tambien se recomiendan las siguientes extensiones:
- HTML CSS Support.
- JavaScript(ES6) code snippets.
- JS_CSS_HTML Formatter.
- Terminal.
- TypeScript Importer.

3. [Git](https://link): Es un manejador de versiones.

# 2 Paquetes Recomendados
## 2.1 Nodemon
[Nodemon](https://www.npmjs.com/package/nodemon): Este paquete nos sera de mucha ayuda para no tener que bajar y subir el servidor manualmente cada vez que hagamos un cambio. Este hara el reinicio automaticamente cuando note un cambio en alguno de los archivos.

**NOTA:** Por default nodemon solo reseteara el servidor cuando hagamos una cambio en los archivos javascript. Si queremos que ejecute estos cambios en otro tipo de ficheros lo haremos de lasiguiente manera: `nodemon app -e js,css,html,hbs`
## 2.2 Yargs
[Yargs](https://www.npmjs.com/package/yargs): Nos sirve para manejar los argumentos de entrada en una app de linea de comandos.

## Colors
[Colors](https://www.npmjs.com/package/colors): Nos ayuda a colorear la salida de nuestra CLI.

## 2.3 Request
[Request](https://link): Nos sirve para hacer peticiones HTTP utilizando callbacks.
**NOTA:** El metodo [encodeUrl()](https://link) nos puede servir de mucha ayuda. Sirve para escapar strign a uri amigables.

## 2.4 Axios
[Axios](https://link): Nos sirve para hacer peticiones HTTP utilizando promesas.
**NOTA:** El metodo [encodeUrl()](https://link) nos puede servir de mucha ayuda. Sirve para escapar strign a uri amigables.

## 2.5 EXPRESS
[Express](https://www.npmjs.com/package/express): Nos permite montar un servidor HTTP. Esta basado en la libreria HTTP que viene por defecto en node.

## 2.6 Handlebars
[hbs](https://www.npmjs.com/package/hbs): Es un motor de platatillas(template engine) para express.
Una configuracion sencilla para este motor de plantillas junto con express es:
``` javascript
const express = require('express')
const app = express()

app.set('view engine', 'hbs')

app.get('/', (req, res) => {
    res.render('filename', {
        // Context
    })
})
```

**NOTA:** Debe haber un fichero con extension `.hbs` en un carpeta views en la raiz de la app. Este fichero contiene el template.

## 2.7 Body-parser
[Body-parser](https://link): No ayuda a leer mensajes serializados desde la URL(como por ejemplo los que son mandados por POST o PUT)

# 2.8 Mongoose
[Mongoose](https://link): Nos permite conectarnos a una base de datos NoSQL(MongoDB)

# 2.9 Moogoose-unique-validator
[Mongoose-unique-validator](https://www.npmjs.com/package/mongoose-unique-validator)
Nos permite mostrar de una manera mas amigable los errores.

# 2.10 Bcrypt
Nos sirve para ecriptar mensajes.

# 2.11 Jsonwebtoken
Nos sirve para la genereacio y firma de JWT.

# 2.12 express-fileupload
Bueno, como su nombre indidca este paquete nos ayudara a la subida de archivos a nuestro servidor.

# 3 Requireds
Tenemos 3 tipos de required:

1. De un proyecto propio de node: Son librerias que ya existen en node. No requieren de ningun paso adicional.
Podemos encontrar dichas librerias en la [documentacion de node](https://link).
Ejemplo:

`const fs = require('fs')`

2. Libreria externas. Paquetes que no son nativos de node.

3. Archivos de nuestro proyecto. Ejemplos
```javascript
const module1 = require('./module1')
const module2 = require('../modules/module2')
```

**NOTA:** los modulos se exportan a traves del metodo exports del objeto module. Este objeto esta disponible a en todo el proyecto. Dicho metodo recibe un JSON con las funciones,objetos,variable, etc a exportar.

# 4 Objetos de NODE
Durando el ciclo de vida de un programa en node hay varios objetos que corren en este. Algunos son:

- module: Este contine valores como cuales son los modulos disponibles o exportados durante nuestra app.

- process: Contiene muchos datos interesantes. Sobre que SO esta corriendo la app, arquitectura del procesaro,argumentos(argv), etc.

# 5 proyecto con npm
Podemos compartir y tener un control de versiones de las dependencias con npm como lo hariamos con composer en PHP.

**NOTA:** Esto es muy importante hacerlo antes de instalar dependencias
Sintasis: `npm init`

# 5.1 script
Al instalar o iniciar un proyecto. en el fichero package.json tenemos un atributo o propiedad *script*. En este estan todos los comando que podremos ejecutar desde nuestra app en produccion.
Para correr un comando la sintaxis seria: `npm run name_comand`

**NOTA:** Si montamos una app en Heroku por defecto esta ejecutara el servidor desde el script *start*.

# Tokents
Los tokents son utilizados para verificar o identificar a un usuario en especial. Se pueden asociar tambien con las variables de session.

Pero estos son mucho mas manejables y permite manejar una mayor cantidad de usuarios(mas de 5 mil) sin invertir en un gran equipo.

## JWT
Los JSON Web Tokents estan compuestos por 3 partes principales separados por un  punto( '.' ):

- Header: Contiene informacion sobre el algoritmo utilizado para la incriptacion junto con el tipo de tokent(en este caso JWT)
- Payload: Contiene la informacion que enviamos en el Token(Aunque pensemos que esta encriptado(de forma segura) es muy facil desencriptar la informacion)

- Firma: Es lo que le permite a los verificadores del JWT que este es valido.

https://jwt.io es una herramientamienta muy util.
