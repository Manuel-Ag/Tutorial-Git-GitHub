---
layout: post
title:  "AsyncTask"
date:   2019-12-3 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

# Asynctask

En el ejemplo anterior utilizamos un hilo de ejecución independiente con la clase Thread. Android nos proporciona una formas más sencilla para trabajar con más hilos de ejecución. Es la clase `AsyncTask`. En nuestro ejemplo de uso haremos que otro hilo de ejecución cuente de 0 a 10 y lo muestre en un `editText`.

* Proyecto GitHub: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/Asynctask>

1\. Creación de la clase anidada que hereda de AsyncTask:
{% highlight java %}
    // <Parámetros, progreso y resultado>
    public class Tarea extends AsyncTask<Integer, Integer, Integer> {
        ...
    }
{% endhighlight %}

Cuando heredemos de esta clase estamos heredando el método abastracto `doInBackground()` por lo que se nos obligará de importarlo. Será en este método donde se encuentre el código que se ejecute en otro hilo de ejecución distinto al principal.

Observa que se definen tres parámetros. Estos parámetros al ser definidos cambiarán la declaración de los métodos al ser implementados automáticamente. Corresponden a:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_asynctask/captura1.png)
{: refdef}
Recuperado de: <https://stackoverflow.com/questions/6053602/what-arguments-are-passed-into-asynctaskarg1-arg2-arg3>

2\. El código que se ejecutará en otro hilo de ejecución será el de dentro del método `doInBackground()`:
{% highlight java %}
        @Override
        protected Integer doInBackground(Integer... objects) {
            for (int i = 0; i <= objects[0]; i++) {
                publishProgress(i,i*100/objects[0]);
                SystemClock.sleep(300);

                // Si cancelamos salimos del bucle
                if (isCancelled())
                    break;
            }

            return objects[0];
        }
{% endhighlight %}

Como puedes observar, simplemente es un contador de 0 al número que se haya pasado por parámetro. En cada iteración paramos el hilo un corto periodo de tiempo y se llama a `publishProgress()` . Este método nos permitirá actualizar el estado del hilo cada vez que se llame desde el hilo principal de ejecución del programa:
{% highlight java %}
        @Override
        protected void onProgressUpdate(Integer... values) {
            editText.setText(values[0].toString());
            progressBar.setProgress(values[1]);
        }
{% endhighlight %}
En nuestro ejemplo hemos utilizado un `progressBar` para mostrar el avance del hilo así como un `editText` donde poner el número actual.


Ten en cuenta que este método no se llamará si se cancela la ejecución:
{% highlight java %}
    public void cancelar(View v) {
        tarea.cancel(true);
    }
{% endhighlight %}

3\. También disponemos de métodos que se ejecutará antes y después del código definido en `doInBackGround()`, aunque estos serán ejecutados en el hilo principal del programa.
{% highlight java %}
        @Override
        protected void onPreExecute() {
            button.setText("Calculando...");
        }

        @Override
        protected void onPostExecute(Integer integer) {
            button.setText("Se ha sumado" + integer + "veces");
        }
{% endhighlight %}

4\. Con todo preparado, simplemente nos queda instanciar la clase y ejecutar:
{% highlight java %}
        tarea = new Tarea();
        tarea.execute(Integer.parseInt(editText.getText().toString()));
{% endhighlight %}

La tarea se ejecutará hasta que termine o cancele.





