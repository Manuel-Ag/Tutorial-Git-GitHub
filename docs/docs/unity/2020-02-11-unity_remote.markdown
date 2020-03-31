---
layout: post
title:  "Unity Remote"
date:   2020-02-11 14:30:00 +0200
categories: unity
order: 1
parent: Unity
---

[Coroutines](https://docs.unity3d.com/Manual/UnityRemote5.html){: .btn .btn-green } [Script](https://github.com/Manuel-Ag/PMD_19-20/tree/master/Unity){: .btn .btn-blue }

# Unity Remote

Unity Remote nos facilita el desarrollo para diferentes dispositivos, tales como Android, iOS o tvOS. Entre otras cosas, nos permite interaccionar con eventos de entrada o sensores de nuestro dispositivo y detectarlos en la aplicación siendo ejecutada en Unity.

## Instalación

1\. Instala en tu dispositivo móvil (el físico) la siguiente app: <https://play.google.com/store/apps/details?id=com.unity3d.genericremote&hl=es_419>

2\. Comprueba que tu proyecto en Unity es un proyecto para Android: *File > Build Settings*

3\. Comprueba que está seleccionada la opción `Any Android Device` en *Edit > Project Settings > Editor*:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_unity_remote/captura1.png)
{:refdef}

4\. Activa el modo depuración de tu Android en las opciones de desarrollador. Mantén la aplicación descargada abierta.

5\. **Reinicia Unity**. A veces cuesta un poco que detecte el dispositivo, en ese caso reiniciando Unity se suele solucionar.

6\. Ejecuta el juego desde Unity.

## Input del dispositivo

Ahora que estamos ejecutando el juego en un dispositivo real, podemos realizar algunos eventos de toque de forma más sencilla (multi-touch). Veamos algunos ejemplos:

Visualiza todos los toques en pantalla y su posición:

```csharp
private void VisualizarToques()
{
    // Cantidad de dedos en pantalla
    Debug.Log(Input.touchCount);

    // Imprimir al posición de cada toque
    foreach (Touch touch in Input.touches)
    {
        Debug.Log(touch.position);
    }
}
```

Muestra si se ha realizado la acción de toque o dejar de toque:

```csharp
private void VisualizarAccionToques()
{
    // Si hay algún toque en pantalla
    if (Input.touchCount > 0)
    {
        // Primer toque
        Touch touch = Input.GetTouch(0);
        if (touch.phase == TouchPhase.Began)
            Debug.Log("Toque en " + touch.position);
        else if (touch.phase == TouchPhase.Ended)
            Debug.Log("Se levantó el dedo en " + touch.position);
    }
}
```

Combinación de los ejemplos anteriores, muestra el touch de cada dedo:

```csharp
private void VisualizarTodosAccionToques()
{
    for (int i = 0; i < Input.touchCount; i++)
    {
        Touch touch = Input.GetTouch(i);
        if (touch.phase == TouchPhase.Began)
            Debug.Log("Toque en " + touch.position + "dedo " + i);
        else if (touch.phase == TouchPhase.Ended)
            Debug.Log("Se levantó el dedo en " + touch.position + "dedo " + i);
    }
}
```

Visualización respecto a la cámara:
```csharp
// Visualiza donde ha realizado la acción toque respecto a la pantalla
private void VisualizarToquePantalla()
{
    // Click izquierdo del ratón, equivale a touch
    if (Input.GetMouseButton(0))
    {
        // Posición respecto a la cámara
        Debug.Log("ScreenToWorldPoint" + Camera.main.ScreenToWorldPoint(Input.mousePosition));
        // Valores entre 0 y 1 de los tres ejes
        Debug.Log("ScreenToViewPoint" + Camera.main.ScreenToViewportPoint(Input.mousePosition));
    }
}
```

Accelerómetro:

```csharp
private void VisualizarAccelerometro()
{
    Debug.Log("Acelerómetro: " + Input.acceleration);
}
```
