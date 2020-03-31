---
layout: post
title:  "Primera aplicación"
date:   2019-09-25 14:30:00 +0200
categories: primer_trimestre
order: 2
parent: Primer trimestre Android
---

# Primera aplicación

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/android.jpg)
{: refdef}

Para esta primera aplicación utilizaremos los elementos <b>TextView, Button y EditText</b>

La aplicación tendrá el siguiente aspecto:

{:refdef: style="text-align: center;"}
![Android1]({{ site.baseurl }}/assets/primeraApp/captura4.jpg)
{: refdef}

El layout utilizado será el de por defecto ConstraintLayout

{:refdef: style="text-align: center;"}
![Android2]({{ site.baseurl }}/assets/primeraApp/captura2.jpg)
{: refdef}

Observa como está organizado el layout. Simplemente arrastra los puntos blancos donde quieras añadir una restricción. Haciendo ajustes en el diseñador se modificará automáticamente el fichero .xml.

Video ConstraintLayout: <a href="https://www.youtube.com/watch?v=Vf3_NqnG7bM">https://www.youtube.com/watch?v=Vf3_NqnG7bM</a> 


A continuación programamos los botones. Hemos puesto 3 botones de 3 formas diferentes.

<b>Forma 1:</b> Implementamos la interface <b>View.OnClickListener</b>

{% highlight java %}
public class MainActivity extends AppCompatActivity implements View.OnClickListener{
{% endhighlight %}

En esta forma deberemos configurar los listener del botón:

{% highlight java %}
        //listener forma1
        boton1 = findViewById(R.id.buttonTipo1);
        boton1.setOnClickListener(this);
{% endhighlight %}

E implementar el método OnClick:

{% highlight java %}
public void onClick(View v) {
        //Hago referencia al elemento que quiero capturar
        EditText campoTexto = findViewById(R.id.editText);
        //Cojo el texto
        String textoUsuario = campoTexto.getText().toString();
        //Y lo muestro en una tostada
        Toast.makeText(this, textoUsuario, Toast.LENGTH_LONG).show();

    }
{% endhighlight %}

En este caso al pulsar el botón llamamos hacemos una referencia, cojemos el texto y a continuación mostramos el texto en una tostada.

<b>Forma 2:</b> Definimos el método a llamar en el fichero .xml

Se crea un método cualquiera con la siguiente estructura:

{% highlight java %}
 public void forma2(View v) {
		//Tostada para comprobar que funciona
        Toast.makeText(this, "Forma 2 de poner un botón", Toast.LENGTH_SHORT).show();
    }
{% endhighlight %}

A continuación especificaremos el método creado en el atributo onClick del botón:

{:refdef: style="text-align: center;"}
![Android3]({{ site.baseurl }}/assets/primeraApp/captura3.jpg)
{: refdef}

<b>Forma 3:</b> Definir el listener y la referencia al botón a la vez.

De esta forma unicamente deberemos de copiar el siguiente código en el método onCreate de la Actividad:

{% highlight java %}
//tercera forma de hacer un botón
        final Button boton3 = findViewById(R.id.buttonTipo3);
        boton3.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                // Code here executes on main thread after user presses button
                Toast.makeText(MainActivity.this, "No necesito implementar la interface", Toast.LENGTH_SHORT).show();
            }
        });
{% endhighlight %}


Todo el código está en: [https://github.com/Manuel-Ag/PMD_19-20/tree/master/Primera_aplicacion]


[https://github.com/Manuel-Ag/PMD_19-20/tree/master/Primera_aplicacion]: https://github.com/Manuel-Ag/PMD_19-20/tree/master/Primera_aplicacion
