---
layout: post
title:  "Reescalando imagenes"
date:   2020-01-14 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

[GitHub](https://github.com/Manuel-Ag/PMD_19-20/tree/master/ReescaladoImagenes){: .btn .btn-blue }

# Reescalado imagen

Cuando se cargan recursos de imágenes en una aplicación se debe tener en cuenta que no siempre es necesario cargar la imagen en su tamaño original. Las pantallas suelen ser relativamente pequeñas para, por ejemplo, una imagen hecha con una buena cámara, por lo que reducir la imagen al mostrarla en nuestra aplicación mejorará la gestión de recursos del dispositivo. Primeramente, consulta la documentación de Android donde se explica paso a paso el proceso:

{:refdef: style="text-align: center;"}
[Documentación](https://developer.android.com/topic/performance/graphics/load-bitmap){: .btn .btn-green }
{:refdef}

En el ejemplo reproduciremos los mismos pasos:

1\. Seleccionamos una imagen del dispositivo utilizando un `intent` implícito.
```java
public void reducirFoto(View v) {
    Intent intent = new Intent(Intent.ACTION_PICK, MediaStore.Images.Media.EXTERNAL_CONTENT_URI);
    startActivityForResult(intent, REDUCIR);
}
```

2\. Definimos un método para redimensionar la imagen.
```java
public Bitmap reducir(String uri, int ancho, int alto) throws FileNotFoundException {
    BitmapFactory.Options options = new BitmapFactory.Options();
    // Evita cargar toda la fotografía en memoria
    options.inJustDecodeBounds = true;
    // Solo cargamos el tamaño y lo guardamos en options
    BitmapFactory.decodeStream(getContentResolver().openInputStream(Uri.parse(uri)), null, options);
    // Definimos un nuevo tamaño. BitmapFactory solo reduce las imágenes en potencia de 2, por lo que puede variar el resultado
    options.inSampleSize = (int) Math.max(Math.ceil(options.outWidth/ancho), Math.ceil(options.outHeight/alto));
    // Activamos la carga de imagen en memoria
    options.inJustDecodeBounds = false;
    // Cargamos la imagen en memoria.
    return BitmapFactory.decodeStream(getContentResolver().openInputStream(Uri.parse(uri)), null, options);
}
```
Los parámetros `ancho` y `alto` especifican el tamaño máximo de la imagen reducida. `inJustDecodeBounds` permite cargar los atributos de la imagen sin necesidad de cargarla en memoria. Una vez recuperadas las opciones se modificarán para cambiar el tamaño de la imagen a cargar. Al llamar a `decodeStream()`, se debe volver a cambiar otra vez el parámetro `inJustDecodeBounds` para recuperar realmente la imagen con las opciones especificadas.
