---
layout: post
title:  "Introducción Git"
date:   2020-03-20 14:30:00 +0200
categories: GitHub
order: 1
parent: GitHub
---

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_github/img1.png)
{:refdef}

# GITHUB

GitHub es una plataforma de desarrollo que permite alojar proyectos utilizando un control de versiones, siendo el más ampliamente utilizado Git.

# CREAR CUENTA

[GitHub](https://github.com/){: .btn .btn-green }

## Registro:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_github/img2.png)
{:refdef}

## Plan gratuito:
* Permite repositorios privados
* Hasta 3 colaboradores (BitBucket 5 y GitLab sin límite)

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_github/img3.png)
{:refdef}

## Al entrar por primera vez en nuestra cuenta aparecerá la siguiente pantalla:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_github/img4.png)
{:refdef}

Campos importantes:
* Nombre del repositorio: Suele tener ser parecido al proyecto que contiene.
* Público/Privado: Siendo público será visible para todo el mundo.
* Add .gitignore: Posiblemente el más importante:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_github/img5.png)
{:refdef}

Busca en el menú desplegable el lenguaje de programación del proyecto. Esto genera un fichero .gitignore con todas las carpetas y extensiones de fichero que ignorará a la hora de subir el proyecto. Básicamente sirve para no subir elementos como por ejemplo, los binarios de java o carpetas de configuración. Se supone que en GitHub almacenaremos únicamente el código.

Contenido de .gitignore para un proyecto java:

```
# Compiled class file

*.class



# Log file

*.log



# BlueJ files

*.ctxt



# Mobile Tools for Java (J2ME)

.mtj.tmp/



# Package Files #

*.jar

*.war

*.nar

*.ear

*.zip

*.tar.gz

*.rar



# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml

hs_err_pid*
```

Una vez creado podremos ver todos nuestros repositorios:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_github/img6.png)
{:refdef}
