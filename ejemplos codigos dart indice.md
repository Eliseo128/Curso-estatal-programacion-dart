# 🛠️ Ejemplos Prácticos: Curso de Dart (Módulos 1-8)

Aquí tienes los ejemplos prácticos solicitados para cada punto del temario, diseñados específicamente para ser claros y ejecutables por estudiantes de preparatoria.

---

## 🧱 Módulo 1: Fundamentos del Lenguaje

### 1. Variables y Tipos de Datos

**Ejemplo 1: Tipado Explícito vs Inferencia**
```dart
void main() {
  int edad = 16;          // Definimos que es entero explícitamente
  var nombre = "Sofia";   // Dart infiere que es String
  double altura = 1.75;   // Números con decimales
  print(nombre);
}
```

**Ejemplo 2: Booleanos**
```dart
void main() {
  bool esEstudiante = true;
  bool tieneLicencia = false;
  print("¿Es estudiante?: $esEstudiante");
}
```

**Ejemplo 3: Inmutabilidad (final vs const)**
```dart
void main() {
  final fechaHoy = DateTime.now(); // Se define en tiempo de ejecución (hoy cambia mañana)
  const pi = 3.1416;               // Se define antes de compilar (nunca cambia)
  // pi = 3.15; // Esto daría error
}
```

### 2. Operadores

**Ejemplo 1: Aritmética simple**
```dart
void main() {
  int x = 10;
  int y = 3;
  print(x % y); // Módulo (residuo): Imprime 1
  print(x ~/ y); // División entera: Imprime 3
}
```

**Ejemplo 2: Operadores de Asignación**
```dart
void main() {
  double puntos = 0;
  puntos += 10; // Suma y asigna (igual a puntos = puntos + 10)
  puntos *= 2;  // Multiplica y asigna
  print(puntos); // 20.0
}
```

**Ejemplo 3: Lógica Booleana**
```dart
void main() {
  bool tengoDinero = true;
  bool tengoTiempo = false;
  // AND (&&) requiere ambos verdaderos
  print(tengoDinero && tengoTiempo); // false
}
```

### 3. Interpolación de Strings

**Ejemplo 1: Básica**
```dart
void main() {
  String usuario = "Alex";
  print("Bienvenido al sistema, $usuario");
}
```

**Ejemplo 2: Con operaciones internas**
```dart
void main() {
  int a = 5;
  int b = 10;
  print("La suma de $a y $b es igual a ${a + b}");
}
```

**Ejemplo 3: Strings multilínea**
```dart
void main() {
  String menu = '''
  1. Jugar
  2. Opciones
  3. Salir
  ''';
  print(menu);
}
```

---

## 🔀 Módulo 2: Control de Flujo

### 1. Condicionales

**Ejemplo 1: If - Else if**
```dart
void main() {
  int calificacion = 85;
  if (calificacion >= 90) {
    print("Excelencia");
  } else if (calificacion >= 70) {
    print("Aprobado");
  } else {
    print("Reprobado");
  }
}
```

**Ejemplo 2: Operador Ternario (If corto)**
```dart
void main() {
  int edad = 17;
  // condición ? valor_si_verdadero : valor_si_falso
  String status = edad >= 18 ? "Mayor de edad" : "Menor de edad";
  print(status);
}
```

**Ejemplo 3: Switch Case**
```dart
void main() {
  String semaforo = "ROJO";
  switch (semaforo) {
    case "VERDE": print("Avanza"); break;
    case "AMARILLO": print("Precaución"); break;
    case "ROJO": print("Detente"); break;
    default: print("Semáforo averiado");
  }
}
```

### 2. Ciclos (Bucles)

**Ejemplo 1: Ciclo For estándar**
```dart
void main() {
  // Imprimir la tabla del 5
  for (int i = 1; i <= 10; i++) {
    print("5 x $i = ${5 * i}");
  }
}
```

**Ejemplo 2: While (mientras)**
```dart
void main() {
  int bateria = 5;
  while (bateria > 0) {
    print("Batería al $bateria%");
    bateria--;
  }
  print("Apagando...");
}
```

**Ejemplo 3: Break y Continue**
```dart
void main() {
  for (int i = 1; i <= 5; i++) {
    if (i == 3) continue; // Salta el 3
    if (i == 5) break;    // Rompe el ciclo antes de imprimir 5
    print("Número: $i");
  }
}
```

---

## 📦 Módulo 3: Funciones

### 1. Definición y Parámetros

**Ejemplo 1: Función simple con retorno**
```dart
double calcularAreaTriangulo(double base, double altura) {
  return (base * altura) / 2;
}
```

**Ejemplo 2: Parámetros Nombrados (Named Parameters)**
```dart
// Las llaves {} hacen los parámetros opcionales por nombre
// 'required' los hace obligatorios
void crearUsuario({required String nombre, int edad = 0}) {
  print("Usuario: $nombre, Edad: $edad");
}
// Uso: crearUsuario(nombre: "Ana", edad: 18);
```

**Ejemplo 3: Parámetros Opcionales Posicionales**
```dart
String saludo(String mensaje, [String? nombre]) {
  if (nombre != null) {
    return "$mensaje $nombre";
  }
  return mensaje;
}
// Uso: saludo("Hola") o saludo("Hola", "Juan")
```

### 2. Arrow Functions y Alcance

**Ejemplo 1: Sintaxis Flecha (=>)**
```dart
// Ideal para funciones de una sola línea
int sumar(int a, int b) => a + b;
```

**Ejemplo 2: Flecha con retorno booleano**
```dart
bool esPar(int numero) => numero % 2 == 0;
```

**Ejemplo 3: Alcance (Scope)**
```dart
String variableGlobal = "Soy visible en todo el archivo";

void prueba() {
  String variableLocal = "Solo existo dentro de prueba";
  print(variableGlobal); // Funciona
  print(variableLocal);  // Funciona
}
// print(variableLocal); // Error: No existe aquí
```

---

## 🗃️ Módulo 4: Colecciones

### 1. Listas y Mapas

**Ejemplo 1: Lista básica**
```dart
void main() {
  List<String> materias = ["Mate", "Historia", "Programación"];
  materias.add("Química");
  print(materias[0]); // Imprime "Mate"
}
```

**Ejemplo 2: Mapa (Diccionario)**
```dart
void main() {
  Map<String, dynamic> alumno = {
    "nombre": "Carlos",
    "edad": 16,
    "promedio": 9.5
  };
  print(alumno["nombre"]);
}
```

**Ejemplo 3: Set (Elementos únicos)**
```dart
void main() {
  Set<int> numeros = {1, 2, 3, 1, 2}; // Los repetidos se ignoran
  print(numeros); // {1, 2, 3}
}
```

### 2. Métodos Funcionales

**Ejemplo 1: For-in (Iteración simple)**
```dart
void main() {
  var frutas = ["Manzana", "Pera", "Uva"];
  for (var fruta in frutas) {
    print("Me gusta la $fruta");
  }
}
```

**Ejemplo 2: .map() (Transformar datos)**
```dart
void main() {
  var numeros = [1, 2, 3];
  var dobles = numeros.map((n) => n * 2).toList();
  print(dobles); // [2, 4, 6]
}
```

**Ejemplo 3: .where() (Filtrar datos)**
```dart
void main() {
  var edades = [15, 22, 12, 30, 17];
  var mayores = edades.where((edad) => edad >= 18).toList();
  print(mayores); // [22, 30]
}
```

---

## 🛡️ Módulo 5: Null Safety

### 1. Manejo de Nulos

**Ejemplo 1: Variable Nullable (?)**
```dart
void main() {
  String? nombre; // Puede ser String o null
  nombre = null;  // Válido
  // String apellido = null; // Error, no tiene '?'
}
```

**Ejemplo 2: Operador de Coalescencia (??)**
```dart
void main() {
  String? apodoUsuario;
  // Si apodoUsuario es null, usa "Invitado"
  String nombreMostrar = apodoUsuario ?? "Invitado";
  print(nombreMostrar);
}
```

**Ejemplo 3: Null Assertion (!)**
```dart
void main() {
  String? mensaje = "Hola";
  // Le aseguramos a Dart que NO es null (cuidado, si es null explota)
  print(mensaje!.length); 
}
```

---

## 🏗️ Módulo 6: Programación Orientada a Objetos (POO)

### 1. Clases, Objetos y Constructores

**Ejemplo 1: Clase básica**
```dart
class Perro {
  String nombre;
  String raza;

  // Constructor corto
  Perro(this.nombre, this.raza);

  void ladrar() {
    print("$nombre dice: ¡Guau!");
  }
}
```

**Ejemplo 2: Instanciación (Crear objeto)**
```dart
void main() {
  Perro miPerro = Perro("Firulais", "Pastor Alemán");
  miPerro.ladrar();
}
```

**Ejemplo 3: Constructor Nombrado**
```dart
class Rectangulo {
  double ancho, alto;
  Rectangulo(this.ancho, this.alto);

  // Constructor alternativo para cuadrados
  Rectangulo.cuadrado(double lado) : ancho = lado, alto = lado;
}
```

### 2. Encapsulamiento y Herencia

**Ejemplo 1: Propiedades Privadas (_)**
```dart
class CuentaBancaria {
  double _saldo = 0; // El _ hace que sea privado

  void depositar(double cantidad) {
    _saldo += cantidad;
  }
}
```

**Ejemplo 2: Herencia (extends)**
```dart
class Animal {
  void comer() => print("Comiendo...");
}

class Gato extends Animal {
  void maullar() => print("Miau");
}
// El gato puede comer() y maullar()
```

**Ejemplo 3: Clases Abstractas**
```dart
abstract class Figura {
  double calcularArea(); // Método sin cuerpo, obliga a definirlo
}

class Circulo extends Figura {
  double radio;
  Circulo(this.radio);

  @override
  double calcularArea() => 3.1416 * radio * radio;
}
```

---

## ⏳ Módulo 7: Asincronía

### 1. Future y Async/Await

**Ejemplo 1: Simulando espera (Future)**
```dart
void main() {
  print("Iniciando...");
  Future.delayed(Duration(seconds: 2), () {
    print("¡Han pasado 2 segundos!");
  });
  print("Fin del main (esto sale antes que los 2 segs)");
}
```

**Ejemplo 2: Async / Await (Esperar el resultado)**
```dart
Future<String> pedirPizza() async {
  await Future.delayed(Duration(seconds: 2));
  return "Pizza de Pepperoni";
}

void main() async {
  print("Pidiendo...");
  String miPizza = await pedirPizza();
  print("Llegó mi $miPizza");
}
```

**Ejemplo 3: Try / Catch en Asincronía**
```dart
Future<void> conectarInternet() async {
  try {
    // Simulamos un error
    throw Exception("No hay señal");
  } catch (e) {
    print("Error detectado: $e");
  }
}
```

---

## 🚀 Módulo 8: Proyecto Final Integrador (Sistema Escolar Simple)

Aquí dividimos el ejemplo en las 3 partes fundamentales de una aplicación.

### Ejemplo 1: El Modelo (La Clase de Datos)

```dart
class Alumno {
  String nombre;
  List<double> calificaciones;

  Alumno(this.nombre, this.calificaciones);

  // Método para obtener el promedio
  double obtenerPromedio() {
    if (calificaciones.isEmpty) return 0;
    double suma = calificaciones.reduce((a, b) => a + b);
    return suma / calificaciones.length;
  }
}
```

### Ejemplo 2: La Lógica (Gestor de Alumnos)

```dart
class Escuela {
  List<Alumno> listaAlumnos = [];

  void inscribir(String nombre) {
    listaAlumnos.add(Alumno(nombre, []));
    print("Alumno $nombre inscrito.");
  }

  void calificar(String nombre, double nota) {
    // Busca al alumno, 'firstWhere' busca el primero que cumpla la condición
    var alumno = listaAlumnos.firstWhere(
      (a) => a.nombre == nombre, 
      orElse: () => Alumno("No existe", []) // Retorno por defecto si no lo encuentra
    );
    
    if (alumno.nombre != "No existe") {
      alumno.calificaciones.add(nota);
      print("Nota agregada.");
    }
  }
}
```

### Ejemplo 3: El Main (La Interfaz de Usuario simulada)

```dart
void main() {
  Escuela prepa = Escuela();

  // 1. Inscribir
  prepa.inscribir("Luis");
  prepa.inscribir("Maria");

  // 2. Calificar
  prepa.calificar("Luis", 9.0);
  prepa.calificar("Luis", 8.5);
  prepa.calificar("Maria", 10.0);

  // 3. Ver resultados
  print("--- BOLETA ---");
  for (var alumno in prepa.listaAlumnos) {
    print("${alumno.nombre}: Promedio ${alumno.obtenerPromedio()}");
  }
}
```
