---
layout: post
title:  "Content providers y acceso a los contactos"
date:   2019-11-19 14:30:00 +0200
categories: primer_trimestre
order: 1
parent: Primer trimestre Android
---

# Content providers y acceso a los contactos

**Guía sobre content providers:**

* <https://developer.android.com/guide/topics/providers/content-providers?hl=es-419>
* <https://developer.android.com/guide/topics/providers/content-provider-basics?hl=es-419>

**GitHub:**

* Proyecto GitHub: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/Consultar_contactos>

Una vez estudiada la teoría tendremos una mejor comprensión de en qué consisten los content providers. Veamos un ejemplo en el que mostraremos los contactos de la agenda: 

{% highlight java %}
    public void listarContactos(View v) {
        // Columnas a recuperar
        String proyeccion[] = {ContactsContract.Contacts._ID, ContactsContract.Contacts.DISPLAY_NAME,
                ContactsContract.Contacts.HAS_PHONE_NUMBER, ContactsContract.Contacts.PHOTO_ID};

        // Filtros de la búsqeda
        String filtro = ContactsContract.Contacts.DISPLAY_NAME + " like ?";
        // Nombres que contenga la 'a'
        String arg_filtro[] = {"%a%"};

        //Consulta de los contactos
        ContentResolver contentResolver = getContentResolver();
        Cursor cur = contentResolver.query(ContactsContract.Contacts.CONTENT_URI, proyeccion, filtro, arg_filtro, null);

        // Al recorrer el cursor, recuperamos el resultado de la consulta
        if (cur.getCount() > 0) {
            while (cur.moveToNext()) {
                // Recuperamos las 3 columnas, ID, DISPLAY_NAME y HAS_PHONE_NUMBER
                String id = cur.getString(cur.getColumnIndex(ContactsContract.Contacts._ID));
                String name = cur.getString(cur.getColumnIndex(ContactsContract.Contacts.DISPLAY_NAME));
                Log.i("Contactos", "ID: " + id + " nombre: " + name);
                // Si el contacto tiene algún número de teléfono, los mostramos todos
                if (Integer.parseInt(cur.getString(cur.getColumnIndex(ContactsContract.Contacts.HAS_PHONE_NUMBER))) > 0) {
                    // Realizamos otra consulta cambiado el filtro, cuando el ID del contacto es igual al ID de la tabla donde se encuentran los números de teléfono
                    Cursor phones = contentResolver.query( ContactsContract.CommonDataKinds.Phone.CONTENT_URI, null,
                            ContactsContract.CommonDataKinds.Phone.CONTACT_ID +" = "+ id, null, null);
                    // Volvemos a recorrer un cursos
                    while (phones.moveToNext())
                    {
                        String telefono = phones.getString(phones.getColumnIndex(ContactsContract.CommonDataKinds.Phone.NUMBER));
                        Log.i("Contactos" , telefono);
                    }
                }
            }
        }
    }
{% endhighlight %}

## El ejemplo se divide dos pasos:

1\. Consulta de todos los contactos de teléfono según un filtro, en este caso contactos que contenga la letra 'a'. Se consulta la id, el nombre y si tiene o no algún teléfono.
{% highlight java %}
 // Columnas a recuperar
        String proyeccion[] = {ContactsContract.Contacts._ID, ContactsContract.Contacts.DISPLAY_NAME,
                ContactsContract.Contacts.HAS_PHONE_NUMBER, ContactsContract.Contacts.PHOTO_ID};

        // Filtros de la búsqeda
        String filtro = ContactsContract.Contacts.DISPLAY_NAME + " like ?";
        // Nombres que contenga la 'a'
        String arg_filtro[] = {"%a%"};

        //Consulta de los contactos
        ContentResolver contentResolver = getContentResolver();
        Cursor cur = contentResolver.query(ContactsContract.Contacts.CONTENT_URI, proyeccion, filtro, arg_filtro, null);
{% endhighlight %}

Siempre se pueden poner a `null` los parámetros de los filtros para recuperar todos los contactos.

2\. Para los contactos que tienen teléfono, realizamos otra consulta en la tabla donde se almacenan esos datos.
{% highlight java %}
ContactsContract.CommonDataKinds.Phone.CONTENT_URI, null,
       ContactsContract.CommonDataKinds.Phone.CONTACT_ID +" = "+ id, null, null);
{% endhighlight %}

Observa como comparamos la `id` de la primera consulta para recuperar ese contacto específicamente en la consulta de teléfonos.

