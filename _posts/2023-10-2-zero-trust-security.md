---
layout: post
header:
    image: /assets/images/zero-trust-security/gatito_hacker_2.jpg
    overlay_color: "#000000"
title: Zero Trust Security
description: "En qué consiste este paradigma de seguridad."
excerpt: "Un popular paradigma de seguridad."
tags: [Security]
categories: 
  - Security

---    

Seguramente hayas escuchado o leido alguna vez este concepto, pero quizá no tengas claro en que consiste. Te lo cuento muy brevemente para que no tengas dudas.

Este paradigma de seguridad de cimienta sobre cinco principios básicos, que si bien a veces pueden resultar algo molestos a la hora de trabajar, tratan de garantizar la seguridad al máximo posible.

### Principio de minimo privilegio

![RQ Logo](/assets/images/zero-trust-security/pollito_hacker_1.jpg){: .align-right}
Este seguramente es el que más de cabeza trae a muchos desarrolladores, ya que en ocasiones no nos permite ser tan libres como nos gustaría. Se trata de que cada usuario (ya sea personal o de aplicación) debería tener los principios minimos e imprescindibles para realizar su función.

Es decir, si un usuario necesita acceder a 12 tablas de una base de datos para realizar consultas, no tiene sentido que pueda acceder a todas las demás, ni que pueda realizar otras acciones como INSERT, UPDATE o mucho menos DELETE o DROP. Si solamente tiene acceso a lo que necesita y para lo que necesita es mucho menoss probable que pueda cometer errores que pongan en riesgo la operativa, y en caso de que alguien pueda llegar a tener acceso a su usuario las consecuencias están más contenidas.

Esto, por supuesto, hace la flexibilidad sea mucho más limitada, si mañana una feature de nuestro programa requiere utilizar una tabla que no está dentro de esas 12, será necesario conseguir permisos de acceso nuevos.

### Never trust, always verify

![RQ Logo](/assets/images/zero-trust-security/pollito_hacker_2.jpg){: .align-left}
Este punto pretende que vivamos de una forma algo paranoica, pensando que nunca estamos en un entorno seguro y que siempre tenemos que asegurarnos de que lo que estamos haciendo tiene seguridad por si mismo.

Un ejemplo común se da con aplicaciones que corren en redes internas. Por irnos a un caso simple, podríamos pensar que una aplicación que tengamos corriendo en nuestra casa, dentro de la red local,  no necesita estar segurizada, porque el punto de acceso o el router ya te pide una contraseña para poder acceder a la red, y por lo tanto, para cuando tienes visibilidad de esta aplicación, ya te encuentras en un entorno securizado.

Pero esto no necesariamente tiene por qué ser así, si alguien logra entrar en nuestra wifi, tendrá acceso a todo lo que hay dentro.

Esto, que puede parecer un caso extraño o aislado, se da de forma común en dispositivos de domotica. En los que el fabricante asume que al estar dentro de la wifi de su cliente no tiene que implentar medidas de protección adicional, o que en los que el cliente deja la contraseña que viene por defecto - o peor, la cambia por una del tipo 1234 - por comodidad, pensando que como no le da acceso desde el exterior ya se encuentra a salvo de accesos indeseables. Luego alguien accede a la wifi y... llegan los disgustos.

### Asume branch

Si el anterior punto suponia una vida de descinfianza, este consiste basicamente en vivir en modo paranoico. Parte de la idea de trabajar siempre con la idea de que hay ubn vulnerabilidades y brechas de seguridad que no conocemos, pero que creemos que existen, por lo que debemos trabajar siempre con la idea de minimizar los problemas que puedan surgir si alguien explota esa vulnerabilidad. Mitigando de forma eficiente la situación con la mayor brevedad posible, y trabajando en que restaurar el servicio sea una tarea rápida.

### Punto unico de falla

![RQ Logo](/assets/images/zero-trust-security/gatito_hacker_1.jpg){: .align-right}
Consiste en minimizar la cantidad de puntos que pueden fallar o ser atacados.

Imaginemos que queremos montar una plataforma de Striming, a esta podrán acceder los usuarios desde su ordenador, su televisión, su dispositivo móvil... multiples destinos que quieren alcanzar un unico orgien: Nuestra servicio.

Podriamos optar por utilizar diferentes metodos de acceso a los datos. Por ejemplo, los dispositivos con más recursos podrían funcionar mediante un socket que mantuviera una conexión permanente, de forma que si añadimos contenido nuevo a la plataforma este aparezca instantaneamente reflejado para que el usuario pueda verlo. En otras circustancias, como dispositivos con menor recursos o que se conectan a redes móviles esto podría ser demasiado costos para que funcione con fluided, así que decimios generar una API que, bajo demanda, devuelva el contenido solicitado para que sea consumido. Por ultimo tenemos el papel de los administradores, que van a realizar otras acciones, quizá más amplias y que requieren flexibilidad a la hora de acceder y poder realizar acciones. En este caso optamos por atacar directamente a la base de datos.

Estamos generando tres puntos de acceso. Tres potenicales sitios desde los que usuarios malintenciados podrían intentar atacarnos. Tres puntos que tenemos que mantener y actualizar. Y securizar en un momento dado, lo que requiere estar al día de vulnerabilidades y z-days en tres tecnologias distintas. Esto es precisamente lo que este punto pretende evitar.

Lo idea, siguiendo esta idea, sería decantarnos por un unico punto. El punto medio entre los tres (Y más recomendable en la mayría de los casos) sería quedarnos con la API y deshechar el resto de opciones. De esta manera podemos volcar todos nuestros esfuerzos en un unico sitio y seremos menos accesibles en caso de que alguien quiera darnos problemas.

### Data Masking

En la mayoría de las ocasiones es necesario probar nuestras apliaciones con datos. Estos datos, en medida de lo posible, deberíamos evitar que fuesen reales. A fin de cuentas, estamos haciendo pruebas y no sabemos como de mal pueden llegar a ir en un momento dado. El uso de datos reales puede desembocar en fugas de información o en dejar expuesto datos senisbles.

En este caso podemos optar por dos estrategias:

Generar datos falsos, usando por ejemplo faker, [del que ya os hablamos en otra ocasión](https://lacodeteca.com/python/testing/crear-datos-de-prueba/)

O, si por la naturaleza de nuestro desarrollo esto no es posible, usar Data Masking para ofuscar la información y que siga siendo compatible con nuestro sistema. A grandes rasgos y de una forma muy simple, consiste en lo siguiente. Supongamos que nuestra muestra de datos son estas personas:

|  Nombre | Apellido  | Religión  | RH  | Documento de identidad  |
|---|---|---|---|---|
| Juan  | Palomo Ortiz  |  Catolico  | +  | 12345678  |
| Maria | Ruiz Sánchez  |  Budista   | -  | 98765431  |
| Cris  | Olmet Urrita  |Protestante | -  | 23455678  |

Estos datos tienen multitud de información sensible y de caracter personal. Usarla podría exponerla y suponer un problema de seguridad. Pero por desgracia para nosotros, nuestro sistema necesita cierta consistencia entre ellos para poder funcionar. Aplicando un data masking simple podríamos utilizar algo similar a esto:

|  Nombre | Apellido  | Religión  | RH  | Documento de identidad  |
|---|---|---|---|---|
| Juan  | Urrita Sánchez  |  Catolico  | +  | xxxxxxxx  |
| Maria | Olmet Ortiz     |  Budista   | -  | xxxxxxxx  |
| Cris  | Ruiz Palomo     |Protestante | -  | xxxxxxxx  |

Hemos distribuido los apellidos de forma aleatoria, haciendo que esa pesona ya no exista. COmo el número del documento de identidad no lo vamos a usar para lo que queremos, directamente lo sustituimos por valores que no aportan nada. Y lo que estamos manteniendo es la correlación entre la religión y el RH, porque en nuestra hipotetica aplicación es lo que estamos buscando.

De esta forma, mantenemos la información que nos interesaba de forma fiel, pero ya no estamos usando datos de caracter personal.

## Conclusiones

Como ves, el paradigma de zero-trust-security es en realidad una serie de consejos y buenas prácticas que nos recomiendan para manenter la seguridad en lo que hacemos.

Siempre es complicado mantener el equilibrio entre seguridad y usabilidad. Un entorno demasiado controlado es poco flexible y tiende a ser incomodo. Un entorno demasiado comodo suele no ser seguro. Encontrar el equilibrio entre ambos es una tarea compleja, que suele llevar tiempo, mucha prueba y error y algún que otro susto en algunas ocasiones.

¿Qué opinas? ¿Añadirías algo más?
