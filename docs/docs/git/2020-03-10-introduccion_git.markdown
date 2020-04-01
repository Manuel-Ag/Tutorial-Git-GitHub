---
layout: post
title:  "Introducción Git"
date:   2020-03-10 14:30:00 +0200
categories: Git
order: 1
parent: Git
---

[Pro Git Book español](https://git-scm.com/book/es/v2){: .btn .btn-green }

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_git/git_logo.png)
{:refdef}

# CONTROL DE VERSIONES GIT

Un control de versiones es un sistema que registra los cambios realizados en un archivo o conjunto de archivos a lo largo del tiempo, de modo que puedas recuperar versiones específicas más adelante. Dicho sistema te permite regresar a versiones anteriores de tus archivos, regresar a una versión anterior del proyecto completo, comparar cambios a lo largo del tiempo, ver quién modificó por última vez algo que pueda estar causando problemas, ver quién introdujo un problema y cuándo, y mucho más. Usar un VCS también significa generalmente que si arruinas o pierdes archivos, será posible recuperarlos fácilmente (Git Book).

Aclarar que Git y GitHub comparten parte del nombre pero no son lo mismo ni tienen los mismos objetivos. Podríamos decir que Git se encarga del control de versiones en local y GitHub nos permite guardar ese mismo repositorio en un servidor externo. Hay alternativas tanto para Git como para para GitHub. Si bien es cierto que Git es la tendencia, para GitHub encontramos otras muchas empresas que ofrecen un servicio de similar calidad, como por ejemplo:
* GitLab
* BitBucket
* SourceForge

<iframe width="560" height="315" src="https://www.youtube.com/embed/5sXcjllHphk" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# SISTEMAS DE VERSIÓN CENTRALIZADOS VS DISTRIBUIDOS

En un VCS (Version Control System) centralizado se guarda en un servidor todos los versionados de los ficheros. En un sistema distribuido como Git se replica todo el repositorio.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_git/img1.png)
{:refdef}

# CICLO DE VIDA

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_git/img2.png)
{:refdef}
