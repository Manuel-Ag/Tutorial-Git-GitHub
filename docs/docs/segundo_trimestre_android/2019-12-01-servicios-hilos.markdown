---
layout: post
title:  "Servicios e hilos"
date:   2019-12-1 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

# Servicios e hilos

En este ejemplo vamos a utilizar un sevicio que compruebe si la wifi está conectada no.

* Proyecto: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/Servicios>

Antes de continuar visita <https://developer.android.com/guide/components/services?hl=es-419> y revisa el contenido respecto a los tipos de servicios, ciclo de vida, métodos importantes, etc.

Para crear el programa se han seguido los siguientes pasos:

1\. Creación de una interface gráfica con dos botones que lancen y paren el servicio.

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_servicios/captura1.png)
{: refdef}

{% highlight java %}
    public void arrancar(View v) {
        Intent intent = new Intent(this, WifiTest.class);
        startService(intent);
    }

    public void parar(View v) {
        Intent intent = new Intent(this, WifiTest.class);
        stopService(intent);
    }
{% endhighlight %}

Para crear y parar el servicio creamos un `Intent` y llamamos a `startService()` o `stopService()` respectivamente.

2\. La clase `WifiTest` es el servicio, por lo que hereda de `Service` 

{% highlight java %}
public class WifiTest extends Service { ... }
{% endhighlight %}

No olvides declarar el componente en el fichero `Manifest`

{% highlight xml %}
<service android:name=".WifiTest"</service>
{% endhighlight %}

3\. Gestión del servicio:

{% highlight java %}
public class WifiTest extends Service {
    private boolean enEjecucion = false;
    Tester tester;
    @Override
    public void onCreate() {
        Log.i("prueba", "onCreate");
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {

        if (!enEjecucion) {
            tester = new Tester();
            tester.start();
            enEjecucion = true;
            Log.i("prueba", "arrancando");
        }else {
            Log.i("prueba", "el sevicio ya estaba arrancado");
        }

        return START_STICKY;
    }

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public void onDestroy() {
        if(enEjecucion)
            tester.interrupt();

        Log.i("prueba", "servicio destruido");
    }

{% endhighlight %}


* `onBind()` devuelve nulo ya que es un servicio no enlazado.
* `onStartCommand()` será el método que se ejecute al lanzar el servicio.
* Con la variable `enEjecucion` controlamos si el servicio ya ha sido lanzado con anterioridad.
* La clase `Tester` es un hilo que se lanzará a la vez del servicio. 

4\. La clase `Tester` es la que incorpora la funcionalidad propia del servicio. 

{% highlight java %}
        public boolean comprobarWifi() {
            ConnectivityManager connectivityManager = (ConnectivityManager) getApplicationContext()
                    .getSystemService(Context.CONNECTIVITY_SERVICE);

            NetworkInfo networkInfo = connectivityManager
                    .getNetworkInfo(ConnectivityManager.TYPE_WIFI);
            if (networkInfo.isConnected())
                return true;

            return false;
        }
{% endhighlight %}

Desde el servicio se instanciará la clase y se ejecutará el hilo. Al parar el servicio también se parará el hilo.
{% highlight java %}
    @Override
    public void onDestroy() {
        if(enEjecucion)
            tester.interrupt();

        Log.i("prueba", "servicio destruido");
    }
{% endhighlight %}



