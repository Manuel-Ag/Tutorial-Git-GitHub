---
layout: post
title:  "Escenario 2D"
date:   2020-01-18 14:30:00 +0200
categories: unity
order: 1
parent: Unity
---

# Scenario 2d Unity

Para construir un escenario simple necesitamos dos elementos, los sprites para dibujar y un Tilemap.

## Tilemap

Este objeto nos sirve para separar el escenario en cuadrículas en la que pintar. Podemos tener todos los que deseemos:

<iframe width="560" height="315" src="https://www.youtube.com/embed/fmNtibNWPhc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[Documentación](https://docs.unity3d.com/Manual/class-Tilemap.html){: .btn .btn-green }

## Sprites y Palette

Para pintar en el Tilemap se utiliza el componente Palette. Los recursos importados de la Unity Store vienen preparados para ser utilizados. Sin embargo, para los recursos importados de fuentes externas debemos de crear nuestra propia Palette. Guía de uso:

<iframe width="560" height="315" src="https://www.youtube.com/embed/JESTeoD7-DE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[Documentación](https://docs.unity3d.com/Manual/Tilemap-Palette.html){: .btn .btn-green }

Para utilizar los sprites de Sunny-land simplemente debemos crear una nueva Palette y arrastrar los elementos a esta paleta. No olvides comprobar que el tamaño de las imágenes concuerdan con el tamaño de las unidades de unity. Se debe indicar el número de pixeles por unidad en los parámetros de la imagen:

{:refdef: style="text-align: center;"}
![Imagen]({{ site.baseurl }}/assets/img_post_u_introduccion/captura3.PNG)
{:refdef}

En este caso se indica que en cada imagen corresponden 16 píxeles por unidad.
