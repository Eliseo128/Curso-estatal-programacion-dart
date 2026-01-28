¡Hola! Bienvenidos al mundo de **Dart**, el lenguaje que se usa para crear apps increíbles con Flutter. En este primer módulo, aprenderemos las bases, es decir, las piezas de "LEGO" con las que construiremos cualquier programa.

---

### 1. Variables y tipos de datos primitivos
Las variables son como "cajas" donde guardamos información. Cada caja tiene una etiqueta que dice qué tipo de cosas puede guardar.

*   **int:** Números enteros (sin decimales).
*   **double:** Números con punto decimal.
*   **String:** Texto (siempre entre comillas).
*   **bool:** Valores lógicos (verdadero o falso).

#### Ejemplo 1: Datos de un videojuego
```dart
void main() {
  int vidas = 3;             // Solo números enteros
  double puntaje = 95.5;      // Permite decimales
  String jugador = "Rex_99";  // Texto
  bool estaVivo = true;       // Solo true o false

  print("Jugador: $jugador, Vidas: $vidas");
}
```
**Explicación:** Aquí definimos la identidad de un jugador. Usamos `int` para las vidas porque no puedes tener "media vida" en este juego, y `double` para el puntaje porque puede ser muy exacto.

#### Ejemplo 2: Información de un producto
```dart
void main() {
  String producto = "Tenis Pro";
  double precio = 1250.50;
  int stock = 15;
  bool tieneDescuento = false;
}
```
**Explicación:** En una tienda escolar, el nombre es un `String`. El precio usa `double` por los centavos y el `stock` (cantidad en bodega) es `int` porque no vendes zapatos a la mitad.

#### Ejemplo 3: Perfil de estudiante
```dart
void main() {
  String nombre = "Ana García";
  int edad = 17;
  double promedio = 9.8;
  bool graduado = false;
}
```
**Explicación:** Representamos a un alumno. El `bool` nos sirve como un "interruptor" para saber si ya terminó la prepa o no.

---

### 2. Inferencia de tipos con `var`
A veces, Dart es lo suficientemente inteligente para saber qué tipo de dato es sin que se lo digamos explícitamente. A esto se le llama **inferencia**.

#### Ejemplo 1: Detectando texto
```dart
var ciudad = "Ciudad de México"; 
// Dart sabe que es un String.
```
**Explicación:** Al poner el texto entre comillas, Dart marca la "caja" como tipo `String` automáticamente.

#### Ejemplo 2: Detectando números
```dart
var anioActual = 2024; 
// Dart sabe que es un int.
```
**Explicación:** Como 2024 no tiene punto decimal, Dart asume que es un entero. Una vez que se asigna como `int`, no podrás meterle texto después.

#### Ejemplo 3: Listas rápidas
```dart
var temperatura = 24.5;
// Dart sabe que es un double.
```
**Explicación:** Útil cuando no quieres escribir `double` y quieres que el código se vea más limpio.

---

### 3. Variables inmutables: `final` y `const`
Usamos estas palabras cuando no queremos que el valor de una variable cambie nunca (son constantes).
*   **const:** El valor se conoce desde que escribes el código (tiempo de compilación).
*   **final:** El valor se conoce hasta que el programa se ejecuta (tiempo de ejecución).

#### Ejemplo 1: Valores matemáticos (`const`)
```dart
const double pi = 3.1415;
const int velocidadLuz = 299792458;
```
**Explicación:** El valor de PI o la velocidad de la luz nunca cambian y ya los conocemos antes de darle "Play" al programa. Usamos `const`.

#### Ejemplo 2: Datos del sistema (`final`)
```dart
final fechaActual = DateTime.now();
```
**Explicación:** La fecha y hora exactas no se saben hasta que corres el programa. Por eso usamos `final`, porque una vez que el programa obtiene la hora, ya no dejará que cambie.

#### Ejemplo 3: Configuración de usuario (`final`)
```dart
final String uuid = "abc-123-unique";
```
**Explicación:** Si un usuario entra a tu app, su ID único se genera en ese momento. No cambiará durante la sesión, pero no lo sabíamos antes de que el usuario iniciara sesión.

---

### 4. Operadores (Aritméticos, Comparación y Lógicos)
Son los símbolos que usamos para hacer cálculos o tomar decisiones.

#### Ejemplo 1: Operadores Aritméticos (Cálculos)
```dart
void main() {
  int a = 10;
  int b = 3;
  print(a + b); // Suma: 13
  print(a % b); // Residuo de la división: 1
}
```
**Explicación:** Usamos `+`, `-`, `*`, `/`. El símbolo `%` (módulo) es muy útil para saber si un número es par o impar.

#### Ejemplo 2: Operadores de Comparación (Preguntas)
```dart
void main() {
  int edad = 18;
  print(edad >= 18); // ¿Es mayor o igual? true
  print(edad == 20); // ¿Es igual a 20? false
}
```
**Explicación:** Se usan para comparar dos valores. El resultado siempre es un `bool` (true o false). Ojo: `==` es para comparar, `=` es para asignar valor.

#### Ejemplo 3: Operadores Lógicos (Combinar condiciones)
```dart
void main() {
  bool tieneTarea = true;
  bool hizoEjercicio = false;
  
  // && (Y): Ambos deben ser ciertos
  print(tieneTarea && hizoEjercicio); // false
  
  // || (O): Al menos uno debe ser cierto
  print(tieneTarea || hizoEjercicio); // true
}
```
**Explicación:** El operador `&&` es muy estricto, ambos deben cumplirse. El operador `||` es más flexible, con uno que se cumpla es suficiente.

---

### 5. Interpolación de cadenas de texto
Es la forma elegante de meter variables dentro de un texto sin estar usando muchos signos de más (`+`). Usamos el símbolo `$`.

#### Ejemplo 1: Variable simple
```dart
String mascota = "Solovino";
print("Mi perro se llama $mascota");
```
**Explicación:** Al poner `$mascota`, Dart saca el valor de la variable y lo pega dentro del mensaje.

#### Ejemplo 2: Operaciones dentro de texto
```dart
int base = 5;
int altura = 10;
print("El área del rectángulo es: ${base * altura}");
```
**Explicación:** Si quieres hacer una operación o usar algo más complejo, usas llaves `${ }`. Aquí multiplicamos antes de mostrar el resultado.

#### Ejemplo 3: Mayúsculas y métodos
```dart
String nombre = "lucía";
print("Hola, ${nombre.toUpperCase()}"); // Resultado: Hola, LUCÍA
```
**Explicación:** También usamos las llaves para llamar funciones especiales, como convertir un texto a mayúsculas justo antes de imprimirlo.
