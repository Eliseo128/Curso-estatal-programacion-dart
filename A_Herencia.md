# Ejemplos de Herencia Simple en Dart (Nivel Principiante)

Aquí tienes **2 ejemplos completos** con herencia simple: `Animal` con subclases y `Empleado` con subclases. Incluyo explicaciones en comentarios, creación de instancias y uso de objetos.

---

## 🐶 Ejemplo 1: Herencia con Clase `Animal`

```dart
void main() {
  print('========== EJEMPLO 1: HERENCIA CON ANIMALES ==========\n');
  
  // ========== CREAR INSTANCIAS ==========
  
  // Crear un objeto de la clase base (Animal)
  Animal animalGenerico = Animal(nombre: 'Criatura', edad: 5);
  
  // Crear objetos de las clases hijas
  Perro perro = Perro(nombre: 'Firulais', edad: 3, raza: 'Labrador');
  Gato gato = Gato(nombre: 'Michi', edad: 2, color: 'Naranja');
  
  // ========== USAR LOS OBJETOS ==========
  
  print('--- Animal Genérico ---');
  animalGenerico.mostrarInformacion();
  animalGenerico.hacerSonido();
  
  print('\n--- Perro ---');
  perro.mostrarInformacion();
  perro.hacerSonido();      // Usa el método sobreescrito de Perro
  perro.morder();           // Método específico de Perro
  
  print('\n--- Gato ---');
  gato.mostrarInformacion();
  gato.hacerSonido();       // Usa el método sobreescrito de Gato
  gato.ronronear();         // Método específico de Gato
  
  // ========== POLIMORFISMO: Tratar objetos hijos como objetos padre ==========
  print('\n========== POLIMORFISMO ==========');
  List<Animal> listaAnimales = [animalGenerico, perro, gato];
  
  for (Animal animal in listaAnimales) {
    print('\n${animal.nombre}:');
    animal.hacerSonido();  // Cada animal hace su propio sonido
  }
}

// ===================================================================
// CLASE BASE (PADRE)
// ===================================================================
class Animal {
  // Atributos de la clase base
  String nombre;
  int edad;
  
  // Constructor de la clase base
  Animal({required this.nombre, required this.edad});
  
  // Método para mostrar información
  void mostrarInformacion() {
    print('Nombre: $nombre');
    print('Edad: $edad años');
  }
  
  // Método que será sobreescrito por las clases hijas
  void hacerSonido() {
    print('$nombre hace un sonido genérico');
  }
}

// ===================================================================
// CLASE HIJA 1: Perro HEREDA de Animal
// ===================================================================
class Perro extends Animal {  // 'extends' indica que Perro hereda de Animal
  // Atributo específico de Perro (no existe en Animal)
  String raza;
  
  // Constructor de Perro
  // Usamos 'super' para llamar al constructor de la clase padre (Animal)
  Perro({
    required String nombre, 
    required int edad, 
    required this.raza
  }) : super(nombre: nombre, edad: edad);  // Llama al constructor de Animal
  
  // SOBREESCRIBIR método de la clase padre
  // Usamos @override para indicar que estamos modificando un método heredado
  @override
  void hacerSonido() {
    print('$nombre dice: ¡Guau guau! 🐕');
  }
  
  // Método específico de Perro (no existe en Animal)
  void morder() {
    print('$nombre está mordiendo un hueso 🦴');
  }
  
  // Sobreescribir mostrarInformacion para incluir la raza
  @override
  void mostrarInformacion() {
    // Llamar al método de la clase padre para mostrar nombre y edad
    super.mostrarInformacion();
    // Agregar información específica de Perro
    print('Raza: $raza');
  }
}

// ===================================================================
// CLASE HIJA 2: Gato HEREDA de Animal
// ===================================================================
class Gato extends Animal {  // 'extends' indica que Gato hereda de Animal
  // Atributo específico de Gato
  String color;
  
  // Constructor de Gato
  Gato({
    required String nombre, 
    required int edad, 
    required this.color
  }) : super(nombre: nombre, edad: edad);  // Llama al constructor de Animal
  
  // SOBREESCRIBIR método de la clase padre
  @override
  void hacerSonido() {
    print('$nombre dice: ¡Miau miau! 🐈');
  }
  
  // Método específico de Gato
  void ronronear() {
    print('$nombre está ronroneando 😺');
  }
  
  // Sobreescribir mostrarInformacion para incluir el color
  @override
  void mostrarInformacion() {
    super.mostrarInformacion();  // Llama al método del padre
    print('Color: $color');
  }
}
```

**Salida esperada:**
```
========== EJEMPLO 1: HERENCIA CON ANIMALES ==========

--- Animal Genérico ---
Nombre: Criatura
Edad: 5 años
Criatura hace un sonido genérico

--- Perro ---
Nombre: Firulais
Edad: 3 años
Raza: Labrador
Firulais dice: ¡Guau guau! 🐕
Firulais está mordiendo un hueso 🦴

--- Gato ---
Nombre: Michi
Edad: 2 años
Color: Naranja
Michi dice: ¡Miau miau! 🐈
Michi está ronroneando 😺

========== POLIMORFISMO ==========

Criatura:
Criatura hace un sonido genérico

Firulais:
Firulais dice: ¡Guau guau! 🐕

Michi:
Michi dice: ¡Miau miau! 🐈
```

---

## 👔 Ejemplo 2: Herencia con Clase `Empleado`

```dart
void main() {
  print('========== EJEMPLO 2: HERENCIA CON EMPLEADOS ==========\n');
  
  // ========== CREAR INSTANCIAS ==========
  
  // Crear un objeto de la clase base (Empleado)
  Empleado empleadoGenerico = Empleado(
    nombre: 'Juan Pérez', 
    puesto: 'Empleado General',
    salario: 2000
  );
  
  // Crear objetos de las clases hijas
  Desarrollador desarrollador = Desarrollador(
    nombre: 'Ana García', 
    salario: 3500,
    lenguajePrincipal: 'Dart',
    experiencia: 5
  );
  
  Gerente gerente = Gerente(
    nombre: 'Carlos López', 
    salario: 5000,
    departamento: 'Tecnología',
    numEmpleados: 10
  );
  
  // ========== USAR LOS OBJETOS ==========
  
  print('--- Empleado Genérico ---');
  empleadoGenerico.mostrarDatos();
  empleadoGenerico.trabajar();
  
  print('\n--- Desarrollador ---');
  desarrollador.mostrarDatos();
  desarrollador.trabajar();           // Usa el método sobreescrito de Desarrollador
  desarrollador.programar();          // Método específico de Desarrollador
  desarrollador.mostrarExperiencia();
  
  print('\n--- Gerente ---');
  gerente.mostrarDatos();
  gerente.trabajar();                 // Usa el método sobreescrito de Gerente
  gerente.dirigirReunion();           // Método específico de Gerente
  gerente.mostrarEquipo();
  
  // ========== POLIMORFISMO ==========
  print('\n========== POLIMORFISMO ==========');
  List<Empleado> listaEmpleados = [empleadoGenerico, desarrollador, gerente];
  
  for (Empleado empleado in listaEmpleados) {
    print('\n${empleado.nombre}:');
    empleado.trabajar();  // Cada empleado trabaja de su manera
  }
}

// ===================================================================
// CLASE BASE (PADRE)
// ===================================================================
class Empleado {
  // Atributos comunes a todos los empleados
  String nombre;
  String puesto;
  double salario;
  
  // Constructor de la clase base
  Empleado({
    required this.nombre, 
    required this.puesto, 
    required this.salario
  });
  
  // Método para mostrar datos básicos
  void mostrarDatos() {
    print('Nombre: $nombre');
    print('Puesto: $puesto');
    print('Salario: \$${salario.toStringAsFixed(2)}');
  }
  
  // Método que será sobreescrito por las clases hijas
  void trabajar() {
    print('$nombre está trabajando 💼');
  }
}

// ===================================================================
// CLASE HIJA 1: Desarrollador HEREDA de Empleado
// ===================================================================
class Desarrollador extends Empleado {
  // Atributos específicos de Desarrollador
  String lenguajePrincipal;
  int experiencia;  // años de experiencia
  
  // Constructor de Desarrollador
  // Nota: El puesto se establece automáticamente como "Desarrollador"
  Desarrollador({
    required String nombre, 
    required double salario, 
    required this.lenguajePrincipal, 
    required this.experiencia
  }) : super(
    nombre: nombre, 
    puesto: 'Desarrollador',  // Valor fijo para todos los desarrolladores
    salario: salario
  );
  
  // SOBREESCRIBIR método trabajar
  @override
  void trabajar() {
    print('$nombre está programando en $lenguajePrincipal 💻');
  }
  
  // Método específico de Desarrollador
  void programar() {
    print('$nombre está escribiendo código limpio ✨');
  }
  
  // Método para mostrar experiencia
  void mostrarExperiencia() {
    print('$nombre tiene $experiencia años de experiencia');
  }
  
  // Sobreescribir mostrarDatos para incluir información específica
  @override
  void mostrarDatos() {
    super.mostrarDatos();  // Muestra nombre, puesto y salario
    print('Lenguaje Principal: $lenguajePrincipal');
    print('Experiencia: $experiencia años');
  }
}

// ===================================================================
// CLASE HIJA 2: Gerente HEREDA de Empleado
// ===================================================================
class Gerente extends Empleado {
  // Atributos específicos de Gerente
  String departamento;
  int numEmpleados;  // número de empleados a cargo
  
  // Constructor de Gerente
  // Nota: El puesto se establece automáticamente como "Gerente"
  Gerente({
    required String nombre, 
    required double salario, 
    required this.departamento, 
    required this.numEmpleados
  }) : super(
    nombre: nombre, 
    puesto: 'Gerente',  // Valor fijo para todos los gerentes
    salario: salario
  );
  
  // SOBREESCRIBIR método trabajar
  @override
  void trabajar() {
    print('$nombre está dirigiendo el departamento de $departamento 👔');
  }
  
  // Método específico de Gerente
  void dirigirReunion() {
    print('$nombre está dirigiendo una reunión importante 📊');
  }
  
  // Método para mostrar tamaño del equipo
  void mostrarEquipo() {
    print('$nombre supervisa a $numEmpleados empleados');
  }
  
  // Sobreescribir mostrarDatos para incluir información específica
  @override
  void mostrarDatos() {
    super.mostrarDatos();  // Muestra nombre, puesto y salario
    print('Departamento: $departamento');
    print('Empleados a cargo: $numEmpleados');
  }
}
```

**Salida esperada:**
```
========== EJEMPLO 2: HERENCIA CON EMPLEADOS ==========

--- Empleado Genérico ---
Nombre: Juan Pérez
Puesto: Empleado General
Salario: $2000.00
Juan Pérez está trabajando 💼

--- Desarrollador ---
Nombre: Ana García
Puesto: Desarrollador
Salario: $3500.00
Lenguaje Principal: Dart
Experiencia: 5 años
Ana García está programando en Dart 💻
Ana García está escribiendo código limpio ✨
Ana García tiene 5 años de experiencia

--- Gerente ---
Nombre: Carlos López
Puesto: Gerente
Salario: $5000.00
Departamento: Tecnología
Empleados a cargo: 10
Carlos López está dirigiendo el departamento de Tecnología 👔
Carlos López está dirigiendo una reunión importante 📊
Carlos López supervisa a 10 empleados

========== POLIMORFISMO ==========

Juan Pérez:
Juan Pérez está trabajando 💼

Ana García:
Ana García está programando en Dart 💻

Carlos López:
Carlos López está dirigiendo el departamento de Tecnología 👔
```

---

## 📌 Resumen Visual de Herencia

```
┌─────────────────────────────────────────────────┐
│              CLASE BASE (PADRE)                 │
│              class Animal / Empleado            │
│  ┌─────────────────────────────────────────┐   │
│  │ Atributos comunes                        │   │
│  │ - nombre                                 │   │
│  │ - edad / salario                         │   │
│  ├─────────────────────────────────────────┤   │
│  │ Métodos comunes                          │   │
│  │ - mostrarInformacion() / mostrarDatos()  │   │
│  │ - hacerSonido() / trabajar()             │   │
│  └─────────────────────────────────────────┘   │
└─────────────────────┬───────────────────────────┘
                      │
        ┌─────────────┴─────────────┐
        │                           │
┌───────▼────────┐         ┌────────▼───────┐
│ CLASE HIJA 1   │         │  CLASE HIJA 2  │
│   class Perro  │         │   class Gato   │
│                │         │                │
│ Atributos      │         │ Atributos      │
│ - raza         │         │ - color        │
│                │         │                │
│ Métodos        │         │ Métodos        │
│ - morder()     │         │ - ronronear()  │
│ - @override    │         │ - @override    │
│   hacerSonido()│         │   hacerSonido()│
└────────────────┘         └────────────────┘
```

---

## 📚 Explicación de Conceptos Clave

### 1. **Herencia (`extends`)**
```dart
class Perro extends Animal { ... }
```
- `extends` indica que `Perro` **hereda** de `Animal`
- `Perro` obtiene automáticamente todos los atributos y métodos de `Animal`
- Se dice que `Animal` es la **clase padre** y `Perro` es la **clase hija**

### 2. **Constructor con `super`**
```dart
Perro({required this.raza}) : super(nombre: nombre, edad: edad);
```
- `super()` llama al constructor de la clase padre
- Es obligatorio cuando la clase padre tiene un constructor con parámetros
- Permite inicializar los atributos heredados

### 3. **Sobreescritura de métodos (`@override`)**
```dart
@override
void hacerSonido() {
  print('$nombre dice: ¡Guau guau!');
}
```
- `@override` indica que estamos modificando un método heredado
- El método debe tener la **misma firma** (mismo nombre y parámetros)
- Permite que cada clase hija tenga su propia implementación

### 4. **Métodos específicos**
```dart
void morder() {
  print('$nombre está mordiendo un hueso');
}
```
- Métodos que existen **solo en la clase hija**
- No están disponibles en la clase padre ni en otras clases hijas

### 5. **Polimorfismo**
```dart
List<Animal> animales = [perro, gato];
for (Animal animal in animales) {
  animal.hacerSonido();  // Cada uno hace su propio sonido
}
```
- Tratar objetos de diferentes clases hijas como si fueran de la clase padre
- Cada objeto ejecuta su propia versión del método

---

## 💡 Consejos para Principiantes

1. **Usa herencia** cuando varias clases comparten características comunes
2. **La clase padre** debe contener lo que es **común** a todas las hijas
3. **Las clases hijas** deben contener lo que las **diferencia** del resto
4. **Siempre usa `@override`** al sobreescribir métodos (es una buena práctica)
5. **`super()` es obligatorio** si la clase padre tiene un constructor con parámetros obligatorios
6. **`super.metodo()`** permite llamar al método original de la clase padre

¡La herencia te ayuda a evitar repetir código y organizar mejor tus clases! 🎯
