---
layout: post
title:  "Broadcast Receiver y SMS"
date:   2019-11-18 14:30:00 +0200
categories: primer_trimestre
order: 1
parent: Primer trimestre Android
---

# BroadcastReceiver y SMS

**Antes de nada, visita los siguientes enlaces:**

* Ya hablamos anteriormente un poco de los receptores de emisiones: <https://developer.android.com/guide/components/fundamentals?hl=es-419>
* Guía Broadcast Receiver: <https://developer.android.com/guide/components/broadcasts>

## Primer ejemplo: Creación de un Broadcast Receiver

Proyecto: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/Broadcastreceiver>

* El Broadcast Receiver: Será el componente que se lance al recibir el mensaje.
{% highlight java %}
public class Receptor extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context, "SMS entrante", Toast.LENGTH_LONG).show();
    }
}
{% endhighlight %}

* Declaración en fichero manifiesto o en tiempo de ejecución: Dependerá, como siempre, de la versión de Android (ver enlace sobre Broadcast Receiver).
{% highlight java %}
        Receptor receptor = new Receptor();
        IntentFilter filter = new IntentFilter();
        filter.addAction("android.provider.Telephony.SMS_RECEIVED");

        this.registerReceiver(receptor, filter);
{% endhighlight %}

{% highlight xml %}
        <receiver android:name=".Receptor">
            <intent-filter>
                <action android:name="android.provider.Telephony.SMS_RECEIVED" />
            </intent-filter>
        </receiver>
{% endhighlight %}

## Segundo ejemplo: Envío y recepción de SMS

A continuación, veremos un ejemplo más completo en el que enviaremos y recuperaremos un SMS. Proyecto: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/RecibirSMS>

El código para enviar un SMS es muy sencillo. Podemos hacerlo mediante un *intent* (no requiere permisos) o mediante SMSManager (requiere permisos). En este enlace puedes ver un ejemplo: <https://www.tutorialspoint.com/android/android_sending_sms.htm>
{% highlight java %}
        // SMS mediante la API
        SmsManager smsManager = SmsManager.getDefault();
        smsManager.sendTextMessage(editText.toString(), null, "sms message", null, null);

        // SMS mediante intent
        Uri uri = Uri.parse("smsto:"+editText.toString());
        Intent intent = new Intent(Intent.ACTION_SENDTO, uri);
        intent.putExtra("sms_body", "The SMS text");
        startActivity(intent);
{% endhighlight %}

Para leer un SMS si será necesario pedir los permisos. Se puede leer el mensaje entrante mediante el siguiente código:
{% highlight java %}
    public void onReceive(Context context, Intent intent) {

        if (intent.getAction().equals(SMS_RECEIVED)) {
            Bundle bundle = intent.getExtras();

            SmsMessage[] msgs = null;
            String origen = null;
            String msg = null;

            if (bundle != null) {
                Object[] pdu = (Object[]) bundle.get("pdus");
                msgs = new SmsMessage[pdu.length];
                for (int i = 0; i < msgs.length; i++) {
                    String format = bundle.getString("format");
                    msgs[i] = SmsMessage.createFromPdu((byte[])pdu[i], format);
                    origen = msgs[i].getOriginatingAddress();
                    msg = msgs[i].getMessageBody();
                }

                respuesta.onRecibeSMS(origen, msg);
                //Toast.makeText(context, "Mensaje", Toast.LENGTH_SHORT).show();
                Log.i("Prueba", "Broadcast funciona");
            }
        }
    }
{% endhighlight %}

En el proyecto de GitHub además hemos implementado un callback. Como recordarás, ya lo utilizamos para los diálgos. Si necesitas un repaso puedes visitar el siguiente enlace: <http://codictados.com/android-callbacks/>



