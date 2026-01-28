¡Claro que sí! Vamos a actualizar el **Módulo 6** incluyendo la función `void main()`. Recuerda que `main` es la puerta de entrada: es donde le damos "Play" a nuestro código para que las clases cobren vida en forma de **objetos**.

---

### 1. Concepto de Clase y Objeto
La **Clase** es el plano y el **Objeto** es la construcción final.

#### Ejemplo 1: El Celular
```dart
class Celular {
  String marca = "Apple";
  String modelo = "iPhone 15";
}

void main() {
  var miCel = Celular(); // Creamos el objeto
  print("Mi celular es un ${miCel.marca} ${miCel.modelo}");
}
```
**Explicación:** La clase `Celular` define qué tiene cualquier teléfono. En `main`, creamos `miCel` (el objeto real) y accedemos a sus datos usando el punto `.`.

#### Ejemplo 2: El Estudiante
```dart
class Estudiante {
  String nombre = "Luis";
  int semestre = 4;
}

void main() {
  var alumno = Estudiante();
  print("El alumno ${alumno.nombre} va en ${alumno.semestre}° semestre.");
}
```
**Explicación:** `Estudiante` es el concepto. `alumno` es la persona real que ocupa un lugar en la memoria de la computadora.

#### Ejemplo 3: El Perro
```dart
class Perro {
  String nombre = "Fido";
}

void main() {
  var miMasTargeta = Perro();
  print("El nombre de mi perro es ${miMasTargeta.nombre}");
}
```
**Explicación:** Definimos un molde para perros y creamos uno llamado `miMasTargeta` para mostrar su nombre en pantalla.

---

### 2. Atributos (Características) y Métodos (Acciones)
Los atributos son variables y los métodos son funciones dentro de la clase.

#### Ejemplo 1: Un Foco inteligente
```dart
class Foco {
  bool encendido = false; // Atributo

  void switchLuz() { // Método
    encendido = !encendido;
    print(encendido ? "El foco está prendido" : "El foco está apagado");
  }
}

void main() {
  var miFoco = Foco();
  miFoco.switchLuz(); // Acción: Prender
  miFoco.switchLuz(); // Acción: Apagar
}
```
**Explicación:** El atributo `encendido` guarda el estado. El método `switchLuz` cambia ese estado y nos avisa qué pasó.

#### Ejemplo 2: Personaje de videojuego
```dart
class Guerrero {
  int vida = 100;

  void recibirDanio(int golpe) {
    vida -= golpe;
    print("¡Auch! Vida restante: $vida");
  }
}

void main() {
  var rambo = Guerrero();
  rambo.recibirDanio(30); // El objeto realiza la acción
}
```
**Explicación:** El guerrero tiene vida (atributo) y la capacidad de ser golpeado (método), lo cual modifica su vida.

#### Ejemplo 3: Contador simple
```dart
class Contador {
  int valor = 0;
  void incrementar() => valor++;
}

void main() {
  var clic = Contador();
  clic.incrementar();
  clic.incrementar();
  print("Total de clics: ${clic.valor}");
}
```
**Explicación:** El objeto `clic` mantiene la cuenta de cuántas veces se llamó al método `incrementar`.

---

### 3. Constructores básicos y nombrados
El constructor sirve para darle datos al objeto desde que "nace".

#### Ejemplo 1: Pizza personalizada (Básico)
```dart
class Pizza {
  String ingredientes;
  Pizza(this.ingredientes); // Constructor básico
}

void main() {
  var miPizza = Pizza("Peperoni y Queso");
  print("Pedí una pizza de ${miPizza.ingredientes}");
}
```
**Explicación:** Al crear `miPizza`, el constructor nos obliga a decirle de qué ingredientes es.

#### Ejemplo 2: Usuario e Invitado (Nombrado)
```dart
class Usuario {
  String nombre;
  Usuario(this.nombre); // Básico
  Usuario.invitado() : nombre = "Anónimo"; // Nombrado
}

void main() {
  var user1 = Usuario("Carlos");
  var user2 = Usuario.invitado();
  print("User 1: ${user1.nombre}, User 2: ${user2.nombre}");
}
```
**Explicación:** Tenemos dos formas de crear usuarios: dándoles un nombre o usando la versión rápida de "invitado".

#### Ejemplo 3: Coordenadas (Nombrado)
```dart
class Punto {
  int x, y;
  Punto.origen() : x = 0, y = 0; // Constructor que empieza en cero
}

void main() {
  var inicio = Punto.origen();
  print("Iniciamos en la posición: X:${inicio.x} Y:${inicio.y}");
}
```
**Explicación:** El constructor nombrado `.origen()` nos ahorra escribir que x y y valen cero.

---

### 4. Encapsulamiento y propiedades privadas
Usamos `_` para que nadie fuera de la clase pueda "meterle mano" a los datos importantes.

#### Ejemplo 1: El Saldo Bancario
```dart
class Cuenta {
  double _saldo = 500.0; // Privada

  void mostrarSaldo() => print("Tu saldo es: \$_$_saldo");
}

void main() {
  var miCuenta = Cuenta();
  // miCuenta._saldo = 0; // Esto daría error porque es privado
  miCuenta.mostrarSaldo();
}
```
**Explicación:** El saldo es secreto. Solo podemos verlo a través del método que el banco (la clase) nos permite usar.

#### Ejemplo 2: Motor de un Auto
```dart
class Auto {
  bool _motorEncendido = false;

  void encender() {
    _motorEncendido = true;
    print("Motor en marcha...");
  }
}

void main() {
  var miCoche = Auto();
  miCoche.encender();
}
```
**Explicación:** El usuario no toca el motor directamente, solo usa la llave (el método `encender`).

#### Ejemplo 3: Sistema de Login
```dart
class Login {
  String _pass = "12345";
  bool verificar(String intento) => intento == _pass;
}

void main() {
  var acceso = Login();
  print("¿Acceso concedido?: ${acceso.verificar("12345")}");
}
```
**Explicación:** La contraseña está oculta (`_pass`). Solo puedes saber si es correcta preguntándole a la clase.

---

### 5. Getters y Setters
Son puentes para leer o escribir datos privados con reglas.

#### Ejemplo 1: Validador de Calificación
```dart
class Examen {
  double _nota = 0;

  set nota(double valor) {
    if (valor >= 0 && valor <= 10) _nota = valor;
    else print("¡Error! La nota debe ser entre 0 y 10");
  }

  double get nota => _nota;
}

void main() {
  var mate = Examen();
  mate.nota = 11; // Intento inválido
  mate.nota = 9.5; // Intento válido
  print("Calificación final: ${mate.nota}");
}
```
**Explicación:** El `set` impide que pongamos un 11 o un -5. El `get` nos permite leer el valor guardado.

#### Ejemplo 2: Formato de nombres
```dart
class Persona {
  String _nombre = "";
  set nombre(String n) => _nombre = n.trim(); // Quita espacios extra
  String get nombre => "Sr/Sra. $_nombre";
}

void main() {
  var p = Persona();
  p.nombre = "  Ana  ";
  print(p.nombre); // Salida: Sr/Sra. Ana
}
```

#### Ejemplo 3: Convertidor de Temperatura
```dart
class Termometro {
  double _c = 0;
  set fahrenheit(double f) => _c = (f - 32) / 1.8;
  double get celsius => _c;
}

void main() {
  var t = Termometro();
  t.fahrenheit = 90;
  print("Grados Celsius: ${t.celsius.toStringAsFixed(1)}");
}
```

---

### 6. Herencia (`extends`) y `super`
Un hijo hereda lo del padre, pero puede tener sus propios detalles.

#### Ejemplo 1: Empleados
```dart
class Empleado {
  String nombre;
  Empleado(this.nombre);
  void trabajar() => print("$nombre está trabajando...");
}

class Programador extends Empleado {
  Programador(String nombre) : super(nombre); // Pasa el nombre al padre
}

void main() {
  var dev = Programador("Kevin");
  dev.trabajar(); // El programador usa el método del padre
}
```
**Explicación:** `Programador` no tuvo que escribir el método `trabajar`, lo heredó de `Empleado`.

#### Ejemplo 2: Animales y Sonidos
```dart
class Animal {
  void hacerSonido() => print("Sonido genérico");
}

class Gato extends Animal {
  @override
  void hacerSonido() => print("Miau!");
}

void main() {
  var michi = Gato();
  michi.hacerSonido();
}
```
**Explicación:** Con `@override` cambiamos el comportamiento que heredamos del padre para hacerlo específico.

#### Ejemplo 3: Superhéroes
```dart
class Heroe {
  String poder;
  Heroe(this.poder);
}

class Volador extends Heroe {
  Volador() : super("Volar");
}

void main() {
  var superman = Volador();
  print("Poder de Superman: ${superman.poder}");
}
```

---

### 7. Clases Abstractas e Interfaces
Definen qué debe hacer una clase, pero no cómo.

#### Ejemplo 1: Instrumento Musical (Abstracta)
```dart
abstract class Instrumento {
  void tocar(); // No tiene cuerpo, es una orden
}

class Guitarra extends Instrumento {
  void tocar() => print("Tocando acordes de guitarra");
}

void main() {
  var miLira = Guitarra();
  miLira.tocar();
}
```

#### Ejemplo 2: Contrato de Pago (Interface)
```dart
class Tarjeta implements Pago {
  void procesar() => print("Procesando pago con tarjeta...");
}

abstract class Pago {
  void procesar();
}

void main() {
  var visa = Tarjeta();
  visa.procesar();
}
```

#### Ejemplo 3: Control de volumen
```dart
abstract class Control {
  void subir();
}

class Radio implements Control {
  void subir() => print("Subiendo volumen de la radio");
}

void main() {
  Radio().subir();
}
```

---

### 8. Mixins (`with`)
Habilidades extra que se pueden "pegar" a las clases.

#### Ejemplo 1: Habilidad de Nadar
```dart
mixin Nadador {
  void nadar() => print("Estoy nadando...");
}

class Delfin with Nadador {}

void main() {
  Delfin().nadar();
}
```
**Explicación:** El `Delfin` adquiere la habilidad `Nadador` sin necesidad de una herencia compleja.

#### Ejemplo 2: Logger de errores
```dart
mixin Logger {
  void log(String msg) => print("DEBUG: $msg");
}

class App with Logger {
  void iniciar() => log("La app inició correctamente");
}

void main() {
  App().iniciar();
}
```

#### Ejemplo 3: Personaje Multitarea
```dart
mixin Volador { void volar() => print("Vuelo!"); }
mixin Corredor { void correr() => print("Corro!"); }

class SuperHumano with Volador, Corredor {}

void main() {
  var heroe = SuperHumano();
  heroe.volar();
  heroe.correr();
}
```
**Explicación:** Los mixins permiten que una clase tenga múltiples habilidades de diferentes fuentes de forma muy limpia.
