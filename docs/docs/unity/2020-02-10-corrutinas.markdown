---
layout: post
title:  "Corrutinas"
date:   2020-02-10 14:30:00 +0200
categories: unity
order: 1
parent: Unity
---

[Coroutines](https://docs.unity3d.com/Manual/Coroutines.html){: .btn .btn-green }

# Corrutinas

Una corrutina es un método que puede pausar su ejecución y continuarla según los parámetros o tiempo definidos. Es muy útil para programar acciones futuras, definir que algo suceda periódicamente, ordenar una serie de eventos para que ocurran uno detrás de otro, etc.

## Ejemplo de utilización

Se debe de crear la corrutina y deffinir en el `yield` el comportamiento, en este caso esperar 2 segundos:

```csharp
IEnumerator Coroutine()
{
    Debug.Log("Iniciada corrutina");
    yield return new WaitForSeconds(2f);
    Debug.Log("Finalizada corrutina");
}
```

Para lanzar la corrutina llamamos al método `StartCoroutine()` :

```csharp
void Update()
{
    if (Input.anyKeyDown)
        StartCoroutine(Coroutine());
}
```
Se puede observar como se lanza el primer `Debug.Log()` pero para el segundo espera 2 segundos.

## Otro ejemplo

Acción periódica:

```csharp
IEnumerator Coroutine2(float time)
{
    int i = 0;
    while (i < 10)
    {
        Debug.Log("Bucle corrutina" + i);
        i++;
        yield return new WaitForSeconds(time);
    }
}
```

En esta ocasión en la corrutina hay un bucle `while` y dentro del `yield return`. El bucle se ejecutará `i` veces pausando un tiempo definido por `time`. `time` se pasará como parámetro de la siguiente forma:

```csharp
void Update()
{
    if (Input.anyKeyDown)
        StartCoroutine(Coroutine2(1f));
}
```

## Tipos de yield return

* **yield break** : Detiene la corrutina.
* **yield return null** : Detiene la corrutina un frame.
* **WaitForSeconds(1f)** : Detiene la corrutina 1 segundo.
* **yield WaitForSecondsRealTime(1f)** : Detiene la corrutina 1 segundo sin escala de tiempo.
* **yield WaitUntil(condición)** : Detiene la corrutina hasta que la condición sea true.
* **yield WaitWhile(condición)** : Detiene la corrutina mientras la condición sea true.


## Detener una Corrutina

* `StopCoroutine(Coroutine)`
* `StopCoroutine(IEnumerator)`
* `StopAllCoroutines()`  

## Corrutina esperando la finalización de otra

Simplemente al declarar `yiel return` se pasa como parámetro el inicio de otra corrutina:

```csharp
IEnumerator Coroutine3()
{
    Debug.Log("Co3: Esperando a que finalice la corrutina 4...");
    yield return StartCoroutine(Coroutine4());
    Debug.Log("Co3: Acabado");
}

IEnumerator Coroutine4()
{
    Debug.Log("Co4: Hola, soy la corrutina4, la 3 está esperando a que yo finalice...");
    yield return new WaitForSeconds(3f);
    Debug.Log("Co4: Acabado");
}
```
