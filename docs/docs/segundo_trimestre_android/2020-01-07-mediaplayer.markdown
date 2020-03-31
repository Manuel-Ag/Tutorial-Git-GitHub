---
layout: post
title:  "MediaPlayer"
date:   2020-01-07 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

[GitHub](https://github.com/Manuel-Ag/PMD_19-20/tree/master/MediaPlayer){: .btn .btn-blue }

# MediaPlayer

Utilizaremos la clase `MediaPlayer` para reproducir una canción, tanto desde los recursos de la aplicación como recursos alojados en un servidor externo. Primeramente, es importante leer la documentación oficial:

{:refdef: style="text-align: center;"}
[Documentación](https://developer.android.com/reference/android/media/MediaPlayer){: .btn .btn-green }
{:refdef}

`MediaPlayer` se basa en estados para gestionar la reproducción. Es importante tener claro el diagrama de estados de esta clase:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_mediaplayer/captura1.gif)
{:refdef}

A la hora de utilizar esta clase es recomendable tener el diagrama presente. Los círculos azules representan el estado actual de la reproducción mientras que las fechas y métodos cómo se puede cambiar de un estado a otro. No se puede pasar libremente de un estado a otro, hay que respetar el flujo de estados marcado por el diagrama. El siguiente código corresponde a un reproductor de música básico.

### 1\. Instancia de la clase

```java
MediaPlayer mediaplayer =  MediaPlayer.create(this, R.raw.ac);
```
Al instanciar con este constructor nos ponemos directamente en el estado `prepared`.

### 2\. Play

```java
public void play(View v) {
    if (mediaPlayer.isPlaying())
        textViewTexto.setText("Ya se está reproduciendo");
    else {
        mediaPlayer.start();
        textViewTexto.setText("Empezando a reproducir...");
    }
}
```

Al estar ya en el estado `prepared` simplemente hay que llamar al método `start()` para comenzar a reproducir. Comprobamos que no llamamos otra vez a `start()` si se está reproduciendo actualmente.

### 2\. Pause

```java
public void pause(View v) {
    if (mediaPlayer.isPlaying()) {
        mediaPlayer.pause();
        textViewTexto.setText("Pausado");
    }
    else
        textViewTexto.setText("No estaba reproduciéndose");
}
```
Para pausar tenemos que comprobar que se está reproduciendo.

### 3\. Stop

```java
public void stop(View v) throws IOException {
    if (mediaPlayer.isPlaying() || mediaPlayer.getCurrentPosition() > 1) {
        textViewTexto.setText("Acabamos de parar");
        mediaPlayer.stop();
        mediaPlayer.prepare();
    }
    else {
        textViewTexto.setText("No estaba sonando la música");
    }
}
```
Podremos parar desde el estado `paused` y `started`. Para saber si estamos `paused` comprobamos que la posición de la canción no es 0 y que además no se está reproduciendo.

### 4\. Cambiar canción

```java
public void cambiarCancion(View v) throws IOException {
    String path = "android.resource://" + getPackageName() + "/" + R.raw.classic;
    Uri uri = Uri.parse(path);

    mediaPlayer.reset();
    mediaPlayer.setDataSource(this, uri);
    mediaPlayer.prepare();
    mediaPlayer.start();
}
```

Hay que obtener la ruta al recurso local y convertirla a tipo `Uri`. Se llamará al método `reset()` lo que nos pondrá al principio del diagrama de estados. `setDataSource()` permite cambiar la fuente de reproducción.

Otra forma posible sería llamar a `release()` y crear otra vez una instancia de la clase `MediaPlayer` como hicimos al principio.

Por último, `prepare()` y `start()` si queremos empezar a reproducir.

### 5\. Streaming

```java
public void cambiarStreaming(View v) throws IOException {
    String path = "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-9.mp3";

    mediaPlayer.reset();
    mediaPlayer.setDataSource(path);

    Toast.makeText(this, "Ruta: " + path, Toast.LENGTH_SHORT).show();

    // Prepare asíncrono
    mediaPlayer.prepareAsync();

    // Listener cuando la carga esté completa
    mediaPlayer.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
        @Override
        public void onPrepared(MediaPlayer mp) {
            mediaPlayer.start();
            // Desactivamos el listener ya que se llama varias veces a prepare() a lo largo del código
            mediaPlayer.setOnPreparedListener(null);
        }
    });
}
```

En esta ocasión el recurso no está en local. Necesitamos una URL válida que permita acceder al fichero. Al llamar a `setDataSource()` podemos pasar una URL de tipo `String`.

Se llama a `prepareAsync()` para cargar el recurso asíncronamente, ya que es posible que se este recurso tarde más en cargar. Con `setOnPreparedListener()` configuramos un listener que esperará a que el estado cambie a `prepared`. Cuando se llegue a este estado empezaremos a reproducir. También desactivaremos el listener ya que no queremos que siempre que se vaya al estado `prepared` empiece a reproducirse la canción.

### 6\.

```java
public void seekTo(View v) {
    EditText editText = findViewById(R.id.editText);

    // Tiempo especificado en milisegundos
    mediaPlayer.seekTo(Integer.parseInt(editText.getText().toString()));
    // Varios métodos sobre MediaPlayer
    Toast.makeText(this, " " + mediaPlayer.getDuration() + " " + mediaPlayer.getCurrentPosition() + " " + mediaPlayer.isLooping(), Toast.LENGTH_SHORT).show();
}
```

`MediaPlayer` nos da muchas posibilidades de gestión a través de sus métodos. Podemos ira un punto de la reproducción, saber el tiempo de reproducción actual, si estamos en loop, el punto actual de reproducción, etc.
