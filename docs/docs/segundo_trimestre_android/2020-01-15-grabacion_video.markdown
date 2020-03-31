---
layout: post
title:  "Grabación de vídeo"
date:   2020-01-15 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

[GitHub](https://github.com/Manuel-Ag/PMD_19-20/tree/master/GrabacionVideo){: .btn .btn-blue }

# Grabación de vídeo

En el siguiente ejemplo se realizará una grabación de vídeo con el dispositivo para, a continuación, reproducirla en un `videoView`.

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_grabacion/gif1.gif)
{:refdef}

Pasos:

1\. Botón y `videoView`.

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_grabacion/captura.jpg)
{:refdef}

2\. Intent implícito para grabar.

```java
public void grabar(View v) {
    Intent intent = new Intent(MediaStore.ACTION_VIDEO_CAPTURE);
    intent.putExtra(MediaStore.EXTRA_DURATION_LIMIT, 5); // límite en segundos
    intent.putExtra(MediaStore.EXTRA_VIDEO_QUALITY, 0); // 0 baja calidad, 1 alta
    startActivityForResult(intent, GRABAR);
}
```
Con `putExtra()` se pueden definir algunos parámetros en la grabación. Consulta la [Documentación](https://developer.android.com/reference/android/provider/MediaStore){: .btn .btn-green }

3\. Recupera la `Uri`.

```java
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    if (requestCode == GRABAR) {
        if (resultCode == RESULT_OK) {
            VideoView videoView = findViewById(R.id.videoView);
            videoView.setVideoURI(data.getData());
            videoView.start();
        }
    }
}
```
Para empezar a reproducir simplemente basta con llamar al método `start()`, pero recuerda que tenemos otros muchos método para administrar un `videoView` definidos en la [Documentación](https://developer.android.com/reference/android/widget/VideoView){: .btn .btn-green }
