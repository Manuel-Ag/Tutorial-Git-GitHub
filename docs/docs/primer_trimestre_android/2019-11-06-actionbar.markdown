---
layout: post
title:  "Action Bar"
date:   2019-11-06 14:30:00 +0200
categories: primer_trimestre
order: 1
parent: Primer trimestre Android
---

# Action Bar

En este ejemplo vamos a añadir un menú al Action Bar de una actividad (barra superior)

1\. Creamos el directorio menu:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_actionBar/captura1.jpg)
{: refdef}

2\. Creamos un fichero menu.xml en el directorio recién creado:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_actionBar/captura2.jpg)
{: refdef}

3\. Crearemos el diseño:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_actionBar/captura3.jpg)
{: refdef}

Recuerda algunos atributos importantes para el comportamiento de algunos elementos de la interface: 

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_actionBar/captura4.jpg)
{: refdef}

4\. Desde la actividad inflamos el menú implementado el siguiente método:

{% highlight java %}
    public boolean onCreateOptionsMenu(Menu menu) {
        MenuInflater inflater = getMenuInflater();
        // Indicamos nuestro recurso menú anteriormente creado
        inflater.inflate(R.menu.menu, menu);
        return super.onCreateOptionsMenu(menu);
    }
{% endhighlight %}
	
5\. Y por último, comprobamos cuando el usuario ha pulsado alguna opción:
	
{% highlight java %}
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()) {
            case R.id.item1:
                Toast.makeText(this, "Se ha pulsado el item1", Toast.LENGTH_SHORT).show();
                break;
            case R.id.item2:
                Toast.makeText(this, "Se ha pulsado el item2", Toast.LENGTH_SHORT).show();
                break;
            case R.id.item3:
                Toast.makeText(this, "Se ha pulsado el item3", Toast.LENGTH_SHORT).show();
                break;
            case R.id.item4:
                Toast.makeText(this, "Se ha pulsado el item4", Toast.LENGTH_SHORT).show();
                break;
        }

        return super.onOptionsItemSelected(item);
    }
{% endhighlight %}
	
**Visita los siguientes enlaces para ver un ejemplo en funcionamiento:**

* GitHub: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/MenuActionBar>
* Documentación oficial: <https://developer.android.com/training/appbar?hl=es-419>
* Ejemplo: <https://www.sgoliver.net/blog/action-bar-en-android-i/>





