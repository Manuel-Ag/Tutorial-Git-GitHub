---
layout: post
title:  "Firebase Firestore"
date:   2020-01-21 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

[GitHub](https://github.com/Manuel-Ag/PMD_19-20/tree/master/firebase){: .btn .btn-blue } [Documentación](https://firebase.google.com/docs/firestore/?hl=ES){: .btn .btn-green }

# Firebase Firestore

<iframe width="560" height="315" src="https://www.youtube.com/embed/QcsAb2RR52c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Firebase nos permite utilizar dos bases de datos NoSQL, `RealTime Database` y `Firestore`. Utilizaremos esta última por se más actual, aunque el funcionamiento de ambas es muy parecido.

El primer paso es configurar en entorno. Tenemos los pasos explicados en la documentación:

[Primeros pasos](https://firebase.google.com/docs/firestore/quickstart?hl=ES){: .btn .btn-green }

No olvides añadir al fichero gradle:` implementation 'com.google.firebase:firebase-firestore:21.2.1' ` ni configurar las reglas para que únicamente puedan acceder los usuarios autenticados.

A continuación, crea la base de datos desde el panel de control de Firebase. Selecciona la base de datos correcta:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_firestore/captura1.png)
{:refdef}

Ya está el entorno preparado para utilizar la base de datos. Desde el código, instancia el siguiente objeto:

```java
// Access a Cloud Firestore instance from your Activity
FirebaseFirestore db = FirebaseFirestore.getInstance();
```

A través del objeto `db` lanzaremos todas las consultas a la base de datos. Los ejemplos básicos de insertar y leer datos los puedes obtener tanto en el GitHub de la asignatura como en Android Studio en `Tools>Firebase>Firestore`. En esta ruta también encontrarás una serie de ejemplos para lanzar consultas simples. Importante consultar:

* Modelo de datos: <https://firebase.google.com/docs/firestore/data-model?utm_source=studio>
* Ejemplos insertar datos: <https://firebase.google.com/docs/firestore/manage-data/add-data?utm_source=studio>
* Ejemplos leer datos: <https://firebase.google.com/docs/firestore/query-data/get-data?utm_source=studio>
* Consultas simples: <https://firebase.google.com/docs/firestore/query-data/queries?utm_source=studio>
