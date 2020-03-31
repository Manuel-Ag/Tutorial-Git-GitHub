---
layout: post
title:  "MediaController"
date:   2020-01-13 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

# MediaController

La clase `MediaController` permite añadir unos controles básicos para administrar la reproducción. Se puede combinar con la clase `MediaPlayer` para la reproducción de audio y con la vista `VideoView` para la de vídeo.

## MediaController y MediaPlayer

[GitHub](https://github.com/Manuel-Ag/PMD_19-20/tree/master/MediaControllerMusica){: .btn .btn-blue }

1\. Instanciamos la clase `MediaController`:

```java
mediaController = new MediaController(this);
mediaController.setMediaPlayer(this);
mediaController.setAnchorView(findViewById(R.id.constLayout));
```

2\. Implementamos la interface:

```java
public class MainActivity extends AppCompatActivity implements MediaController.MediaPlayerControl{
 ...
}
```

3\. Por cada método de la interface de debe de llamar al método correspondiente de `MediaPlayer` o devolver un valor definido:

```java
public void start() {
        mediaPlayer.start();
    }

    public void pause() {
        mediaPlayer.pause();
    }

    public int getDuration() {
        return mediaPlayer.getDuration();
    }

    public int getCurrentPosition() {
        return mediaPlayer.getCurrentPosition();
    }

    public void seekTo(int i) {
        mediaPlayer.seekTo(i);
    }

    public boolean isPlaying() {
        return mediaPlayer.isPlaying();
    }

    public int getBufferPercentage() {
        return 0;
    }

    public boolean canPause() {
        return true;
    }

    public boolean canSeekBackward() {
        return true;
    }

    public boolean canSeekForward() {
        return true;
    }

    @Override
    public int getAudioSessionId() {
        return 0;
    }
```

Se puede cambiar algunos parámetros para cambiar el comportamiento en la reproducción.

4\. Mostramos el controlador:

```java
public boolean onTouchEvent(MotionEvent event) {
    mediaController.show(2000);
    return super.onTouchEvent(event);
}
```

## MediaController y VideoView

[GitHub](https://github.com/Manuel-Ag/PMD_19-20/tree/master/MediaControllerVideo){: .btn .btn-blue }

Utilizarl `MediaController` junto a `VideoView` requiere de menos pasos:

1\. Instanciamos la clase `MediaController`:

```java
        mediaController = new MediaController(this);
        mediaController.setAnchorView(videoView);
        videoView.setMediaController(mediaController);
        String uri = "https://permadi.com/thirdParty/videos/redcliff450.webm";
        videoView.setVideoURI(Uri.parse(uri));
```

2\. Implementamos la interface:

```java
public class MainActivity extends AppCompatActivity implements MediaController.MediaPlayerControl{
 ...
}
```
Si bien la interface nos obliga a declarar los métodos, no será necesario dotarlos de funcionlidad.

3\. Mostramos el controlador:

```java
public boolean onTouchEvent(MotionEvent event) {
    mediaController.show(20000000);
    return false;
}
```
