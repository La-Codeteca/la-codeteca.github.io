---
layout: post
header:
    image: /assets/images/lowconsumption.png
title: Mejora la observabilidad de tu NGINX
description: "Activar el módulo de status del NGINX nos permite conocer el estado del servicio de una forma sencilla. "
excerpt: "Activar el módulo de status del NGINX nos permite conocer el estado del servicio de una forma sencilla."
tags: [observability, SRE, NGINX]
categories: 
  - Observability
header:
  overlay_color: "#000000"

---    

Seguramente uses, o al menos hayas oido hablar de NGINX. De un tiempo a esta parte se ha convertido en una pieza habitual de software en nuestros despliegues,
ya que permite exponer un servicio web con opciones y funcionalidades para simplificar tareas como el balanceo de carga, además de poder ser empleado como
proxy inverso.

Cuanto más importante se hace un elemento, más importante es controlar su estado, aquí es dónde cobran especial importancia la monitorización y la observabilidad.
Dos conceptos fundamentales si queremos estar seguros de dar un servicio confiable a nuestros usuarios.

En este sentido Nginx cuenta con un módulo que no todo el mundo conoce, pero que permite mejorar la monitorización de una forma muy sencilla. Este módulo,
que generalemnte viene ya pre-instalado (aunque deshabilidado en algunos casos) es el **ngx_http_stub_status_module**. Que nos provee de una sencilla pero eficiente "_status page_" en la que podemos ver datos como el número total de clientes conectados, peticiones aceptadas, solicitudes procesadas, conexiones... entre otras.

Lo primero es ver si el módulo está habilitado. Podemos hacerlo con el siguiente comando:

 ``` 
 nginx -V 2>&1 | grep -o with-http_stub_status_module
 ```

Si este comando devuelve algo significa que el módulo está activo (generalmente lo estará), en caso contrario, será necesario seguir estas indicaciones para conseguirlo: [compile NGINX from source ](https://www.tecmint.com/install-nginx-in-centos-7/)

En caso de estar corriendo Nginx en un contenedor, puedes optar por realizar esto en el Dockerfile, aunque si usas alguna de las imagenes oficiales como punto de partida ya contarás con este módulo, por lo que no será necesario:

```
RUN wget http://nginx.org/download/nginx-1.13.12.tar.gz\
tar xfz nginx-1.13.12.tar.gz\
cd nginx-1.13.12/\
./configure --with-http_stub_status_module\
make\
make install
```

Sea como fuere, a estas alturas ya deberíamos tener el módulo activo, solo necesitamos añadir unas líneas al fichero de configuración (ubicado en /etc/nginx/nginx.conf) para poder usarla:
```
server {
    listen 80;
    root /usr/share/nginx/html;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location /nginx_status {
        stub_status;
        allow 127.0.0.1;
        deny all;
 }
}
```
Si quieres poder atacar a esta pagina de status desde una ubicación no que sea localhost, cambia la línea "allow 127.0.0.1" por la IP desde la que quieras atacarla. Por lo general no te recomiendo ir a visitar está pagina para hacer un diagnostico visual, sino recoger la información que en ella se publica con fluent-d para volcarla en un prometheus u otro stack de monitorización.

Ahora reinicia el contenedor, o en caso de tener NGINx corriendo como un servicio del sistema reincialo con:

``` 
nginx -t
```

```
nginx -s reload 
```

Puedes probar que el módulo funciona correctamente accediendo al endpoint que expone mediante http://127.0.0.1/nginx_status o http://www.example.com/nginx_status

⚠️  Recuerda que si tienes nginx corriendo en un contenedor, estas URLs te devolverán un error, ya que internamente para el contenedor no estás accediendo desde 127.0.0.1. Una opción para verificar el comportamiento en este caso, sin tener que abrir más los permisos en el fichero de configuración es entrar en el contenedor y hacer un curl. Por ejemplo:

```
docker exec -it nombreOidDelContenedorDeNginx curl http://127.0.0.1/nginx_status
```

---

 ℹ️ Fuentes:
[How to Enable NGINX Status Page](https://www.tecmint.com/enable-nginx-status-page/)