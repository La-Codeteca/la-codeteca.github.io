---
layout: post
toc: true
comments: true
share: true
author_profile: false
header:
    image: /assets/images/paginacion/paginacion.png
    overlay_color: "#000000"
title: Paginar resultados en Fastapi
description: "Aprende a paginar las respuestas de un endpoint de forma sencilla."
excerpt: "Aprende a paginar las respuestas de un endpoint de forma sencilla."
tags: [Backend, developer, APIs, Fast-API, Python]
categories: 
  - Python
  - Fastapi

---   

## Introducción

Cuando empezamos nuestros proyectos es normal que tengamos pocos datos, por lo que no importa si enviamos todo lo que nos devuelve la base de datos "a cholón", ya que por lo general
no supondrá ningún problema.

Las dificultades llegan cuando, con el paso del tiempo y el uso, los datos empiezan a incrementarse y las respuestas se vuelven cada vez más pesadas, haciendo que sean complidadas de mantener, de visualizar e incluso lleguen a dar problemas por la cantidad de recursos que empiecen a consumir. Es en ese momento en el que la paginación pasa a ser una necesidad.

En esencia, paginar los resultados no es más que dividir la información que queremos enviar en subgrupos, a los que llamaremos páginas. Cada pagina contendrá una parte del total, de forma que podemos consumir una parte manejable de los datos y, si necesitamos más, sencillamente pediremos la siguiente página.

![paginado](/assets/images/paginacion/paginacion.png){: .align-left}

Hoy vamos a ver como implementar la paginación de resultados en un proyecto de FastAPI. Utilizaremos la librería [FastAPI Pagination](https://uriyyo-fastapi-pagination.netlify.app/) para simplificar el proceso y veremos como obtener paginas del tamaño que nos interese.

{% include video id="XsxDH4HcOWA" provider="youtube" %}

## Empezando con el experimento

Lo primero será crear un proyecto sencillo, con un endpoint que nos devuelva datos falsos de usuarios. Para simplificar el ejemplo no haremos uso ni siquiera de una base de datos, sencillamente devolveremos un JSON escrito en duro, pero la implementación será exactamente la misma independiemente de dónde recibamos los datos.

Vamos primero con el punto de partida, un proyecto que nos devuelva - por el momento - toda la inforación sin paginar:

```python

from fastapi import FastAPI
import json

app = FastAPI()

f = open('data.json')
data = json.load(f)

@app.get("/data")
async def get_all_data():
    return data

```

El fichero con la data falsa puedes obtenerlo [aquí](). Te recomiendo que veas nuestro post sobre [crear datos falsos para pruebas usando fake] para que puedas crear tus propios datos de la longitud que necesites y con los tipos que más convengan.

Si lo lanzamos y nos vamos al navegador podemos ver nuestro endpoint, si lo probamos veremos que nos devuelve el JSON con los datos:
![paginado](/assets/images/paginacion/sin_paginar.png){: .align-left}

## Paginando los resultados

Ahora, vamos a instalar la librería FastAPI Pagination

Y haremos unos cambios en el código para que empice a funcionar:

```python
from typing import Union, Optional
from fastapi import FastAPI
from fastapi_pagination import Page, paginate, add_pagination
from pydantic import BaseModel, Field

import json

app = FastAPI()

f = open('data.json')
data = json.load(f)

class User(BaseModel):
    name: str = Field(..., example="Paco")
    location: str = Field(..., example="Madrid")
    birth: str = Field(..., example="1 Enero 1970")

@app.get("/data", response_model=Page[UserOut])
async def get_all_data():
    return paginate(data)
    
add_pagination(app)
```

Lo primero es importar la librería de fastapi_pagination

```python
from fastapi_pagination import Page, paginate, add_pagination
```

Y crear una clase con los datos que vamos a querer devolver, esto nos servirá a modo de "plantilla" para que fastapi_pagination sepa como crear las páginas.

```python
class User(BaseModel):
    name: str = Field(..., example="Paco")
    location: str = Field(..., example="Madrid")
    birth: str = Field(..., example="1 Enero 1970")
```

Ahora vamos a indicar que nuestra respuesta será de la clase User, y más concretamente que queremos que sea una pagina de clase User (es decir, una pagina que use esa plantilla que hemos creado). Todo esto se indica en el decorador, justo despúes de la ruta del endpoint:

```python
@app.get("/data", response_model=Page[UserOut])
```

Por ultimo, añadimos add_pagination() pasando la APP para que la librería funcione. Y ya está, si refrescamos el navegador en la pagina de la documentación veremos que ahora tenemos dos parametros opcionales, por un lado el tamaño de la página (cuandos resultados queremos que nos devuelvan por petición) y el número de página que queremos que nos devuelva.

![paginado](/assets/images/paginacion/paginado.png){: .align-left}

De esta forma, si pedimos un tamaño de página de 10 y la segunda pagina nos devolverá los resultados a partir del número 11.

Y ya está, eso es todo, puedes descargar el ejemplo completo desde el [github de la codeteca](https://github.com/La-Codeteca) desde [este enlace](https://github.com/La-Codeteca/paginando-con-fastapi), incluido todo lo necesario para levantarlo con un docker-compose y empezar a utilizarlo rápidamente.

Pronto publicaremos otra entrada explicando como incluir filtros en tus endpoint.

¡Hasta pronto!

<div class="aditional-info">

<h2>/** Comentarios del post **/</h2>

<h3> # Todos los enlaces:</h3>
<ul>
  <li> // <a href="https://uriyyo-fastapi-pagination.netlify.app/">Documentación oficial sobre FastAPI Pagination</a></li>
  <li> // <a href="https://gist.github.com/crakernano/11812a4df3b31e9d744ef5bec14018c3">Un ejemplo hecho por mi</a></li>
</ul>


<h3> # Recursos usados:</h3> 
  <ul>

    <li> <a href=""> Logo de FastAPI</a></li>
  </ul>
</div>