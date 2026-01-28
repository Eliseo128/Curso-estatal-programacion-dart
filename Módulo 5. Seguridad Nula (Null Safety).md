¡Bienvenido al **Módulo 5**! Este es uno de los temas más importantes en el Dart moderno. 

**¿Qué es Null Safety?** Imagina que intentas abrir una caja de cereal para desayunar, pero cuando la abres, la caja está totalmente vacía. ¡Qué decepción! En programación, cuando una variable no tiene nada, decimos que es `null`. Si intentas hacer algo con una variable vacía (como calcular su tamaño o sumar su valor), el programa "explota" (falla). Null Safety es un sistema de seguridad que evita que estos errores ocurran.

---

### 1. El problema de los valores nulos
Antes, Dart permitía que cualquier variable fuera `null`. Esto causaba muchos errores porque el programador olvidaba que una variable podía estar vacía.

#### Ejemplo 1: El nombre que no existe
```dart
// Si no existiera Null Safety:
String nombre; // Imagina que esto puede ser null
print(nombre.length); // ERROR: No puedes contar las letras de "nada"
```
**Explicación:** Si intentas contar las letras de un nombre que no ha sido escrito, el programa se cierra. Es como intentar cepillarle el pelo a alguien que no está en la habitación.

#### Ejemplo 2: Operaciones matemáticas con "nada"
```dart
int precio;
int total = precio + 10; // ERROR
```
**Explicación:** No puedes sumarle 10 a un valor que no existe. Dart moderno te detiene desde antes de que corras el programa para avisarte que `precio` no tiene valor.

#### Ejemplo 3: El "Crush" de la App
**Explicación:** En apps de redes sociales antiguas, si un usuario no ponía su biografía y la app intentaba mostrarla, la app se cerraba sola. Ese es el famoso error "Null Pointer Exception". Null Safety evita que el usuario vea esos cierres inesperados.

---

### 2. Tipos Nullable y Non-nullable (`?`)
En Dart moderno, por defecto, **nada puede ser nulo**. Si quieres permitir que una variable esté vacía, debes avisarle a Dart usando un signo de interrogación `?`.

#### Ejemplo 1: El segundo nombre
```dart
String nombre = "Juan"; // No puede ser nulo nunca
String? segundoNombre = null; // Sí puede ser nulo (porque tiene ?)
```
**Explicación:** Todos tenemos un primer nombre, pero no todos tenemos un segundo nombre. Por eso, el primer nombre es "seguro" y el segundo es "nullable" (`?`).

#### Ejemplo 2: Teléfono opcional
```dart
int? telefono; // El usuario puede decidir no darlo
int edad = 17; // La edad es obligatoria
```
**Explicación:** Al poner `int?`, le decimos a Dart: "Oye, esta caja puede tener un número o puede estar vacía, no te asustes".

#### Ejemplo 3: Red de Wi-Fi
```dart
String? redActual = "Infinitum_5G";
redActual = null; // Me desconecté, ahora no hay red.
```
**Explicación:** Como la conexión puede ir y venir, usamos `String?`. Si no usáramos el `?`, Dart no nos dejaría poner la variable en `null`.

---

### 3. Operador de aserción de no nulidad (`!`)
A veces, Dart está preocupado porque piensa que algo es nulo, pero tú, como programador, **estás 100% seguro** de que no lo es. El signo `!` es como decirle: "¡Confía en mí, yo sé lo que hago!".

#### Ejemplo 1: Forzar la lectura
```dart
String? mensaje Secreto = "Hola";
print(mensajeSecreto!.length); 
```
**Explicación:** Dart ve que `mensajeSecreto` tiene un `?`, así que tiene miedo de medirlo. Con el `!`, tú le aseguras que en ese momento exacto sí hay un mensaje ahí. *¡Cuidado! Si usas ! y la variable está vacía, el programa fallará.*

#### Ejemplo 2: De un nullable a un seguro
```dart
int? monedasEnBolsillo = 10;
int total = monedasEnBolsillo!; // Forzamos a que entre en una variable no-nula
```
**Explicación:** Como `total` no acepta nulos, usamos `!` para pasarle el valor de la variable que sí aceptaba nulos.

#### Ejemplo 3: El examen entregado
```dart
String? examenRecibido = "Examen de Matemáticas";
// El profesor está seguro que ya lo recibió:
print("Revisando: " + examenRecibido!);
```
**Explicación:** El profesor usa `!` porque ya vio el examen sobre su escritorio, aunque el sistema diga que "podría" no estar.

---

### 4. Inicialización tardía con `late`
A veces sabes que una variable **no será nula**, pero no puedes darle su valor justo en el momento en que la creas (por ejemplo, porque el valor vendrá de una base de datos más tarde). Para eso usamos `late`.

#### Ejemplo 1: Nombre de usuario tras el Login
```dart
late String usuario;

void login() {
  usuario = "GamerPro_22";
}

void mostrarPerfil() {
  print(usuario);
}
```
**Explicación:** No sabemos el nombre del usuario hasta que haga login. Usamos `late` para prometerle a Dart: "No te doy el valor ahorita, pero te juro que te lo daré antes de que lo uses".

#### Ejemplo 2: El resultado de una suma después
```dart
late int resultado;

void calcular() {
  resultado = 5 + 5;
}
```
**Explicación:** Si tratas de usar `resultado` antes de llamar a `calcular()`, el programa fallará. `late` es una promesa de que llenarás la caja pronto.

#### Ejemplo 3: Configuración de la App
```dart
late double anchoPantalla;

void configurar() {
  anchoPantalla = 1080.0;
}
```
**Explicación:** El ancho de la pantalla se sabe hasta que la app arranca en el celular. Como no es un valor que cambie (es seguro), usamos `late` en lugar de `?` para no tener que estar lidiando con nulos después.
