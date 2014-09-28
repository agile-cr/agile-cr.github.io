---
layout: post
title: "Cómo funciona el blog"
description: "Pequeño manual para usar octopress"
date: 2014-09-28 12:20:44 +0200
comments: true
categories: 
- blog
---

En este pequeño artículo se repasará lo básico sobre cómo funciona el blog.

## Estructura básica

Hay dos ramas:

### Rama Source

La rama **source** contiene los fuentes de la página. Cualquier cambio debe realizarse o mergearse contra esta rama. Más adelante hablaremos de cómo gestionarla.

### Rama Master

Contiene los HTML ya compilados. Normalmente la descargaremos en el directorio `_deploy` y se gestionará automáticamente.

## Preparación del entorno

Primero nos clonaremos el repositorio y nos situaremos en la rama `source`::

    git clone git@github.com:agile-cr/agile-cr.github.io.git
    cd agile-cr.github.io
    git checkout -t origin/source

A continuación crearemos la carpeta `_deploy` con otro clon del mismo repositorio, pero en la rama `master`:

    git clone git@github.com:agile-cr/agile-cr.github.io.git _deploy

Finalmente, nos descargamos todo lo que necesitamos. Tendremos que tener instalado **ruby**, **gem** y **bundler**:

    bundle install --path vendor/bundle

## Realizando modificaciones

En la rama `source`, podemos editar cualquier página existente. También podemos crear contenido nuevo:

### Posts

Se crea una plantilla nueva con::

    rake new_post["Título del artículo nuevo a crear"]

Acordáos de añadir la propiedad `description` y `author`. Elegid las `categories` con cuidado, a ser posible coincidiendo con alguna ya existente.

Una vez editado, basta con comitear y pushear.

### Pages

Se crea una plantilla nueva con::

    rake new_page[nombre_de_la_pagina]

Acordáos de añadir la propiedad `description` y quitar `date` y `comments`. Muy probablemente también queráis enlazarlo, modificando `source/_includes/custom/navigation.html`.

Una vez editado, basta con comitear y pushear.

## Publicar

Si tenemos todo preparado, bastará con:

    bundle exec rake deploy