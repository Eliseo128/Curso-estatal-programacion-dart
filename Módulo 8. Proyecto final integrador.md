¡Felicidades! Has llegado al **Módulo 8**, el proyecto final. Aquí es donde todas las piezas del rompecabezas se unen.

En lugar de ver temas aislados, vamos a construir una estructura sólida. Dividiremos esta sección en la **Opción A** (Lógica pura de programación) y la **Opción B** (Cómo se conecta esto con el mundo real de las Apps).

---

## Opción A: Sistema de Gestión Escolar (Consola)

Este proyecto une Clases, Listas, Ciclos y Asincronía.

### 1. Definición de Clases: Alumno, Materia y Calificación
Primero, creamos los "moldes" para organizar nuestra información escolar.

#### Ejemplo 1: El objeto Alumno
```dart
class Alumno {
  String nombre;
  int id;
  Alumno(this.nombre, this.id);
}

void main() {
  var est = Alumno("Sofia", 101);
  print("Alumno registrado: ${est.nombre}");
}
```
**Explicación:** Usamos una clase básica con constructor para representar a un estudiante. Es la base de nuestro sistema.

#### Ejemplo 2: Materia con Calificación
```dart
class Materia {
  String nombre;
  double nota;
  Materia(this.nombre, this.nota);
}

void main() {
  var mat = Materia("Matemáticas", 9.5);
  print("Materia: ${mat.nombre}, Nota: ${mat.nota}");
}
```
**Explicación:** Aquí representamos una materia específica y la calificación que el alumno obtuvo en ella.

#### Ejemplo 3: El Alumno con sus Materias (Relación)
```dart
class Alumno {
  String nombre;
  List<Materia> materias = []; // Lista de objetos Materia
  
  Alumno(this.nombre);
}

void main() {
  var ana = Alumno("Ana");
  ana.materias.add(Materia("Programación", 10.0));
  print("${ana.nombre} tiene ${ana.materias.length} materia(s).");
}
```
**Explicación:** Este ejemplo es más avanzado (POO). Un objeto `Alumno` ahora "contiene" una lista de objetos `Materia`.

---

### 2. Uso de Listas y Funciones
Ahora necesitamos manejar a muchos alumnos y realizar acciones con ellos.

#### Ejemplo 1: Lista de Alumnos
```dart
void main() {
  List<String> alumnos = ["Pedro", "Lucía", "Roberto"];
  alumnos.add("Elena"); // Agregar
  alumnos.forEach((a) => print("Estudiante: $a"));
}
```
**Explicación:** Usamos una `List` para almacenar nombres y un ciclo para imprimir cada uno.

#### Ejemplo 2: Función para buscar alumnos
```dart
String buscarAlumno(List<String> lista, String nombre) {
  return lista.contains(nombre) ? "Encontrado" : "No registrado";
}

void main() {
  var lista = ["Juan", "Maria", "Jose"];
  print(buscarAlumno(lista, "Maria"));
}
```
**Explicación:** Creamos una función lógica que recibe una lista y un nombre, devolviendo un resultado usando el operador ternario.

#### Ejemplo 3: Filtrar aprobados (Funciones de lista)
```dart
void main() {
  List<double> notas = [5.5, 8.0, 9.2, 4.5, 7.0];
  var aprobados = notas.where((n) => n >= 6.0);
  print("Notas aprobatorias: $aprobados");
}
```
**Explicación:** Usamos `.where`, que es una función muy potente de Dart para filtrar datos rápidamente.

---

### 3. Búsqueda, Promedios y Simulación Asíncrona
El toque final: hacer que el sistema se sienta real con una carga de datos.

#### Ejemplo 1: Calcular promedio
```dart
double calcularPromedio(List<double> notas) {
  double suma = 0;
  for (var n in notas) { suma += n; }
  return suma / notas.length;
}

void main() {
  print("Promedio final: ${calcularPromedio([8, 9, 10])}");
}
```
**Explicación:** Un ciclo `for` recorre las notas para sumarlas y obtener la media aritmética.

#### Ejemplo 2: Simular carga de base de datos
```dart
Future<void> cargarBaseDatos() async {
  print("Conectando al servidor escolar...");
  await Future.delayed(Duration(seconds: 2));
  print("Datos descargados correctamente.");
}

void main() async {
  await cargarBaseDatos();
}
```
**Explicación:** Usamos `Future` y `async/await` para simular el tiempo que tardaría una app real en traer datos de internet.

#### Ejemplo 3: Sistema Integrado (Búsqueda Asíncrona)
```dart
Future<void> buscarEnArchivo(String nombre) async {
  print("Buscando a $nombre...");
  await Future.delayed(Duration(seconds: 1));
  print("Resultado: $nombre tiene promedio de 9.0");
}

void main() async {
  await buscarEnArchivo("Luis");
}
```
**Explicación:** Combinamos asincronía con lógica de búsqueda para crear una experiencia de usuario fluida.

---

## Opción B: Introducción Visual (Hacia Flutter)

Aquí vemos cómo lo que aprendiste se convierte en botones y pantallas.

### 1. Relación del código Dart con Flutter
En Flutter, todo es un "Widget", pero el Widget se alimenta de clases de Dart.

#### Ejemplo 1: Clase de Datos para la UI
```dart
class CardDato {
  String titulo;
  String color;
  CardDato(this.titulo, this.color);
}
// En Flutter, usarías esta clase para llenar una tarjeta visual.
```
**Explicación:** Las clases no solo guardan números, guardan la configuración de lo que el usuario verá en pantalla.

#### Ejemplo 2: Función que cambia el estado
```dart
bool estaPresionado = false;

void alDarClick() {
  estaPresionado = !estaPresionado;
  print("¿Boton encendido?: $estaPresionado");
}
```
**Explicación:** Esto es la base de la interactividad. Un clic en la pantalla ejecuta una función de Dart que cambia un valor.

#### Ejemplo 3: Mapeo de datos a "Pantalla"
```dart
void main() {
  List<String> mensajes = ["Hola", "Bienvenido", "Adiós"];
  // Imagina que cada mensaje se convierte en un globo de texto
  var widgets = mensajes.map((m) => "WidgetTexto($m)").toList();
  print(widgets);
}
```
**Explicación:** Usamos `.map` para transformar una lista de simples textos en una lista de "objetos visuales".

---

### 2. Demostración básica: To-Do List
La lógica detrás de una lista de tareas.

#### Ejemplo 1: Clase Tarea (Modelado)
```dart
class Tarea {
  String titulo;
  bool completada = false;
  Tarea(this.titulo);
}
```
**Explicación:** Cada tarea es un objeto con un nombre y un estado (completado o no).

#### Ejemplo 2: Agregar y eliminar tareas
```dart
void main() {
  List<Tarea> misTareas = [];
  misTareas.add(Tarea("Estudiar Dart")); // Agregar
  misTareas.removeAt(0); // Eliminar la primera
  print("Tareas pendientes: ${misTareas.length}");
}
```
**Explicación:** Las listas en Dart permiten gestionar dinámicamente lo que el usuario agrega o quita de su pantalla.

#### Ejemplo 3: Marcar como completada
```dart
void main() {
  var t1 = Tarea("Hacer ejercicio");
  print("¿Completada?: ${t1.completada}");
  
  t1.completada = true; // El usuario dio clic en el Checkbox
  print("¿Completada?: ${t1.completada}");
}
```
**Explicación:** Cambiar un atributo de un objeto es lo que hace que en una app visual aparezca una palomita o el texto se raye.

---
**¡Felicidades, programador!** Has completado los fundamentos de Dart. Ahora estás listo para dar el salto a **Flutter** y crear aplicaciones reales.
