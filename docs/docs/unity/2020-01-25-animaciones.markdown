---
layout: post
title:  "Animaciones 2D"
date:   2020-01-24 11:30:00 +0200
categories: unity
order: 1
parent: Unity
---

# Animaciones

Unity incorpora una herramienta para añadir animaciones 2D a un GameObject. Para abrir el editor de animaciones selecciona el GameObject en la jerarquía y a continuación *Window > Animation > Animation* o la tecla rápida *Crtl + 6*.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_animaciones/captura1.png)
{:refdef}

Al seleccionar `Create` se puede crear una animación. Puedes arrastrar Sprites a este menú o pulsar el botón grabar para que se queden guardados los cambios que realices en la escena. No olvides dejar de grabar para que esos cambios en la escena no se añadan a la animación.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_animaciones/captura2.png)
{:refdef}

Para añadir más animaciones simplemente despliega el menú superior izquierdo de animaciones y selecciona `Create New Clip`.

Observa como también se ha añadido un componente `Animator` al GameObject del que hemos creado la animación. Se puede acceder al diagrama de estados de las animaciones mediante doble click en el animator o mediante *Window > Animation > Animator*.

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_animaciones/captura3.png)
{:refdef}

En esta ventana podemos añadir las diferentes animaciones creadas con anterioridad y definir la condición cuando cambia de uno a otro estado. Las flechas indican la dirección. En el inspector podemos definir la condición para que pase de un estado a otro.

Primeramente debemos definir los parámetros con que utilizaremos para pasar de un estado a otro:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_animaciones/captura4.png)
{:refdef}

Y a continuación, en la propia transición (flecha entre estados), podemos definir que condición se debe cumplir para cambiar a la animación a la que apunta:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_animaciones/captura5.png)
{:refdef}

Estos parámetros serán modificados desde un script, normalmente en el propio GameObject, por ejemplo de personaje.

Declaro la variable:
```csharp
private Animator anim;
```

Acceso al componente:
```csharp
void Start()
{
  ...
  anim = GetComponent<Animator>();
  ...
}
```

Y cambios los parámetros del `Animator` a través de `anim`. Por ejemplo para el *Trigger*:
```csharp
public void Update()
{
  ...
  anim.SetTrigger("Salto");
  ...
}
```

Cada tipo de paŕametro tiene su método correspondiente: [Animation Parameters](https://docs.unity3d.com/Manual/AnimationParameters.html){: .btn .btn-green }

<iframe width="560" height="315" src="https://www.youtube.com/embed/hkaysu1Z-N8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
