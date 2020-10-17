---
title: "APIs REST"
slug: "api-rest"
description: "👩‍🔧"
keywords: [programacion, desarrollo, software ,API, REST]
draft: true
tags: []
math: false
toc: false
---
# Conceptos Basico para manejar un API

## HTTP
HTTP son las siglas de Hypertext Transfer Protocol o protocolo de transferencia de hipertexto, es el conjunto de reglas en las que se van a comunicar dos entidades, en este caso dos computadoras.

## REST
Es un acrónimo de Representational State Transfer o transferencia de estado representacional, le agrega una capa muy delgada de complejidad y abstracción a HTTP. Mientras que HTTP es transferencia de archivos, REST se basa en la transferencia de recursos.

## API RESTful
Es una API diseñada con los conceptos de REST:

- Recurso: todo dentro de una API RESTful debe ser un recurso.
- URI: los recursos en REST siempre se manipulan a partir de la URI, identificadores universales de recursos.
- Acción: todas las peticiones a tu API RESTful deben estar asociadas a uno de los verbos de HTTP: *GET* para obtener un recurso, *POST* para escribir un recurso, *PUT* para modificar un recurso y *DELETE* para borrarlo.

REST es muy útil cuando:

- Las interacciones son simples.
- Los recursos de tu hardware son limitados.

**NOTA:**No conviene cuando las interacciones son muy complejas.

# Consumir servicio (GET)
Consumir un API es tan sencillo como consultar su URL. Para este caso vamos a utilizar la linea de comandos.

Utilizando el comando ‘curl’ dentro de nuestra terminal podemos realizar peticiones a cualquier sitio web, por ejemplo una API como la de xkcd.

`curl https://xkcd.com/info.0.json`

El anterior comando nos regresa información del API, pero de manera poco legible. para poder verlo de manera más ordenada podemos un pequete o lenguaje para JSON, en este caso 'jq':

`curl https://xkcd.com/info.0.json | jq`

# Exponer Datos

En el caso de que recibamos una peticion de tipo **GET**/**POST**/**DELETE**/**UPDATE** debemos realizar la logica de negocio y devolver un archivo tipo JSON(si es necesario).
Es una buena practica mandar en el HEADER de la respuesta el 'Content-Type : application/json'


# Restriccion de acceso (Autentificaciones)

## Via HTTP
Se hace por medio de la super global SERVER del servidor, lo cual es poco recomendado. Dado a que la autenticación vía HTTP tiene dos problemas:

- **Es poco segura**: las credenciales se envían en cada request anteponiendo el usuario y contraseña en la url, por ejemplo: user:password@platzi.com.

- **Es ineficiente**: la autenticación se debe realizar en cada request.

## Via HMAC
Es un codigo de autentificacion basado en HASH de mensajes. Para esta autenticación necesitamos 3 elementos:

- Función Hash: Difícil de romper, que sea conocida por el cliente y servidor.
- Clave secreta: Solamente la pueden saber el cliente y el servidor, será utilizada para corroborar el hash.
- UID: El id del usuario, será utilizado dentro de la función hash junto con la clave secreta y un timestamp.

Es mucho más segura que la autenticación vía HTTP, por ello la información que se envía a través de este método no es muy sensible.

# Via Access Tokens (Accesos temporales)
Está forma es la más compleja de todas, pero también es la forma más segura utilizada para información muy sensible. El servidor al que le van a hacer las consultas se va a partir en dos:

- Uno se va a encargar específicamente de la autenticación.
- El otro se va a encargar de desplegar los recursos de la API.

El flujo de la petición es la siguiente:

1. Nuestro usuario hace una petición al servidor de autenticación para pedir un token.
2. El servidor le devuelve el token y almacena este en una base de datos temporal.
3. El usuario hace una petición al servidor para pedir recursos de la API.
4. El servidor con los recursos hace una petición al servidor de autenticación para verificar que el token sea válido(este en la base de datos).
5. Una vez verificado el token, el servidor le devuelve los recursos al cliente.

**NOTA:** El token es temporanl, tiene caducidad en el tiempo.

# Buenas Practicas
- Siempre utiliza **sustantivos** para nombrar tus **recursos**(casa, libro, auto, ect).
- Añade los **nombres** en **plural** para las **urls** (https://misitio.com/serviciosbancarios/v1/transferencias/, https://misitio.com/serviciosbancarios/v1/pagoprovedores/, https://misitio.com/serviciosbancarios/v1/nominas/, etc).
- Las modificaciones a recursos deben hacerse con su verbo HTTP correspondiente: POST, PUT o DELETE.
- Para devolver recursos asociados a otro recurso utiliza url que incorporen subrecursos: /Autos/1/Choferes.
- Navegabilidad vía vínculos.
- Cuando devuelvas colecciones los pedidos deben ser filtrables, ordenables y paginables.
- Versiona tu API, añade el número de versión en la url: v1/Autos.