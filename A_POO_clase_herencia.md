Aquí tienes el código convertido a formato Markdown con resaltado de sintaxis para Dart.

### 1. El Código en Markdown

```dart
class Animal {
  String nombre;
  int edad;

  Animal({required this.nombre, required this.edad});

  void mostrarInformacion() {
    print('Nombre: $nombre');
    print('Edad: $edad años');
  }

  void hacerSonido() {
    print('$nombre hace un sonido genérico');
  }
}

void main() {
  Animal gato = Animal(nombre: 'peter', edad: 15);
  gato.mostrarInformacion();
  gato.hacerSonido(); 
}

```
Aquí tienes el código formateado en Markdown, listo para copiar y pegar en tu editor o notas.

Debajo del código, he añadido una explicación detallada de los conceptos nuevos que aparecen aquí (Herencia, `super` y `@override`), ya que este es un paso importante en tu aprendizaje de Dart.

### Código en Markdown

```dart
class Animal {
  String nombre;
  int edad;

  Animal({required this.nombre, required this.edad});

  void mostrarInformacion() {
    print('--- Información de Animal (desde Animal) ---');
    print('Nombre: $nombre');
    print('Edad: $edad años');
    print('------------------------------------------');
  }

  void hacerSonido() {
    print('$nombre hace un sonido genérico');
  }
}

// 'extends' indica Herencia: Perro adquiere todas las características de Animal
class Perro extends Animal {
  String raza;
  
  // Constructor:
  // 1. Recibe nombre, edad y raza.
  // 2. 'this.raza' se asigna a la propiedad de Perro.
  // 3. ': super(...)' envía el nombre y edad al constructor del padre (Animal).
  Perro({
    required String nombre, 
    required int edad, 
    required this.raza
  }) : super(nombre: nombre, edad: edad);
  
  // @override indica que estamos reemplazando el comportamiento original
  @override
  void hacerSonido() {
    print('$nombre dice: ¡Guau guau! 🐕');
  }
  
  // Método exclusivo de Perro (Animal no tiene esto)
  void morder() {
    print('$nombre está mordiendo un hueso 🦴');
  }
  
  @override
  void mostrarInformacion() {
    print('=== Información de Perro (desde Perro) ===');

    // super.metodo() llama a la versión original de la clase padre
    super.mostrarInformacion(); 
    
    print('Raza: $raza');
    print('==========================================');
  }
}

void main() {
  print('--- Demostrando un Animal genérico (Gato) ---');
  Animal gato = Animal(nombre: 'peter', edad: 15);
  gato.mostrarInformacion();
  gato.hacerSonido();
  
  print ('\n--- Demostrando Herencia con un Perro ---');
  Perro perro = Perro(nombre: 'Tobi', edad: 3, raza: 'chiuas');
  
  // Aquí se ejecuta la versión de Perro, que internamente llama a la de Animal
  perro.mostrarInformacion(); 
  
  perro.hacerSonido(); // Ejecuta la versión modificada (ladra)
  perro.morder();      // Ejecuta el método exclusivo de Perro
}

```

---

### Análisis de los Nuevos Conceptos

Este código introduce la **Herencia**, uno de los pilares de la Programación Orientada a Objetos.

#### 1. `extends Animal` (Herencia)

Al poner `class Perro extends Animal`, estás diciendo que el Perro **ES UN** Animal.

* Automáticamente gana las variables `nombre` y `edad`.
* Gana los métodos `mostrarInformacion` y `hacerSonido` sin tener que escribirlos de nuevo.

#### 2. `: super(...)` (El Constructor del Padre)

Cuando creas un `Perro`, Dart necesita asegurarse de que la parte de "Animal" del perro se construya correctamente.

* **El problema:** `nombre` y `edad` están en `Animal`.
* **La solución:** Usamos `: super(nombre: nombre, edad: edad)` para pasar esos datos hacia arriba, al constructor de la clase padre.

#### 3. `@override` (Sobrescritura)

A veces, lo que hace el padre no es suficiente o es incorrecto para el hijo.

* `Animal` hace un sonido genérico.
* `Perro` necesita ladrar.
* Usamos `@override` para decirle a Dart: "Ignora la función del padre, usa esta nueva versión específica para perros".

#### 4. `super.mostrarInformacion()`

Dentro de `Perro`, quieres mostrar la raza, pero **también** quieres mostrar el nombre y la edad.

* En lugar de escribir `print(nombre)` de nuevo (repertir código), llamas a `super.mostrarInformacion()`.
* Esto ejecuta el código de la clase `Animal` y luego continúa ejecutando el resto del código de `Perro`.

¿Te gustaría probar creando una tercera clase, por ejemplo `Gato extends Animal`, que tenga una propiedad única como `vidasRestantes`?
---

