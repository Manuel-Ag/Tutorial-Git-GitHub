---
layout: post
title:  "Recorrido de un TableLayout"
date:   2019-10-17 14:30:00 +0200
categories: primer_trimestre
order: 2
parent: Primer trimestre Android
---

# Recorrido de un TableLayout

Esta vez vamos a intentar añadir botones mediante código en tiempo de ejecución.

**Ejemplo realizado en clase**: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/RecorridoContenedor>

En el ejemplo hay implementados tres métodos:

* *mostrarTableRows()*: Accede a los *TableRow* del *TableLayout*.

{% highlight java %}
private void mostrarTableRows() {
    TableRow tableRow;
    View view;
    TableLayout tableLayout = findViewById(R.id.tableLayout);

    for (int i = 0; i < tableLayout.getChildCount(); i++) {
        //Hacemos cast porque sabemos su tipo
        tableRow = (TableRow) tableLayout.getChildAt(i);
        //también podría funcionar
        //view = tableLayout.getChildAt(i);
        //Compruebo si realmente tengo acceso
        Log.i("Prueba", tableRow.toString());
    }
}
{% endhighlight %}

* *mostrarVistas()*: Muestra las vistas que hay dentro cada *TableRow*.

{% highlight java %}
private void mostrarVistas() {
    TableRow tableRow;
    View view;
    TableLayout tableLayout = findViewById(R.id.tableLayout);

    for (int i = 0; i < tableLayout.getChildCount(); i++) {
        //Hacemos cast porque sabemos su tipo
        tableRow = (TableRow) tableLayout.getChildAt(i);
        //Recorremos los tableRow
        for (int j = 0; j < tableRow.getChildCount(); j++) {
            //Como no sabemos el tipo de vista, lo guardo en un tipo View
            view = tableRow.getChildAt(j);
            Log.i("Prueba", view.toString());
        }
    }
}
{% endhighlight %}

* *anadirBotones()*: Añade botones en tiempo de ejecución aunque, podría ser cualquier tipo de vista.

{% highlight java %}
private void anadirBotones() {
    TableRow tableRow;
    View view;
    TableLayout tableLayout = findViewById(R.id.tableLayout);

    for (int i = 0; i < tableLayout.getChildCount(); i++) {
        //Hacemos cast porque sabemos su tipo
        tableRow = (TableRow) tableLayout.getChildAt(i);
        //Creamos un botón
        Button button = new Button(this);
        button.setText("Texto");
        //Generamos Id
        button.setId(View.generateViewId());
        //Añadimos el listener a cada botón
        button.setOnClickListener(this);
        //Asignamos una etiqueta
        button.setTag("boton" + i);
        //Añadimos botón
        tableRow.addView(button);
    }
}
{% endhighlight %}

Por último, se ha añadido un nuevo *TableRow* en el *TableLayout*:

{% highlight java %}
//Para ello, creo un tableRow
TableRow tr_head = new TableRow(this);
//Y lo añado al tableLayout
tableLayout.addView(tr_head);

//Añadimos un botón a la fila creada
Button button = new Button(this);
button.setText("Texto");
button.setId(View.generateViewId());
tr_head.addView(button);
{% endhighlight %}

Con todo ello, tendremos el siguiente resultado:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_contenedores/captura1.jpg)
{: refdef}

Como se puede observar, se ha introducido un botón en cada fila. Si quisieramos más de uno en cada *TableRow*, ¿cómo podrías introducir varios botones en la misma fila?. Observa que en cada iteración del bucle se tiene acceso al *TableRow* correspondiente, pero únicamente se añade un botón...


