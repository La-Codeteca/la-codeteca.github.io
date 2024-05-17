---
layout: post
toc: true
comments: true
share: true
author_profile: false
header:
    image: /assets/images/patrones/frase_motivacional.png
    overlay_color: "#000000"
title: Programa como... 
description: "Vamos a repasar algunos patrones, principios y conceptos que te ayudarán a escribir mejor código."
excerpt: "Vamos a repasar algunos patrones, principios y conceptos que te ayudarán a escribir mejor código."
tags: [development, SOLID, KISS, STUPID, Clean Code, DRY, technical debt]
categories: 
  - Development

---  

![Clean Code](/assets/images/patrones/frase_motivacional.png){: .align-center}

Siempre que vayas a empezar un nuevo proyecto o hacer una actualización de uno existente, deberías tener presente esa preciosa frase motivacional que encabeza esta entrada.

Mucha gente programa pensando que si hace cosas muy complejas, muy enrrevesadas, muy dificiles de entender se van a convertir en imprescindibles en su empresa y van a tener el puesto asegurado. Nada más lejos de la realidad. Nadie en esta vida es imprescindible, lo unico que estas haciendo es dejar una deuda a los que vengan detrás, una fuente de frustraciones y un potencial nido de problemas. Cada función que es creas es tu portfolio, una oportunidad para demotrar la calidad de tu trabajo. Por lo tanto debería demostrar lo que eres capaz de hacer, y nada demuestra más tu profesionalidad que escribir código de calidad, sencillo, fácil de entender, expandir y modificar.

Una muestra de buena artes es seguir los patrones de diseño que están establecidos. Recuerda que cuando sigues un estandar o un patrón no estas sometiendote a la forma de hacer las cosas de otros, estás empleando una manera de hacer las cosas que se usa habitualmente y que por lo tanto esta probada, revisada y ya se ha topado con problemas y muros que, si no sigues, probablemente termines encontrandote, así que ¿por qué no aprovecharnos de los errores que los demás ya han tenido que solucionar para empezar un peldaño más alto?

En este sentido, te diría que _no seas [STUPID](https://lacodeteca.com/best_practices/stupid/), hagas cosas [SOLID](https://lacodeteca.com/best_practices/solid/) con mucho [KISS](https://lacodeteca.com/best_practices/kiss/)_. Y si, como habrás podido deducir por los enlaces, la elección de palabras no es aleatoria. Se trata de buenas prácticas y patrones de diseño que te será muy útil conocer. Luego la forma de implementarlos ya depende de tí.

### STUPID

- **S**ingleton
- **T**ight coupling
- **U**ntestable
- **P**remature optimizacion
- **I**indescriptible naming
- **D**uplication : Nunca me cansaré de decirlo y nunca lo diré lo suficiente... **NO** repitas código. Sobre esto hay otro principio, llamado [DRY](https://lacodeteca.com/best_practices/dry/)

Puedes ver una entrada en la que tratamos con más detalle cada punto en [esta entrada](https://lacodeteca.com/best_practices/stupid/).

### SOLID

- **S**ingle Responibility: Principio de responsabilidad única, o lo que es lo mismo, que cada función haga una sola cosa, pero que la haga muy bien.
- **O**pen and Close: Cerrado a la expansión, pero cerrada a la modificación.
- **L**iskov Sustitution: Cuando defines una clase, debe ser lo suficientemente generica y sencilla como para que ningún caso requiera no usar algún elemento.
- **I**nterface Segregation:
- **D**ependency Inversion:

Si quieres saber más sobre lo que significa e implica cada punto en este [otro post](https://lacodeteca.com/best_practices/solid/)

### KISS

- **K**eep
- **I**t
- **S**imple
- **S**tupid

Aprende más sobre KISS [aqui](https://lacodeteca.com/best_practices/kiss/) y sobre otro principio muy relacionado, el de [YAGNI](https://lacodeteca.com/best_practices/yagni/)

## Código limpio

No, no te voy a decir que si no te has leido [Clean Code](https://www.fnac.es/a8671601/Clean-code-a-handbook-of-agile-soft) no tienes derecho a tocar un teclado. Sinceramente - y esta es mi opinión y solo eso - ese libro no está mal, pero no vale la fama que tiene.

![Clean Code](/assets/images/clean_code/pollito_y_gatito_limpieza_1.jpg){: .align-right}

Tener un ejemplar de este popular "tocho" no te hará mejor desarrollador, lo que si lo hará es seguir estas sencillas normas:

- Usa nombres claros y expresivos. No les pongas nombres a tus variables tipo _a_ o _aux_, usa nombres que al leerlos sepas que se está almacenando ahí, sin necesidad de leer el código compleot. Esto también aplica a las funciones y las clases.

- Dependiendo del lenguaje a veces es más habitual usar Camel Case o Snake Case. Pero si no hay un estandar para el lenguaje que estas usando, se consistente: elige uno y usalo igual en todas partes.

- Idealmente evita recibir más de 3 parametros en una función.

- Evita replicar código.

Solo con estos cuatro puntos tu código será mucho más legible, pero [aquí](https://lacodeteca.com/best_practices/clean_code/) puedes ver de forma más detallada algunas cosas más que te ayudarán a escribir código más limpio.

## Deuda técnica

La deuda técnica tiene mala fama, pero es tan inevitable como necesaria en muchas ocasiones. Cuando tenemos escaneos como puede ser [Sonar Qube](https://www.sonarsource.com/products/sonarqube/) a veces nos obsesionamos con que la deuda técnica sea 0. Es cierto que es lo ideal, aquello a lo que todos debemos aspirar. Pero también es ideal liquidar la hipoteca y no por ello vas a ir ahora mismo corriendo a hacerlo ¿no?, sea por falta de tiempo, de medios, o porque las prioridades sean otras, no siempre es posible liquidar las deudas. Y en ocasiones eso no es malo, siempre que seamos conscientes de ello y no se nos vayan de las manos. Lo que si te recondaría - en deuda técnica y de cualquier otro tipo - es que la tendencia siempre sea hacia hacerla más pequeña. Nunca es buena idea dejar aumenten de forma continuada y sostenida. Mucho menos exponencial.

Si profundizamos un poco más, existen cuatro tipos de deuda técnica:

- **Imprudente y deliberada**: Es lo que comunmente se dice "hazlo de cualquier forma, lo importante es que funcione". O peor aún "haz que funcione y ya en despúes lo hacemos bien". Spoiler: Nunca llegará ese despúes. Quién dijo aquello de que el camino al infierno está empedrado con buenas intenciones, estaba pensando en la duda técnica imprudente y deliberada. Ese momento libre para hacer esto nunca llegará, porque incluso si llega, la marañan que habrá para entonces hará más sencillo empezar de 0 que arreglar lo hecho. Sencillamente evita meterte aquí.

- **Imprudente e involuntaria**: La más peligrosa. La que crece sin limite y además sin ser consciente de ello. Un ejemplo claro es lo que se conoce cómo código spagetti. Que hace muy complicado mantener o evolucionar ese software.

- **Prudente e involuntaria**: Es una deuda comedida y contenida. Pequeña, pero al no ser conscientes de su existencia es probable que crezca sin control, convirtiendose en la categoría anterio.

- **Prudente y deliberada**: La más aceptable y hasta sana. Aquella que dejamos a sabiendas de que es algo a lo que hay que poner solución, y dejamos acotada y documentada para ser consiences de lo que supone, las implicaciones que tiene y cual debería ser la vía para solventarla.

En cualquiera de los casos, la deuda se paga refactorizando el código. Y para esto es **Muy recomendable** tener test automaticos para validar que la refactorización no ha roto nada. Cuando pagamos deuda técnica no buscamos cambiar la funcionalidad de nuestra aplicación, ni añadir nada nuevo. Buscamos que siga haciendo lo mismo, pero mejor hecho, ya sea a nivel de rendimiento o de mantenibilidad del código. Por eso los test son una herramienta tan importante. Los test deberían pasar exactamente igual antes de la refactorización que despúes. Si lo hemos hecho bien, nuestros test no deberían enterarse de que hemos hecho cambios.

Me gustó mucho esta charla que vi hace tiempo sobre vivir con deuda tecnica:

{% include video id="YyWiJLzjdhE" provider="youtube" %}
