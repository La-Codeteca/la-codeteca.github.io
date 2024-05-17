---
layout: splash
permalink: /
hidden: true
header:
  overlay_color: "#000000"
excerpt: >
  Si vas a hacerlo más de dos veces, automatizalo.<br />
  <small><a href="https://github.com/La-Codeteca"><i class="fab fa-github"></i></a></small> 
  ·
  <small><a href="https://twitter.com/lacodeteca"><i class="fab fa-fw fa-twitter-square"></i></a></small> 
  ·
  <small><a href="https://www.youtube.com/@La_Codeteca"><i class="fab fa-youtube"></i></a></small> 

feature_row:
  - image_path: /assets/images/coffe.png
    alt: "customizable"
    title: "Vídeo"
    excerpt: "Tutoriales y sesiones de livecoding en vídeo. No te pierdas el canal de Youtube de La Codeteca"
    url: "/videos/"
    btn_class: "btn--primary"
    btn_label: "Ver más"
  - image_path: /assets/images/coffe.png
    alt: "fully responsive"
    title: "Blog"
    excerpt: "Tutoriales, noticias, eventos, información para mantenerse al día."
    url: "/blog/"
    btn_class: "btn--primary"
    btn_label: "Ver más"
  - image_path: /assets/images/coffe.png
    alt: "100% free"
    title: "Pildoras"
    excerpt: "Snippets o Gist... llamalos como quieras, ¡Lo importante es que son funciones que funcionan!"
    url: "/pildoras/"
    btn_class: "btn--primary"
    btn_label: "Ver más"      
---

{% include feature_row %}

## Ultimas entradas:

<div class = "last_post">
{% for post in site.posts limit:4 %}
<div class = "grid__item">

  <article class = "archive__item">
    <div class = "archive__item-teaser">
      <img src="{{post.header.image}}" alt="">
    </div>
    <h2><a href="{{post.url}}">{{post.title}}</a></h2>
      <p class="page__meta">
      <span class="page__meta-readtime">
        <i class="far fa-clock" aria-hidden="true"></i>
          {{ post.date | date_to_string  }}
      </span>
      </p>
    <p class="archive__item-excerpt" itemprop="description">{{post.excerpt | strip_html | truncatewords: 30}}</p>
  </article>
</div>
{% endfor %}

</div>

<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
