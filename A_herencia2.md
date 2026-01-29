# Ejemplos de Herencia Simple en Dart (Nivel Principiante)

## 🐶 Ejemplo 1: Herencia con Clase `Animal`

```dart
void main() {
  print('========== EJEMPLO 1: HERENCIA CON ANIMALES ==========\n');
  
  Animal animalGenerico = Animal(nombre: 'Criatura', edad: 5);
  Perro perro = Perro(nombre: 'Firulais', edad: 3, raza: 'Labrador');
  Gato gato = Gato(nombre: 'Michi', edad: 2, color: 'Naranja');
  
  print('--- Animal Genérico ---');
  animalGenerico.mostrarInformacion();
  animalGenerico.hacerSonido();
  
  print('\n--- Perro ---');
  perro.mostrarInformacion();
  perro.hacerSonido();
  perro.morder();
  
  print('\n--- Gato ---');
  gato.mostrarInformacion();
  gato.hacerSonido();
  gato.ronronear();
  
  print('\n========== POLIMORFISMO ==========');
  List<Animal> listaAnimales = [animalGenerico, perro, gato];
  
  for (Animal animal in listaAnimales) {
    print('\n${animal.nombre}:');
    animal.hacerSonido();
  }
}

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

class Perro extends Animal {
  String raza;
  
  Perro({
    required String nombre, 
    required int edad, 
    required this.raza
  }) : super(nombre: nombre, edad: edad);
  
  @override
  void hacerSonido() {
    print('$nombre dice: ¡Guau guau! 🐕');
  }
  
  void morder() {
    print('$nombre está mordiendo un hueso 🦴');
  }
  
  @override
  void mostrarInformacion() {
    super.mostrarInformacion();
    print('Raza: $raza');
  }
}

class Gato extends Animal {
  String color;
  
  Gato({
    required String nombre, 
    required int edad, 
    required this.color
  }) : super(nombre: nombre, edad: edad);
  
  @override
  void hacerSonido() {
    print('$nombre dice: ¡Miau miau! 🐈');
  }
  
  void ronronear() {
    print('$nombre está ronroneando 😺');
  }
  
  @override
  void mostrarInformacion() {
    super.mostrarInformacion();
    print('Color: $color');
  }
}
```

## 👔 Ejemplo 2: Herencia con Clase `Empleado`

```dart
void main() {
  print('========== EJEMPLO 2: HERENCIA CON EMPLEADOS ==========\n');
  
  Empleado empleadoGenerico = Empleado(
    nombre: 'Juan Pérez', 
    puesto: 'Empleado General',
    salario: 2000
  );
  
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
  
  print('--- Empleado Genérico ---');
  empleadoGenerico.mostrarDatos();
  empleadoGenerico.trabajar();
  
  print('\n--- Desarrollador ---');
  desarrollador.mostrarDatos();
  desarrollador.trabajar();
  desarrollador.programar();
  desarrollador.mostrarExperiencia();
  
  print('\n--- Gerente ---');
  gerente.mostrarDatos();
  gerente.trabajar();
  gerente.dirigirReunion();
  gerente.mostrarEquipo();
  
  print('\n========== POLIMORFISMO ==========');
  List<Empleado> listaEmpleados = [empleadoGenerico, desarrollador, gerente];
  
  for (Empleado empleado in listaEmpleados) {
    print('\n${empleado.nombre}:');
    empleado.trabajar();
  }
}

class Empleado {
  String nombre;
  String puesto;
  double salario;
  
  Empleado({
    required this.nombre, 
    required this.puesto, 
    required this.salario
  });
  
  void mostrarDatos() {
    print('Nombre: $nombre');
    print('Puesto: $puesto');
    print('Salario: \$${salario.toStringAsFixed(2)}');
  }
  
  void trabajar() {
    print('$nombre está trabajando 💼');
  }
}

class Desarrollador extends Empleado {
  String lenguajePrincipal;
  int experiencia;
  
  Desarrollador({
    required String nombre, 
    required double salario, 
    required this.lenguajePrincipal, 
    required this.experiencia
  }) : super(
    nombre: nombre, 
    puesto: 'Desarrollador',
    salario: salario
  );
  
  @override
  void trabajar() {
    print('$nombre está programando en $lenguajePrincipal 💻');
  }
  
  void programar() {
    print('$nombre está escribiendo código limpio ✨');
  }
  
  void mostrarExperiencia() {
    print('$nombre tiene $experiencia años de experiencia');
  }
  
  @override
  void mostrarDatos() {
    super.mostrarDatos();
    print('Lenguaje Principal: $lenguajePrincipal');
    print('Experiencia: $experiencia años');
  }
}

class Gerente extends Empleado {
  String departamento;
  int numEmpleados;
  
  Gerente({
    required String nombre, 
    required double salario, 
    required this.departamento, 
    required this.numEmpleados
  }) : super(
    nombre: nombre, 
    puesto: 'Gerente',
    salario: salario
  );
  
  @override
  void trabajar() {
    print('$nombre está dirigiendo el departamento de $departamento 👔');
  }
  
  void dirigirReunion() {
    print('$nombre está dirigiendo una reunión importante 📊');
  }
  
  void mostrarEquipo() {
    print('$nombre supervisa a $numEmpleados empleados');
  }
  
  @override
  void mostrarDatos() {
    super.mostrarDatos();
    print('Departamento: $departamento');
    print('Empleados a cargo: $numEmpleados');
  }
}
```
