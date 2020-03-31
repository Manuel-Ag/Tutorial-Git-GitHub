---
layout: post
title:  "Audio Source"
date:   2020-02-02 14:30:00 +0200
categories: unity
order: 1
parent: Unity
---

[AudioSource](https://docs.unity3d.com/es/530/Manual/class-AudioSource.html){: .btn .btn-green } [AudioListener](https://docs.unity3d.com/Manual/class-AudioListener.html){: .btn .btn-green }

# Audio Source

El componente audio source nos permite reproducir ficheros de audio.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_audio/captura1.png)
{:refdef}

Se pueden configurar multitud de párametros, como *loop*, *pitch*, *volume*, etc. Arrastra el recurso al campo `AudioClip` y la reproducción comenzará automáticamente con los parámetros definidos. También se puede gestionar la reproducción mediante un script:

```csharp
public class AudioManager : MonoBehaviour
{
    // Recursos de audio
    public AudioClip[] audioClips;

    // Componente AudioSource
    private AudioSource audioSource;

    void Start()
    {
        // Selección de audio y reproducción
        audioSource = GetComponent<AudioSource>();
        audioSource.clip = audioClips[0];
        audioSource.Play();
    }

    // Update is called once per frame
    void Update()
    {
        Debug.Log(audioSource.isPlaying);
    }
}
```

En el ejemplo anterior nada más crear el componente se empezará a reproducir la música. Podríamos gestionar la reproducción de audio a través de los métodos que nos proporiona `AudioSource`. En este ejemplo simplemente comprobamos si se está reproduciendo la canción.

Con esta configuración se podrá reproducir cualquier clip de audio como música o efectos de sonido. El componente que hace las veces de micrófono es el `AudioListener` que normalmente se encuentra por defecto en la cámara, aunque es posible cambiarlo de posición según las necesidades. Hay únicamente un `AudioListener` por escena, por lo que habrá que desactivar el antiguo si se desea añadir otro.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_audio/captura2.png)
{:refdef}

<iframe width="560" height="315" src="https://www.youtube.com/embed/1BMJFgK68IU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
