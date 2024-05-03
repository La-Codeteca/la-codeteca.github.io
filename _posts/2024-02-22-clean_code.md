---
layout: post
toc: true
comments: true
share: true
author_profile: false
header:
    image: /assets/images/solid/SOLID.png
    overlay_color: "#000000"
title: Código limpio, Nombres
description: "Una buena elección de nombres mejora enormemente la legibilidad de tu código."
excerpt: "Una buena elección de nombres mejora enormemente la legibilidad de tu código."
tags: [clean code ,best practices, developer]
categories: 
  - Best_Practices

---


## Nombres claros, expresivos y descriptivos

Algo que ayuda mucho, muchisimo a la legibilidad del código es utilizar nombres descriptivos para variables, funciones, clases, metodos... etc. Hay que desterrar para siempre el uso de letras sueltas, palabras como _aux_ o _temp_ y cualquier opción que solamente con leerlas no nos aporten información sobre lo que hacen o contienen.

No siempre es fácil encontrar un nombre, de hecho te encontraras que algo que en principio parece tan sencillo en ocasiones es realmente complejo, pero merece la pena pararse a pensarlo por el tiempo que te vas a ahorrar despues pensando "y a esto como lo llamé" y revisando que hace y contiene cada elemento. Si solo con leer lo puedes entender tu código va a ser mucho más claro y mantenible.

### Variabes: Nombres según el tipo de datos

Cuando creemos una variable, pongamos un nombre que indique que es lo que va a contener. Si lo que va a contener es una temperatura, llamemosle temperatura. Da igual que esta solo se vaya a almacenar durante un instante, o que ahora mismo según escribrimos te parezca que llamarla T es una buena opción. No te va a llevar demasiado tiempo llamarla temperatura y en el futuro, cuando tú mismo y otra persona tenga que leer el código, no tendrá dudas de lo que conetiene.

![Clean Code](/assets/images/clean_code/pollito_y_gatito_limpieza_1.jpg){: .align-left}

Además, es útil seguir este tipo de convenciones para que todo quede aun más claro:

- **Arrays** : ya que este tipo de dato tiene la peculiaridad de almacenar varios elementos, usa plurales. Además, es conveniente que busques la forma de dejar claro el tipo de dato de los elementos que contiene. Por ejemplo, si quieres crear un array que contenga OBJETOS de tipo USUARIO puedes llamar a tu array USUARIOS, mientras que si unicamente va a contener datos de tipo STRING con el nombre del usuario, sería mejor que lo llamases nombresDeUsuarios, por ejemplo. De esta forma, están indicando el contenido y el tipo de lo que está conteniendo.

- **Booleanos** : Usa prefijos como is_ o has_ y siempre en positivo, de esta forma al leerlo tendra más sentido. Por ejemplo, si quieres crear un booleano para determinar si algo esta vacio y lo llamas is_empty, será fácil entender el estado en el que se encuentra, además de lo que indica: _is_empty = true_.

- **Numeros** : En este caso, tan importante como usar nombres representativos es saber si esta indicando  algún tipo de limite o totalización, para eso podemos usar prefijos como max_ min_ total_ para indicar si, por ejemplo, es la temperatura máxima max_temperatura, la minima min_temperatura, o si estamos conteniendo en esa variable un valor calculado a partir de otros valores, cómo podría ser el total_aforo, que podría indicar la suma de todas las personas que han entrado a un local y que podrías estar comparando con el max_aforo que indica la capacidad máxima del sitio. De esta manera queda claro, que significa cada número.

### Funciones

Lo importante es que el nombre indica que hace esa función, para ello lo que mejor se suele entender es usar un verbo y un sustantivo que explique la funcionalidad de la forma más sencilla y concisa posible. Por ejemplo, una función que crea un usuario puede llamarse *createUser*, la que lo actualiza *updateUser*, *deleteUser* para la que lo borra... solamente con leer el nombre te harás una idea bastante concreta de lo que hace.

Esto funciona aún mejor si tenemos presente el principio de responsabilidad única que nos indica [SOLID](https://lacodeteca.com/best_practices/solid/). Porque si una función hace una cosa, y solo una cosa, es más fácil que con un nombre escueto podamos saber que hace, o que buscar cuando queramos cambiarlo.

### Clases

Las clases deberían ser sustantivos: usuario, fruta, producto... Esto suele ser lo más sencillo, ya que una clase no deja de ser la representación de algo con lo que queremos trabajar.
