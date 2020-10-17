---
title: "Nginx"
slug: "nginx"
description: "📭"
keywords: [programacion, desarrollo, software, servidores, nginx, devops]
draft: true
tags: []
math: false
toc: false
---
Nginx es un servidor WEB, que de igual forma nos sirve como Proxy Inverso, Balanceador de carga, Sevidor de Emails, etc.

Una de las principales caracteristicas de Nginx es que funciona de manera Asincrona y basada en Eventos.

# Conceptos Basicos

## Directivas
Son basicamente funciones, estan compuestas por un nombre seguidas de un conjunto de parametros. Ejemplo `auth_basic "String"`. Una de las caracteristicas de una directiva es que esta debe encotrarse dentro de un contexto.

**NOTA:** Algunas directivas solo pueden ejecutarse dentro de un contexto en especial.

## Contexto
Estos no son mas que una directiva a la cual de definimos un cuerpo a traves de una llaves(`{}`), la cual puede cotnener a multiples directivas.

**NOTA:** Es posible definir contextos de una forma anidada.

### Core Contexts
Estos nos permiten definir la funcionabilidad basica de Nginx. Aquí algunos de los [core contexts](http://nginx.org/en/docs/http/ngx_http_core_module.html) mas sobresalientes son:


1. Main: Es el primer contexto que contiene toda la configuración.
2. Event: Es utilizado para definir la configuracion sobre las configuraciones de usuarios. Ejem: Cantidad de peticiones a aceptar, numero de procesadores, etc. **NOTA:** Este contexto solo puede ser definido una vez.
3. Http: Aca se definen las directivas para el manejo de peticioens http y https.
4. Server: Ese contexto lo definiremos dentro del contexto de http para el manejo de multiples configuraciones. 
5. Location: Nos permite poder manipular la petición de los usuarios. En esta directiva nosotros podremos modificar el comportamiento de una peticion. Ejem: redireccionar al usuario cuando acceda a una determinadata ruta coomo puede ser /admin.
6. Upstream: Aca podremos definir un conjunto de servidores los cuales podremos utilizar para hacer balanceo de cargar, proxy reversivos. Este contexto se debe encontrar dentro del contexto de http pero fuera del contexto de server.
7. Mail:
8. If: Basicamente este contexto funciona igual que en cualquier lenguaje de programación. Ejem: Podremos redirigir al usuaria desde una peticion http a una https.


# Gestion
Indicarle a Nginx que cargue una nueva configuración. `nginx -s reload`.
Testear los ficheros de configuración. `nginx -t`.

