---
layout: post
toc: true
comments: true
share: true
author_profile: false
header:
    image: /assets/images/paginacion/paginacion.png
    overlay_color: "#000000"
title: Cinco atajos imprescindibles de VS code
description: "No apartar las manos del teclaro ahorra muchisimo tiempo, aquí te dejo los atajos de Visual Studio Code sin los que yo ya no sé vivir."
excerpt: "No apartar las manos del teclaro ahorra muchisimo tiempo, aquí tedejo los atajos de Visual Studio Code sin los que yo ya  no sé vivir."
tags: [ developer, VS code]
categories: 
  - Developer

---   


Depende de la configuración de Visual Studio Code y el sistema operativo estos atajos pueden no ser los mismos para ti. Lo importante no es si esta combinación de teclas u otra, ya que son configurables y hacer tu propia paleta de comandos que te resulte más sencilla de recordar. Lo importante es que sepas que existen estos atajos en Visual Studio Code, que te ahorrarán mucho tiempo.

Aquí te dejo los atajos sin los que yo no sé vivir.

## Mover lineas

A veces necesitamos subir o bajar una línea a otra posición. Podemos copiarla y pegar, pero es más rápido usar este atajo de teclado:
Alt + Flecha

![alt + flecha](/assets/images/mis-atajos-vscode/kbs_alt_arrowdown.png){: .align-center}
![Mover linea](/assets/images/mis-atajos-vscode/mover_lineas.gif){: .align-center}

## Comentar bloques de código

Muchas veces necesitamos comentar un trozo de código, por ejemplo para ver cómo se comporta el código sin esa parte o para ejecutar una parte especifica del mismo. Una opción es irse al principio, colocar el caracter de inicio de comentario, luego irse a la ultima, colocar el caracter de cierre del comentario... pero también podemos seleccionar el bloque de código y hacer:

Ctrl + shift + /

```bash
commentline
```

![Ctrl + shift + /](/assets/images/mis-atajos-vscode/kbs_ctrl_shift__.png){: .align-center}
![Comentar bloque](/assets/images/mis-atajos-vscode/comentar_bloque.gif){: .align-center}

## Copiar una línea arriba o debajo

A veces necesitamos crear varias líneas muy similares, este atajo nos permite copiar la línea en la que estamos por encima o por debajo del punto en el que estamos

Mayusculas + Alt + Fecha

![Mayusculas + Alt + Fecha](/assets/images/mis-atajos-vscode/kbs_alt_shift_arrowup.png){: .align-center}
![Clonar lineas](/assets/images/mis-atajos-vscode/clonar_linea.gif){: .align-center}

## Multicursores

Los multicursores son una de las herramientas más útiles de cualquier IDE moderno. Nos permite realizar ediciones en varias líenas de forma simultanea. Lo que normalmente nos ahorra muchisimo tiempo. Podemos generar nuevos cursores con esta combinación de teclas.

Ctr + Alt + Flecha

![Ctr + Alt + Flecha](/assets/images/mis-atajos-vscode/kbs_ctrl_alt_arrowup.png){: .align-center}
![Multicursor](/assets/images/mis-atajos-vscode/multi_cursor.gif){: .align-center}

Puedes configurarlo buscando la configuración de los atajos:

```bash
Add Cursor Above/Belowe
```

## Pasar un texto (o una letra) a mayusculas

alt + shift + pageUp

![alt + shift + pageUp](/assets/images/mis-atajos-vscode/kbs_alt_shift_pageup.png){: .align-center}
![alt + shift + pageUp](/assets/images/mis-atajos-vscode/uppercase.gif){: .align-center}

Puedes configurarlo buscando la configuración de los atajos:

```bash
Tranform To Uppercase
```

Todos estos comandos son configurables, puedes buscar en la paleta de comandos "shortcut" o presionar ctrl + k + s para acceder al menú de configuración de los atajos. Te recomiendo que los configures de forma que te resulten cómodos de usar y fáciles de recordar y verás como tu velocidad usando la herramienta aumenta notablemente en poco tiempo.

---

<div class="aditional-info">

  <h2>/** Comentarios del post **/</h2>

  <h3> # Todos los enlaces:</h3>
  <ul>
    <li> // <a href="https://code.visualstudio.com/">Pagina oficial de Visual Studio Code</a></li>
  </ul>


  <h3> # Recursos usados:</h3> 
    <ul>

      <li> // <a href="https://monsterbrain.github.io/keyboard-shortcut-image-generator/">Generador de imagenes de teclas</a></li>
      
    </ul>
</div>
