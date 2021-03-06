---
layout: post
title:  "Introducción GitHub"
date:   2020-03-20 14:30:00 +0200
categories: GitHub
order: 1
parent: GitHub
---

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_github/img1.png)
{:refdef}

# GitHub

GitHub es una plataforma de desarrollo que permite alojar proyectos utilizando un control de versiones, siendo el más ampliamente utilizado Git. Los proyectos se almacenan en la nube, lo que permite trabajar de forma simultánea en el mismo proyecto con otros desarrolladores o, incluso, crear un proyecto abierto que permita a todo el mundo proponer nuevas características o cambios.

Un ejemplo de flujo de trabajo que se podría dar:

* Desarrollador realiza uno o varios cambios en su repositorio local de Git (Commits). Puede realizar los commits que estime oportuno. En estos commits se guarda el estado del proyecto en ese momento.
* Decide que quiere subir todos sus cambios a GitHub, por lo que realiza un Push. Todos los commits guardados en local se guardan también en la nube.
* Otro desarrollador, con una versión más antigua del proyecto, desea actualizar su proyecto a la última versión que hay en GitHub, por lo que realiza un Pull. Ahora tiene acceso a todos los commits del primer desarrollador.
* Realiza sus propios commits y los sube otra vez a GitHub mediante un Push.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_introduccion_github/img7.png)
{:refdef}

# Crear cuenta

[Enclace GitHub](https://github.com/){: .btn .btn-green }

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
