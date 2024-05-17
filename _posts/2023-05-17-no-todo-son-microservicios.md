---
layout: post
toc: true
comments: true
share: true
author_profile: false
header:
    image: /assets/images/no-solo-microservicios/microservicio.png
    overlay_color: "#000000"
title: No todo en microservicios
description: "Amazon Video pasa parte de aplicativo de microservicios a monolitico."
excerpt: "Amazon Video pasa parte de aplicativo de microservicios a monolitico."
tags: [Backend, developer]
categories: 
  - Arquitectura
  - Devops
---   

Amazon Video a publicado un articulo como el paso de microservicios a una estructura más monolítica ha supuesto un ahorro significativo. Vamos a analizar [su publicación](https://www.primevideotech.com/video-streaming/scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90) antes de ponernos a refactorizar todas nuestras aplicaciones.

![scaling-up-the-prime-video-audio-video-monitoring-service-and-reducing-costs-by-90](/assets/images/no-solo-microservicios/prime_video.png){: .align-center}

A primera vista, es llamativo. Durante años se ha estado diciendo que los microservicios son el futuro, la solución a todos nuestros problemas, la estructura que todo lo puede... Y ahora llega un gigante como Amazon y nos dice que han logrado reducir sus costes 90% pasando de una arquitectura de microservicios a una monolotica. Haciendo que además sea escalable y resiliente. ¿Que esta pasando aquí?¿ __emosido engañados__ ? Bueno, como casi siempre, la cosa no es tan sencilla.

![emosio engañados](https://ep01.epimg.net/verne/imagenes/2020/02/12/articulo/1581533769_341780_1581537731_noticia_normal.jpg){: .align-left}

Lo primero que hay que tener claro es que Amazon Prime Video es una aplicación enooooorme. Y no nos están diciendo que hayan migrado TODO a una estructura monolítica. Tiene partes que están desarrolladas en microservicios. Muchas. Un montón. Lo que han modificado es su sistema de análisis de la calidad del vídeo. Por lo que cuentan en el articulo, Amazon Video cuenta con un sistema que hace una monitorización de las transmisiones que está realizando (bastante impresionante si tenemos en cuenta la cantidad de usuarios simultaneos que debe tener esta plataforma en cualquier momento). Este servicio básicamente supervisa las transmisiones para "darse cuenta" de cuando hay un problema, por ejemplo una desincronización entre audio y vídeo, y ejecuta de manera automática formas de solucionarlo, puedes ver más información sobre como usan [machine learning para realizar este proceso de mejora](https://www.primevideotech.com/computer-vision/how-prime-video-uses-machine-learning-to-ensure-video-quality).

Este sistema, por lo que ellos cuentan, constaba de tres servicios distribuidos. El primero tomaba los flujos de datos y generaba los fotogramas o el audio que estuviera en ese flujo, una vez hecho se lo mandaba a un segundo servicio que se encargaba de analizarlos, buscando defectos como problemas de sincronización o congelación. Y otro más que se encargaba de orquestar este proceso. Decidieron hacerlo así porque, a primera vista, parecía la opción que mejor escalaba y daba como resultado componentes relativamente sencillos que podían ser desarrollados de forma rápida. Pero luego, a la hora de poner esto en producción se dieron cuenta de que esta solución requería de una ingente cantidad de componentes funcionando, que suponía un coste enorme y una complejidad excesiva para un sistema que no dejaba de ser accesorio al servicio. En el articulo original hay una explicación muy pormenorizada de todo el proceso y de dónde encontraron los mayores problemas.

{% include video id="XsxDH4HcOWA" provider="youtube" %}

Simplificando mucho el proceso, lo que hicieron fue agrupar estos tres microservicios en un único servicio monolítico. Y usar las capacidades de AWS para detectar cargar para decidir cunado era necesario escalar la capacidad de ese proceso. Esto supuso un ahorro de infraestructura del 90%, aumentó la capacidad de escalado y permitió mover el servicio de AWS Lambda a Amazon EC2, un servicio significativamente más barato y sencillo. Y esto, además, ha permitido mejorar la experiencia de los usuarios, ya que al tener ahora capacidad de sobra han podido dejar de monitorear las transmisiones con más espectadores y empezar a hacerlo sobre __TODAS__ las transmisiones que se producen en tiempo real.

## Conclusiones

Creo que si algo podemos aprender de este articulo publicado por prime video tech es que no existen soluciones mágicas que se puedan aplicar en todos los casos y lo solucionen todo. Cada vez que hacemos un desarrollo estamos generando una solución a un problema o una necesidad y es necesario realizar un análisis para determinar, no solo la arquitectura, sino la tecnologia, la infra que lo va a sustentar, la manera en la que será más mantenible y sostenible.

Sería ideal poder encontrar una solución universal, decir que un backend en python, con una base de datos Postgres, un front en React y una cola redis es la manera en la que se solucionan todos los problemas, pero lo cierto es que en la actualidad contamos con multitud de recursos y estrategias que podemos combinar para conseguir la herramienta que mejor se adapta a nuestras necesidades.
