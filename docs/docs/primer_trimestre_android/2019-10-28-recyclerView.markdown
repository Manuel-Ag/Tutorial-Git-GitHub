---
layout: post
title:  "RecyclerView"
date:   2019-10-28 14:30:00 +0200
categories: primer_trimestre
order: 1
parent: Primer trimestre Android
---

# RecyclerView

**Pasos para implementar un *RecyclerView*:**

1.Crea tu propia clase adaptador *MyAdapter*:

{% highlight java %}
public class MyAdapter extends RecyclerView.Adapter<MyAdapter.MyViewHolder> {
...
}
{% endhighlight %}

El propio entorno te indicará que métodos y clases debes de implementar.


2.Para darle funcionalidad a los botones, define los *listener* en la subclase:

{% highlight java %}
public class MyViewHolder extends RecyclerView.ViewHolder implements View.OnClickListener {
...
}
{% endhighlight %}


3.También definimos la interface para el *callback*:

{% highlight java %}
public interface ItemClickListener {
    void onItemClick(View view, int position);
}
{% endhighlight %}


4.En la actividad principal es donde deberemos de utilizar nuestro adaptador:

{% highlight java %}
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        recyclerView = (RecyclerView) findViewById(R.id.recyclerView);

        // use this setting to improve performance if you know that changes
        // in content do not change the layout size of the RecyclerView
        recyclerView.setHasFixedSize(true);

        // use a linear layout manager
        layoutManager = new LinearLayoutManager(this);
        recyclerView.setLayoutManager(layoutManager);

        // specify an adapter (see also next example)
        mAdapter = new MyAdapter(myDataSet);
        mAdapter.setClickListener(this);
        recyclerView.setAdapter(mAdapter);
    }
{% endhighlight %}


5.Y, obviamente, implementar la interface para el *callback*:

{% highlight java %}
public class MainActivity extends AppCompatActivity implements MyAdapter.ItemClickListener {
...

    public void onItemClick(View view, int position) {
        Log.d("prueba", "You clicked " + mAdapter.getItem(position) + " on row number " + position);
    }
}
{% endhighlight %}
	
Para modificar el contenido de la lista tenemos a nuestra disposición varios métodos para notificar el cambio. En el ejemplo en GitHub se ha implementado un botón que añade un elemento a la lista:

{% highlight java %}
    public void boton(View v) {
        myDataSet.add("Añadido");
        mAdapter.notifyDataSetChanged();
    }
{% endhighlight %}

En este caso simplemente se ha añadido un elemento al final; se ha modificado *myDataSet* y se ha notificado a *mAdapter* el cambio con el método `notifyDataSetChanged()` . Existen otros métodos para notificar otros tipos de cambios como:

* `notifyItemInserted()` : INsertar un item.
* `notifyItemRangeInserted()` : Insertar varios items.
* `notifyItemRemoved()` : Eliminar un item.
* `notifyItemRangeRemoved()` : Eliminar varios items.
* `clear()` : Vaciar lista.
* `notifyDataSetChanged()` : Cambio de todos los elementos.
* `notifyItemChanged()` : Actualizar un item.
* `notifyItemMoved()` : Mover solo un item.


	
**Visita los siguientes enlaces para ver un ejemplo en funcionamiento:**

* GitHub: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/RecyclerView>
* Documentación oficial: <https://developer.android.com/guide/topics/ui/layout/recyclerview>
* Ejemplo paso a paso en StackOverflow: <https://stackoverflow.com/questions/40584424/simple-android-recyclerview-example/40584425#40584425>
* Ejemplo añadir nuevos elementos en StackOverflow: <https://stackoverflow.com/questions/31367599/how-to-update-recyclerview-adapter-data/48959184#48959184>











