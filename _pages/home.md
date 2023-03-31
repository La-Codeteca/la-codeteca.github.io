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
  <small><a href="https://twitter.com/trastejant"><i class="fab fa-fw fa-twitter-square"></i></a></small> 
  ·
  <small><a href="https://youtube.com/trastejant"><i class="fab fa-youtube"></i></a></small> 

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

{% assign entries_layout = 3 | default: 'list' %}
{% assign postsByYear = site.posts | where_exp: "item", "item.hidden != true" | group_by_exp: 'post', 'post.date | date: "%Y"' | limit: 3 %}
{% for year in postsByYear limit:1 %}
  <section id="{{ year.name }}" class="taxonomy__section">
    <div class="entries-{{ entries_layout }}">
    <div class="row">
      {% for post in year.items  limit:3 %}
      <div class="col-sm-6">
        <div class="card">
        <h5 class="card-title"><a href="{{post.url}}">{{post.title}}</a></h5>
        
        <span style="font-size:.6rem">{{ post.date | date_to_string  }}</span>
        <p class="card-text">{{post.excerpt | strip_html | truncatewords: 30}}</p>
        </div>
        </div>
      {% endfor %}
      </div>
    </div>
    <a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
  </section>
{% endfor %}
