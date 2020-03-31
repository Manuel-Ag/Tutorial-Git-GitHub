---
layout: post
title:  "Firebase Authentication"
date:   2020-01-17 14:30:00 +0200
categories: segundo_trimestre
order: 1
parent: Segundo trimestre Android
---

[GitHub](https://github.com/Manuel-Ag/PMD_19-20/tree/master/firebase){: .btn .btn-blue } [Documentación](https://firebase.google.com/docs/auth?hl=es){: .btn .btn-green }

# Firebase Authentication

<iframe width="560" height="315" src="https://www.youtube.com/embed/8sGY55yxicA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

En el propio entorno de Android Studio tenemos una pequeña ayuda para empezar con Firebase (tools>Firebase):

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_firebase/captura7.png)
{:refdef}

En los diferentes apartados tendremos un ejemplo de código para tener una prueba funcionando rápidamente. Utilizaremos este código para realizar una autenticación en nuestra app. Recuerda importar el `google-services.json` de tu proyecto Firebase, ya que no está en el repositorio. También activa la opción de autenticarse por usuario y contraseña:

{:refdef: style="text-align: center;"}
![Android]({{ site.baseurl }}/assets/img_post_firebase/captura8.png)
{:refdef}

Y configurar el proyecto para permitir autenticación:

[Documentación](https://firebase.google.com/docs/auth/android/start?hl=es){: .btn .btn-green }

Se dividirá en varios apartados:

## Instancia

```java
FirebaseAuth mAuth = FirebaseAuth.getInstance();
```

A través de los métodos de `mAuth` podremos realizar todas las opciones.

## Login

```java
    public void login(View v) {
        mAuth.signInWithEmailAndPassword(editTextEmail.getText().toString(), editTextPassword.getText().toString())
                .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {
                        if (task.isSuccessful()) {
                            // Sign in success, update UI with the signed-in user's information
                            Log.d("prueba", "signInWithEmail:success");
                            FirebaseUser user = mAuth.getCurrentUser();
                            Toast.makeText(MainActivity.this, "Correcto: " + user, Toast.LENGTH_SHORT).show();
                            startActivity(new Intent(MainActivity.this, Main2Activity.class));
                        } else {
                            // If sign in fails, display a message to the user.
                            Log.w("prueba", "signInWithEmail:failure", task.getException());
                        }
                    }
                });
    }
    
```

Cuando el usuario consiga autenticarse lanzaremos otra actividad.

## Crear usuario

```java
public void crear(View v) {
    mAuth.createUserWithEmailAndPassword(editTextEmail.getText().toString(), editTextPassword.getText().toString())
            .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
                @Override
                public void onComplete(@NonNull Task<AuthResult> task) {
                    if (task.isSuccessful()) {
                        // Sign in success, update UI with the signed-in user's information
                        Log.d("prueba", "createUserWithEmail:success");
                    } else {
                        // If sign in fails, display a message to the user.
                        Log.w("prueba", "createUserWithEmail:failure", task.getException());
                    }
                }
            });
}
```

Se debe proporcionar un usuario y contraseña válidos.

## Enviar email de verificación en el registramos

```java
private void enviarEmail() {
    final FirebaseUser user = mAuth.getCurrentUser();
    user.sendEmailVerification()
            .addOnCompleteListener(this, new OnCompleteListener() {
                @Override
                public void onComplete(@NonNull Task task) {
                    if (task.isSuccessful()) {
                        Toast.makeText(MainActivity.this, "Email enviado", Toast.LENGTH_SHORT).show();
                    } else {
                        Toast.makeText(MainActivity.this, "Error", Toast.LENGTH_SHORT).show();
                    }
                }
            });
}
```

Hay que llamar a este método cuando se cree una cuenta de usuario satisfactoriamente.

## Login comprobando que se ha verificado mediante Email

```java
public void loginConEmail(View v) {
    mAuth.signInWithEmailAndPassword(editTextEmail.getText().toString(), editTextPassword.getText().toString())
            .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
                @Override
                public void onComplete(@NonNull Task<AuthResult> task) {
                    if (task.isSuccessful()) {
                        // Sign in success, update UI with the signed-in user's information
                        Log.d("prueba", "signInWithEmail:success");
                        FirebaseUser user = mAuth.getCurrentUser();
                        if (user.isEmailVerified()) {
                            startActivity(new Intent(MainActivity.this, Main2Activity.class));
                        }
                        else
                            Toast.makeText(MainActivity.this, "Verifica el email", Toast.LENGTH_SHORT).show();
                    } else {
                        ...
                    }
                }
            });
}
```
