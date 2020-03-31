---
layout: post
title:  "Ejemplo Switch e ImageView"
date:   2019-10-9 14:30:00 +0200
categories: primer_trimestre
order: 2
parent: Primer trimestre Android
---

# Ejemplo Switch e ImageView

**Ejemplo de clase**: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/SwitcheImageView>

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/swiches_imageView/ejemplo_Sonic.jpg)
{: refdef}

Este ejemplo lo podemos dividir en dos partes:

__1. Utilización de *Switch* y *ToggleButton:*__

{% highlight java %}
public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        // podemos acceder a la id del ToggleButton pulsado en
        //caso de tener varios (comparar con R.id.ToggleButton)
        int id = buttonView.getId();

        Toast.makeText(this, "Pulsado: " + id + " a " + isChecked, Toast.LENGTH_SHORT).show();
    }
{% endhighlight %}

Observa como se puede obtener el estado *(isChecked)* y la id del elemento que se ha pulsado. En caso de querer comprobar el botón que se ha pulsado simplemente podríamos compararlo con *R.id.nombreSwitch.* 


__2. Cambio de imagen tanto en un ImageView como en un ImageButton.__ En este caso nos hemos apoyado de un botón. Al pulsarlo vemos que se ejecuta:

{% highlight java %}
public void imageButton(View v) {
        ImageView imageView = findViewById(R.id.imageView);
        ImageButton imageButton = findViewById(R.id.imageButton);

        if (isSonic) {
            imageView.setImageResource(R.drawable.knuckles);
            imageButton.setImageResource(android.R.drawable.star_big_off);
            isSonic = false;
        }
        else {
            imageView.setImageResource(R.drawable.sonic);
            imageButton.setImageResource(android.R.drawable.star_big_on);
            isSonic = true;
        }
    }
{% endhighlight %}

Ten en cuenta que los recursos que se acceden mediante *android.R.* son recursos que vienen incluidos en la instalación de Android Studio.
 
Por último, observa que modificar en ambos la imagen resulta sencillo. En este caso controlamos si está una imagen u otra y las rotamos.
