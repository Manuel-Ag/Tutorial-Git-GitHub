---
layout: post
title:  "Ejemplo sencillo de Fragment"
date:   2019-10-18 14:30:00 +0200
categories: primer_trimestre
order: 1
parent: Primer trimestre Android
---

# Ejemplo sencillo de Fragment

En este ejemplo vamos a cambiar dónde creamos la interfaz de usuario, pasando de la Actividad principal a un Fragmento.

* **Enlace al proyecto:** <https://github.com/Manuel-Ag/PMD_19-20/tree/master/EjemplosencilloFragment>
* **Enlace a la documentación:** <https://developer.android.com/guide/components/fragments?hl=es-419>

El código para crear un Fragmento es sencillo, únicamente debemos hacer que una clase herede de *Fragment*:

{% highlight java %}
public class Fragmento1 extends Fragment {
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragmento1, container, false);
    }
}
{% endhighlight %}

Como se puede apreciar, se ha creado un fichero *fragmento1.xml*, pasándose como parámetro al método *inflate()* de la clase *LayoutInflater*. Será en este fichero donde se añadan las vistas.

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_fragment/captura1.jpg)
{: refdef}

Observa cómo en nuestro ejemplo en realidad hay 3 ficheros con el mismo nombre. En este caso se ha aplicado lo aprendido en el ejemplo de aplicación multi-lenguaje; simplemente se ha cambiado los criterios para la utilización de un fichero u otro, cambiando el idioma por la orientación del teléfono (*portrait* o *landscape*).

Por último, simplemente añade un contenedor de tipo *fragment* al fichero .xml correspondiente al *layout* principal. Esto hará que este fragmento se cargue dentro de este *layout* (puedes observarlo tanto en el diseñador como en el pripio fichero .xml).

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_fragment/captura2.jpg)
{: refdef}





