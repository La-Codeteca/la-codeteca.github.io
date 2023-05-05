---
layout: post
toc: true
comments: true
share: true
author_profile: false
header:
    image: /assets/images/paginacion/paginacion.png
    overlay_color: "#000000"
title: Crear datos de prueba
description: "A veces necesitamos datos para probar nuestras aplicaciones. Aquí te enseño a generarlos like a PRO"
excerpt: "A veces necesitamos datos para probar nuestras aplicaciones. Aquí te enseño a generarlos like a PRO"
tags: [Backend, developer, Data, test, bigdata , Python]
categories: 
  - Python
  - Testing
---   


A veces nuestras aplicaciones requieren de datos para porderse usar o probar. Ya sea tener unos cuantos usuarios en la base de datos, productos, información sobre el clima... lo que sea.

Lo normal es que cuando eso ocurra nos dediquemos a picar un JSON o meter registros en una base de datos hasta conseguir un conjunto de datos lo suficientemente grande para nuestro proposito.

Sin embargo, esto hace que generalmente tengamos muy pocos datos, lo que hace que nuestras pruebas queden muy sesgadas y supone un problema enorme cuando estamos tratando con aplicaciones
que requieren de un volumen de datos enorme para poder probar su funcionamiento (Como pueden ser todas aquellas que usan ML o Bigdata).

En estos casos, lo normal es buscar en internet si algún alma caritativa a compartido un dataset que podamos usar. Pero y si te dijera que puedes crear todos los datos ficticios que quieras de una forma sencilla y, sobre todo, automática.

La librería que os traigo hoy hace precisamente eso, generar datos falsos partiendo de lo que le pidamos, se llama [Faker](https://faker.readthedocs.io/en/master/) y se va a convertir en vuestra mejor amiga a la hora de testear aplicaciones. ¡Vamos a ello!

{% include video id="XsxDH4HcOWA" provider="youtube" %}

Lo primero de todo es instalar la librería, esta disponible en pip así que simplemente tenemos que hacer

```bash
pip install Faker
```

Listo, ya podemos empezar a usarla. Vamos a comenzar por algo sencillo... supongamos que necesitamos un conjunto de nombres, podemos hacer un pequeño script para que nos los genere:

```python
from faker import Faker
fake = Faker()

userName = fake.name()

print(userName)
```

Si ejecutamos este script, nos dará un nombre completo, y cada vez que lo lancemos nos dará uno distinto. ¿chulo? Pues hay mucho más. Faker puede crear no solo nombres, también numeros de telefono, direcciones, IPs, texto, códigos de barras, cuentas corrientes, texto... y mucho, mucho más. Además todo ello configurable, pudiendo pedirle por ejemplo solo nombres de hombre o de mujer, solo direcciones de un determinado pais, etc.  Te recomiendo revisar su [documentación](https://faker.readthedocs.io/en/master/)  para ver todo lo que ofrece.

Vamos a suponer que queremos probar una aplicación que recoja datos de usuarios, queremos tener una base de datos de lo más completa, así que vamos a pedir los siguientes datos:

- Nombre y apellidos
- año de nacimiento
- teléfono
- número de cuenta corriente
- Dirección
- Puesto de trabajo
- Un texto que podría ser su biografia.

Vamos a ir poco a poco, crearemos un unico usuario y luego con un bucle crearemos todos los necesitemos:

Vamos primero a conseguir los datos, sencillamente haciendo uso de Faker podriamos escribir:

```python
from faker import Faker

fake = Faker()

print(fake.name())
print(fake.date_between())
print(fake.phone_number())
print(fake.iban())
print(fake.address())
print(fake.job())
print(fake.paragraph(nb_sentences=5))
```

y obtener algo como esto:

```bash
Douglas Roth
1994-01-31
001-858-543-9321
GB96OXSG52158500309060
3632 Alison Manors
New Rebecca, RI 56401
Magazine features editor
Paper your beat learn opportunity. Foreign account cover street result day senior much. Wall include church our.
```

Pero podemos mejorar un poco la implementación, si lo que queremos es utilizar esto para alimentar la base de datos de nuestra aplicación, seguramente queramos que usuario sea una clase que podamos almacenar, es sencillo:

```python

from faker import Faker

fake = Faker()

class User:
    user:str
    birth:str
    phone:str
    bank:str
    address:str
    job:str
    bio:str

usuario = User()

usuario.user    = fake.name()
usuario.birth   = fake.date_between() # Opcional: start_date - Por defecto hace 30 años. end_date - Por defecto hoy
usuario.phone   = fake.phone_number()
usuario.bank    = fake.iban()
usuario.address = fake.address()
usuario.job     = fake.job()
usuario.bio     = fake.paragraph(nb_sentences=5) 
```

Ahora solo tendríamos que almacenar ese objeto en nuestra base de datos. Y si en lugar de crear un usuario queremos almacenar 10, 50, 100 o cualquier otro número solo tenemos que meter la creación y guardado de ese objeto en un bucle:

```python

from faker import Faker

fake = Faker()

class User:
    user:str
    birth:str
    phone:str
    bank:str
    address:str
    job:str
    bio:str

for i in range(11):
    usuario = User()

    usuario.user    = fake.name()
    usuario.birth   = fake.date_between() 
    usuario.phone   = fake.phone_number()
    usuario.bank    = fake.iban()
    usuario.address = fake.address()
    usuario.job     = fake.job()
    usuario.bio     = fake.paragraph(nb_sentences=5)

    # ToDo: Aquí tu código para volcar ese usuario en un ficher, en tu base de datos o en lo que necesites... 
```

Hasta aquí este pequeño tutorial sobre el uso de esta interesante librería. Insisto en que las opciones de personalización y los tipos de campos que puedes generar van mucho más allá de lo que aquí hemos visto y de nuevo te recomiendo que mires la documentación oficial de [Faker](https://faker.readthedocs.io/en/master/). Espero que esto te sirva para no tener que generar datos de prueba a mano nunca más. Recuerda, __si vas a hacerlo más de dos veces, automatizalo__.
