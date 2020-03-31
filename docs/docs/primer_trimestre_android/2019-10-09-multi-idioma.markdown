---
layout: post
title:  "Compatibilidad entre distintos idiomas"
date:   2019-10-9 14:30:00 +0200
categories: primer_trimestre
order: 2
parent: Primer trimestre Android
---

# Compatibilidad entre distintos idiomas

**Ejemplo de clase**: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/Directorio_values>

Es hora de quitar los *warnings* que teníamos hasta ahora en el diseñador: 

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/multi_lenguaje/warnings.jpg)
{: refdef}

Para ello, únicamente deberemos definir en el fichero *strings.xml* de la carpeta *values* las cadenas que utilizará nuestro programa, por ejemplo el texto de nuestros dos botones:

{% highlight xml %}
<resources>
    <string name="app_name">Name application</string>

    <string name="btn_aceptar">Accept</string>
    <string name="btn_cancelar">Cancel</string>
</resources>
{% endhighlight %}

A continuación, en las vistas que muestren texto, se deberá realizar una referencia al fichero *strings.xml* utilizando como primer caracter *@*:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/multi_lenguaje/captura1.jpg)
{: refdef}

Los *warnings* relativos al texto *hardcoded* deberían de desaparecer. 

Ya tenemos nuestra aplicación casi preparada para soportar varios idiomas. Únicamente falta un paso; crear otro fichero *strings.xml* para cualquier otro idioma soportado por nuestra aplicación. Simplemente deberemos hacer click derecho en la carpeta *res* y a continuación *New>Android resource file*. Nos mostrará la siguiente ventana:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/multi_lenguaje/Captura2.jpg)
{: refdef}

Observa que podemos añadir diferentes restricciones. Nos centraremos en las de idioma. Selecciona *Locale* y pulsa la flecha doble para añadir, a continuación seleccionamos el idioma español de cualquier región (observa como el *Directory name* va variando según añadimos parámetros). Al finalizar se mostrará una estructura como la siguiente:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/multi_lenguaje/captura3.jpg)
{: refdef}

La clave estará en replicar las cadenas definidas en el fichero *strings.xml* del inicio en el fichero *strings.xml* del idioma seleccionado, traduciendo el texto pero manteniendo el nombre de la cadena a la que hacemos referencia en el botón. 

{% highlight xml %}
<resources>
    <string name="app_name">Nombre aplicación</string>

    <string name="btn_aceptar">Aceptar</string>
    <string name="btn_cancelar">Cancelar</string>
</resources>
{% endhighlight %}

De esta forma Android automáticamente seleccionará el fichero con los recursos correspondientes al idioma seleccionado, en este caso el español. Cuando cambiemos el idioma del sistema operativo a español, la aplicación cambiará también de idioma si tiene recursos para ese idioma específico. Es una buena práctica de programación que siempre definiamos las cadenas en un fichero *.xml* aunque solo tengamos compatibilidad con un idioma.


Continuando con el ejemplo de clase, podrás observar que también se cambia la imagen del ImageView. Esto es porque también podremos crear una carpeta de imágenes según idioma, región, características del dispositivo, etc., al igual que con el fichero *strings.xml*. En este caso, comprueba la estructura real del proyecto, seleccionando la vista *Project* (arriba izquierda):

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/multi_lenguaje/captura4.jpg)
{: refdef}

Al igual que para la carpeta *values*, para la carpeta *drawable* hemos creado su versión para español. Para crear una carpeta simplemente haz click derecho en la carpeta *res* y a continuación en *New>Android Resource Directory*:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/multi_lenguaje/captura5.jpg)
{: refdef}

Los dos recursos deben de tener el mismo nombre, ya que será el que se utilizar para referenciarlo desde el atributo de la vista (el formato puede ser distinto). 

Con todo esto ya sabemos como hacer una aplicación que muestre unos textos e imágenes dependiendo del idioma seleccionado en el sistema operativo Android.

Ejemplo de youtube: <https://www.youtube.com/watch?v=ffjLi4Cwg1k>

