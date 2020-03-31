---
layout: post
title:  "Notificaciones"
date:   2019-12-5 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

# Notificaciones

Para este ejemplo vamos a seguir paso a paso la documentación oficial de Android respecto a las notificaciones:

* Página 1: <https://developer.android.com/guide/topics/ui/notifiers/notifications?hl=es-419>
* Página 2: <https://developer.android.com/training/notify-user/build-notification?hl=es-419>
* Página 3: <https://developer.android.com/training/notify-user/expanded?hl=es-419>

Revisa la documentación antes de continuar. En el ejemplo se ha separado cada tipo de notificación en un botón diferente.

## Creación del canal de notificaciones
{% highlight java %}
    private void createNotificationChannel() {
        // Create the NotificationChannel, but only on API 26+ because
        // the NotificationChannel class is new and not in the support library
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            CharSequence name = getString(R.string.channel_name);
            String description = getString(R.string.channel_description);
            int importance = NotificationManager.IMPORTANCE_DEFAULT;
            NotificationChannel channel = new NotificationChannel(CHANNEL_ID, name, importance);
            channel.setDescription(description);
            // Register the channel with the system; you can't change the importance
            // or other notification behaviors after this
            NotificationManager notificationManager = getSystemService(NotificationManager.class);
            notificationManager.createNotificationChannel(channel);
        }
    }
{% endhighlight %}

Este canal de notificaciones es obligatorio únicamente a partir del API 26, por lo que la primera línea que tenemos al intentar crearlo es ` if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) { ... }` . Por lo tanto si la versión es inferior no es necesario la creación de este canal.

El canal deberá de tener un `CHANNEL_ID` único, que habrá que tener en cuenta cuando creemos la notificación. Una vez configurados todos los parámetros se creará el canal con `notificationManager.createNotificationChannel(channel)`


## Notificación básica

{% highlight java %}
        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_android_black_24dp)  // el icono debe de ser en gama de blancos y negros
                .setContentTitle("Título")
                .setContentText("Contenido")
                .setPriority(NotificationCompat.PRIORITY_DEFAULT);

        // Mostramos la notificación
        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(this);
        // notificationId is a unique int for each notification that you must define
        notificationManager.notify(1, builder.build());

{% endhighlight %}

A tener en cuenta:
* Se debe haber creado anteriormente el canal, y utilizar esa ID para crear la notificación (`CHANNEL_ID`).
* Para que se muestre el icono correctamente debe de tener un canal alfa. El icono se mostrará en blanco y negro, pero podemos cambiar el color mediante:
{% highlight java %}
builder.setColor(ContextCompat.getColor(context, R.color.colorPrimary))
{% endhighlight %}
* El `requestCode` en `notify()` debe de ser único para cada notificación. En caso contrario se irán agrupando.


## Notificación con acción toque a una actividad

{% highlight java %}
        // Intent explícito hacia una actividad
        Intent intent = new Intent(this, Main2Activity.class);
        intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_CLEAR_TASK);
        PendingIntent pendingIntent = PendingIntent.getActivity(this, 0, intent, 0);

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_android_black_24dp)
                .setContentTitle("My notification")
                .setContentText("Hello World!")
                .setPriority(NotificationCompat.PRIORITY_DEFAULT)
                // Set the intent that will fire when the user taps the notification
                .setContentIntent(pendingIntent)
                .setAutoCancel(true);

        // Mostramos la notificación
        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(this);
        // notificationId is a unique int for each notification that you must define
        notificationManager.notify(2, builder.build());
{% endhighlight %}

Cambios respecto a la notificación básica:
* Utilización de PendingIntent <https://developer.android.com/reference/android/app/PendingIntent>, <https://android.jlelse.eu/intent-vs-pendingintent-8ef2ad5824ed>.


## Con botón de acción

{% highlight java %}
        Intent snoozeIntent = new Intent(this, Main2Activity.class);
        snoozeIntent.setAction("Botón");
        snoozeIntent.putExtra("extra", 0);
        PendingIntent snoozePendingIntent =
                PendingIntent.getActivity(this, 0, snoozeIntent, 0);

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_android_black_24dp)
                .setContentTitle("My notification")
                .setContentText("Hello World!")
                .setPriority(NotificationCompat.PRIORITY_DEFAULT)
                .addAction(R.drawable.ic_android_black_24dp, "Botón",
                        snoozePendingIntent)
                // podemos añadir hasta 3 botones, en este caso botón 2 utiliza el mismo pending intent,
                // por lo que tendrá la misma funcionalidad de botón 1
                .addAction(R.drawable.ic_android_black_24dp, "Botón2",
                        snoozePendingIntent);

        // Mostramos la notificación
        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(this);
        // notificationId is a unique int for each notification that you must define
        notificationManager.notify(3, builder.build());
{% endhighlight %}

Cambios respecto a la acción con toque:
* Observa la instancia de `intent` y la llamada a `.addAction()`.


## Acción con respuesta directa

En este caso debemos incluir también código en la actividad que recibe el mensaje.

1\. Creación de la notificación:
{% highlight java %}
        RemoteInput remoteInput = new RemoteInput.Builder(KEY_TEXT_REPLY)
                .setLabel("Etiqueta1")
                .build();

        // Build a PendingIntent for the reply action to trigger.
        Intent intent = new Intent(this, Main3Activity.class);
        //intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_CLEAR_TASK);
        PendingIntent pendingIntent = PendingIntent.getActivity(this, 0,
                intent, 0);

        // Create the reply action and add the remote input.
        NotificationCompat.Action action =
                new NotificationCompat.Action.Builder(R.drawable.ic_android_black_24dp,
                        "Etiqueta2", pendingIntent)
                        .addRemoteInput(remoteInput)
                        .build();

        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_android_black_24dp)
                .setContentTitle("My notification")
                .setContentText("Hello World!")
                .setPriority(NotificationCompat.PRIORITY_DEFAULT)
                .addAction(action)
                .setAutoCancel(true);


        // Issue the notification.
        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(this);
        notificationManager.notify(4, builder.build());
{% endhighlight %}

2\. Código de la actividad receptora:
{% highlight java %}
public class Main3Activity extends AppCompatActivity {

    private static final String KEY_TEXT_REPLY = "key_text_reply";
    static final String CHANNEL_ID = "ID_CANAL";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main3);

        String mensaje = getMessageText(getIntent()).toString();
        Toast.makeText(this, mensaje, Toast.LENGTH_SHORT).show();
        // Build a new notification, which informs the user that the system
        // handled their interaction with the previous notification.
        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_android_black_24dp);

        // Issue the new notification.
        NotificationManagerCompat notificationManager = NotificationManagerCompat.from(this);
        notificationManager.notify(4, builder.build());

    }

    private CharSequence getMessageText(Intent intent) {
        Bundle remoteInput = RemoteInput.getResultsFromIntent(intent);
        if (remoteInput != null) {
            return remoteInput.getCharSequence(KEY_TEXT_REPLY);
        }
        return null;
    }
}

Es en el método `getMessageText()` donde se recupera el mensaje. Además, se debe de devolver un `notify()` a la notificación con una id concreta para responder. 

{% endhighlight %}

Cambios respecto a las notificaciones anteriores:
* Utilización de la clase RemoteInput.
* `Notification.Action.Builder().addRemoteInput().build()`
* Debemos de recibir el mensaje y responder.



## Barra de progreso

Es una notificación más simple que las anteriores. La dividiremos en varias partes.

1\. Creación:
{% highlight java %}
public void notifiacionBarra(View v) {
    notificationManagerProgreso = NotificationManagerCompat.from(this);
    builderProgreso = new NotificationCompat.Builder(this, CHANNEL_ID);
    builderProgreso.setContentTitle("Picture Download")
            .setContentText("Download in progress")
            .setSmallIcon(R.drawable.ic_android_black_24dp)
            .setPriority(NotificationCompat.PRIORITY_LOW);

    // Issue the initial notification with zero progress
    int PROGRESS_MAX = 100;
    int PROGRESS_CURRENT = 0;
    builderProgreso.setProgress(PROGRESS_MAX, PROGRESS_CURRENT, false);
    notificationManagerProgreso.notify(5, builderProgreso.build());
}
{% endhighlight %}

2\. Aumentar la barra de progreso:
{% highlight java %}
public void notificacionUp(View v) {
    // Si estamos por debajo del máximo
    if (PROGRESS_CURRENT < PROGRESS_MAX) {
        builderProgreso.setProgress(PROGRESS_MAX, PROGRESS_CURRENT += 10, false);
        notificationManagerProgreso.notify(5, builderProgreso.build());
    }
    // Si llegamos al máximo
    else {
        builderProgreso.setContentText("Download complete")
                .setProgress(0, 0, false);
        notificationManagerProgreso.notify(5, builderProgreso.build());
    }
}
{% endhighlight %}

3\. Disminuir la barra de progreso:
{% highlight java %}
public void notificacionDown(View v) {
    builderProgreso.setProgress(PROGRESS_MAX, PROGRESS_CURRENT-=10, false);
    notificationManagerProgreso.notify(5, builderProgreso.build());
}
{% endhighlight %}


* **Proyecto GitHub:** <https://github.com/Manuel-Ag/PMD_19-20/tree/master/Notificaciones>
