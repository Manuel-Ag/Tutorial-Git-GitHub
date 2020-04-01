---
layout: post
title:  "Merge conflict"
date:   2020-03-29 14:30:00 +0200
categories: GitHub
order: 1
parent: Git y GitHub
---

# Merge conflict

Es muy habitual que, habiendo dos o más desarrolladores actualizados sus repositorios locales, modifiquen el mismo fragmento de código. En ese caso, cuando un segundo programador intente hacer push de su repositorio tendrá un merge conflict.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_merge_conflict/img1.png)
{:refdef}

Git siempre avisará de estos problemas. Dependiendo de la herramienta que se utilice, se visualizará de una forma u otra.

### Por Git Bash

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_merge_conflict/img2.png)
{:refdef}

Observa los errores al intentar hacer primero push y luego pull. En este caso es sencillo de resolver. El comando:

```
git status
```
{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_merge_conflict/img3.png)
{:refdef}

Nos dirá el fichero que tiene un conflicto, en este caso el Main. Al abrir el citado fichero el contenido habrá cambiado:
```
<<<<<<< HEAD
// Cambios de local
=======
// Cambios de remoto
>>>>>>> 962c24528930f2a505df70dca166b36cb6088f0d
```
En este caso los comentarios varían, por lo que simplemente es necesario borrar todo lo sobrante y dejar la versión definitiva, con el código correcto, por ejemplo:
```
// Cambio de remoto
```
A continuación, git add ., git commit y git push.

Si intentásemos hacer push desde Git GUI con un conflicto, también saldría el siguiente mensaje:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_merge_conflict/img4.png)
{:refdef}

Y habría que realizar un pull mediante comandos y hacer lo mismo que anteriormente.

### Por Git Desktop

La lógica es la misma, simplemente tendremos una pantalla más visual.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_merge_conflict/img5.png)
{:refdef}

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_merge_conflict/img6.png)
{:refdef}
