---
layout: post
title:  "Scripts movimiento y salto"
date:   2020-01-24 14:30:00 +0200
categories: unity
order: 1
parent: Unity
---

[Scripts](https://github.com/Manuel-Ag/PMD_19-20/tree/master/Unity/Movimiento_salto){: .btn .btn-blue }

# Scripts movimiento y salto

## `Update()` y `FixedUpdate()`:

Antes de nada hay que entender el uso de estos métodos:

<iframe width="560" height="315" src="https://www.youtube.com/embed/u42aWzAIAqg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Movimiento horizontal y vertical

```csharp
    [SerializeField] private float horizotal;
    [SerializeField] private float vertical;
    [SerializeField] private int velocidad = 2;
    private Rigidbody2D _rigid;

    // Start is called before the first frame update
    void Start()
    {
        _rigid = GetComponent<Rigidbody2D>();
    }

    // Update is called once per frame
    void Update()
    {
        horizotal = Input.GetAxis("Horizontal");
        vertical = Input.GetAxis("Vertical");

        Debug.Log(horizotal);
        Debug.Log(vertical);
    }

    private void FixedUpdate()
    {
        _rigid.velocity = new Vector2(horizotal * velocidad, vertical * velocidad);
    }
```

* `Debug.Log()` : Muestra mensajes por consola, en este caso las entradas del usuario.
* `_rigid.velocity` : Permite cambiar la velocidad del objeto.
* `[SerializeField]` : Tiene el mismo efecto que poner la variable `public`. Permite modificar la variable desde la interfaz de usuario de Unity.
* `GetComponent<Rigidbody2D>` : Devuelve una referencia al tipo de objeto definido dentro del mismo objeto.
* `GetAxis("horizontal")` : Variable predefinida por el entorno que permite capturar el evento de las fechas del teclado izquierda y derecha.


## Salto

```csharp
    [SerializeField] float _fuerzaSalto = 5f;
    private Rigidbody2D _rigid;
    private bool _isJump = false;


    // Start is called before the first frame update
    void Start()
    {
        _rigid = GetComponent<Rigidbody2D>();

    }

    // Update is called once per frame
    void Update()
    {
        if (Input.GetKey(KeyCode.Space))
            _isJump = true;
        else
            _isJump = false;
    }

    private void FixedUpdate()
    {
        if (_isJump)
        {
            _rigid.AddForce(new Vector2(0, _fuerzaSalto));
        }
    }
```

* `AddForce()` : Añade una fuerza en la dirección indicada al componente `_rigid`.
* `Input.GetKey(KeyCode.Space)` : Captura el evento click definido.

## Comprobar suelo

Para saltar hay que comprobar que el personaje está tocando el suelo. Lo podemos comprobar de tres formas

* Poniendo un objeto a los pies del personaje, obteniendo su compontente `transform` y calculando un círculo con algunos parámetros.

```csharp
private bool ComprobarSuelo1()
{
    return Physics2D.OverlapCircle(comprobadorSuelo.position, comprobadorRadio, mascaraSuelo);
}
```

<iframe width="560" height="315" src="https://www.youtube.com/embed/oBVemjrWocI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

* Cálculo mediante un rayo vertical partiendo del centro del objeto. `Debug.DrawRay()` al pasarle los mismo valores que a `Physics2D.RayCast()` nos permite visualizar donde está el rayo.

```csharp
private bool ComprobarSuelo2()
{
    RaycastHit2D raycastHit = Physics2D.Raycast(transform.position, Vector2.down, distanciaSuelo, mascaraSuelo);
    Debug.DrawRay(transform.position, Vector2.down, Color.red);
    if (raycastHit.collider != null)
    {
        return true;
    }

        return false;
}
```

* Cálculo mediante una caja. En vez de crear un rayo se crea una caja donde se desee. El método `BoxCast()` está definido en el script de GitHub y sirve para visualizar el espacio ocupado.

```csharp
private bool ComprobarSuelo3()
{
    // parámetros: centro, tamaño, ángulo, dirección, distancia?, layer
    BoxCast(new Vector2(transform.position.x, transform.position.y - 0.9f), new Vector2(2f,0.5f), 0f, new Vector2(-200, -200), 200f, mascaraSuelo);
    return Physics2D.BoxCast(new Vector2(transform.position.x, transform.position.y - 0.9f), new Vector2(2f, 0.5f), 0f, new Vector2(-200, -200), 200f, mascaraSuelo);
}
```

Ejemplo de `ComprobarSuelo2()` y `ComprobarSuelo3()`:

<iframe width="560" height="315" src="https://www.youtube.com/embed/c3iEl5AwUF8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
