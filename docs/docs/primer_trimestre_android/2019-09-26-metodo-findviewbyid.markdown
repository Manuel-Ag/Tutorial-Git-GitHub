---
layout: post
title:  "Método FindViewByID"
date:   2019-09-26 14:30:00 +0200
categories: primer_trimestre
order: 1
parent: Primer trimestre Android
---

# Método FindViewById

Para acceder a una vista (botones, cajas de texto, checkboxes, etc.) deberemos primeramente de referenciar ese elemento:

{% highlight java %}
//En este ejemplo un textView.
TextView myTextView = findViewById(R.id.textViewNombre);
{% endhighlight %}

De esta forma podremos acceder a sus atribunos, asignar un listener, cambiar la visibilidad, etc. Por ejemplo, si quisieramos acceder al texto de ese elemento deberíamos de escribir:

{% highlight java %}
//En este ejemplo un textView.
TextView myTextView = findViewById(R.id.textViewNombre);
String cadena = myTextView.getText().toString();
{% endhighlight %}

Recuerda que aunque en la paleta del diseñador tengamos muchos nombres diferentes, las cajas de texto en las que el usuario puede escribir son un EditText, como se puede ver en el árbol de componetes de la siguiente imagen:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/metodoFindViewById/captura2.jpg)
{: refdef}

En el primer proyecto se puede ver también un ejemplo de esto: [https://github.com/Manuel-Ag/PMD_19-20/tree/master/Primera_aplicacion]


[https://github.com/Manuel-Ag/PMD_19-20/tree/master/Primera_aplicacion]: https://github.com/Manuel-Ag/PMD_19-20/tree/master/Primera_aplicacion
