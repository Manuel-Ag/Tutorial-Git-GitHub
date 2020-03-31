---
layout: post
title:  "Preferencias"
date:   2019-12-20 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

# Preferencias

Las preferencias nos permiten almacenar valores para almacenar varios tipos de datos, como por ejemplo la configuración del usuario, opciones de visionado, etc. Los valores se almacenan en un fichero con el formato clave-valor. Veremos dos formas de almacenar estas preferencias en el dispositivo.

### Utilizando la clase `SharedPreferences`

Permite guardar preferencias en el fichero sin necesidad de utilizar ninguna vista, aunque si lo deseásemos obviamente podrían utilizarse.

1\. Instancia la clase:

```java
SharedPreferences misPreferencias = getSharedPreferences("prefs", MODE_PRIVATE);
```
Se crea en modo privado, por lo que el fichero será accesible únicamente por nuestra aplicación. Si existe el fichero `prefs` se prepara la clase para leerlo, en caso contrario se creará.

2\. Guarda las preferencias deseadas:

```java
SharedPreferences.Editor editor = misPreferencias.edit();
editor.putString("nombre", "Paco");
editor.putInt("edad", 40);
editor.putBoolean("soltero", true);
editor.apply();
```

Se guardarán de la forma clave-valor. Puedes comprobar que hay muchos métodos dependiendo del tipo de dato que se desea guardar, aunque la clave será siempre `String`. Al final se aplicarán los cambios con el método `apply()`.

3\. Recupera los datos:

```java
String nombre = misPreferencias.getString("nombre", "Sin dato");
int edad = misPreferencias.getInt("edad", 0);
boolean soltero = misPreferencias.getBoolean("soltero", true);
```

Observa como dependiendo del tipo de dato a recuperar se utiliza un método u otro.

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/assets_post_preferencias/sharedpref.gif)
{:refdef}


### Utilizando la clase `PreferenceActivity`

El nombre de la clase ya indica que en realidad se va a trabajar con una clase que hereda de `Activity`. Esta clase nos permitirá crear un menú para el usuario que guarde automáticamente las preferencias en el fichero.

1\. Crea un fichero `preferencias.xml` en el directorio `xml` de `resources`:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/assets_post_preferencias/ficheropref.gif)
{:refdef}

2\. Añade los controles que desees que tenga esa ventana a través del diseñador:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/assets_post_preferencias/Captura1.jpg)
{:refdef}

3\. Crea la actividad:

```java
public class PreferenciasActivity extends PreferenceActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        getFragmentManager().beginTransaction().replace(android.R.id.content,
                new Fragmento()).commit();
    }

    public static class Fragmento extends PreferenceFragment {

        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            addPreferencesFromResource(R.xml.preferencias);
        }
    }
}
```

Lo que estamos haciendo en realidad es cambiar la vista actual a la definida en `preferencas`.

4\. Llama a esa actividad mediante un intent:

```java
public void clasePreferenceActivity(View v) {
    startActivity(new Intent(MainActivity.this, PreferenciasActivity.class));
}
```

Cuando se llame a la actividad el usuario podrá cambiar los valores cambiando el estado de los controles.

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/assets_post_preferencias/Captura2.jpg)
{:refdef}

5\. Recuperar la información:

Para recuperar los valores almacenados debemos de fijarnos en el atributo `key` de los elementos que hay en las propiedades.

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/assets_post_preferencias/Captura3.jpg)
{:refdef}

 Utilizaremos `key` para recuperar el valor:

```java
@Override
protected void onResume() {
    SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
    String campo1 = sharedPreferences.getString("edit_text_preference_1","Sin dato");
    boolean campo2 = sharedPreferences.getBoolean("check_box_preference_1", false);
    String campo3 = sharedPreferences.getString("list_preference_1", "Sin selección");
    Set<String> entries = sharedPreferences.getStringSet("multi_select_list_preference_1", new HashSet<String>());

    Toast.makeText(this, campo1 + " "+ campo2 + " " + campo3 + " " + entries.toString(), Toast.LENGTH_SHORT).show();

    super.onResume();
}
```

Observa como es la clase `SharedPreferences` la que nos permite acceder al fichero.

### ¿Puedo ver todos esos ficheros creados desde Android Studio?

Despliega el menú de la derecha llamado `Device File Explorer` y accede a la ruta `data/data/`, a continuación busca tu proyecto.

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/assets_post_preferencias/Captura4.jpg)
{:refdef}

* Proyecto GitHub: <https://github.com/Manuel-Ag/PMD_19-20/tree/master/Preferencias>
* Documentación oficial: <https://developer.android.com/guide/topics/ui/settings?hl=es-419>
