# Ejemplos de Clases en Dart (Nivel Principiante)

Aquí tienes **2 ejemplos completos** con clases `Animal` y `Empleado`, cada una con 2 atributos y 2 funciones, incluyendo creación de instancias y uso de objetos.

---

## 🐶 Ejemplo 1: Clase `Animal`

```dart
void main() {
  // Crear instancias (objetos) de la clase Animal
  Animal perro = Animal(nombre: 'Firulais', edad: 3);
  Animal gato = Animal(nombre: 'Michi', edad: 2);
  
  // Usar los objetos
  print('=== Primer Animal ===');
  perro.mostrarInformacion();
  perro.hacerSonido();
  
  print('\n=== Segundo Animal ===');
  gato.mostrarInformacion();
  gato.hacerSonido();
  
  // Modificar atributo y volver a mostrar
  print('\n=== Después de cumplir años ===');
  perro.cumplirAnios();
  perro.mostrarInformacion();
}

// Definición de la clase Animal
class Animal {
  // Atributos (propiedades)
  String nombre;
  int edad;
  
  // Constructor
  Animal({required this.nombre, required this.edad});
  
  // Función 1: Mostrar información del animal
  void mostrarInformacion() {
    print('Nombre: $nombre');
    print('Edad: $edad años');
  }
  
  // Función 2: Hacer un sonido característico
  void hacerSonido() {
    print('$nombre dice: ¡Guau guau!'); // Para perros, pero podríamos personalizar
  }
  
  // Función extra para demostrar modificación de atributos
  void cumplirAnios() {
    edad = edad + 1;
    print('$nombre ha cumplido un año más 🎂');
  }
}
```

**Salida esperada:**
```
=== Primer Animal ===
Nombre: Firulais
Edad: 3 años
Firulais dice: ¡Guau guau!

=== Segundo Animal ===
Nombre: Michi
Edad: 2 años
Michi dice: ¡Guau guau!

=== Después de cumplir años ===
Firulais ha cumplido un año más 🎂
Nombre: Firulais
Edad: 4 años
```

---

## 👔 Ejemplo 2: Clase `Empleado`

```dart
void main() {
  // Crear instancias (objetos) de la clase Empleado
  Empleado empleado1 = Empleado(nombre: 'Ana García', puesto: 'Desarrolladora');
  Empleado empleado2 = Empleado(nombre: 'Carlos López', puesto: 'Diseñador');
  
  // Usar los objetos
  print('=== Empleado 1 ===');
  empleado1.mostrarDatos();
  empleado1.trabajar();
  
  print('\n=== Empleado 2 ===');
  empleado2.mostrarDatos();
  empleado2.trabajar();
  
  // Modificar atributo directamente y mostrar cambios
  print('\n=== Después de un ascenso ===');
  empleado1.puesto = 'Senior Developer';
  empleado1.mostrarDatos();
}

// Definición de la clase Empleado
class Empleado {
  // Atributos (propiedades)
  String nombre;
  String puesto;
  
  // Constructor
  Empleado({required this.nombre, required this.puesto});
  
  // Función 1: Mostrar datos del empleado
  void mostrarDatos() {
    print('Nombre: $nombre');
    print('Puesto: $puesto');
  }
  
  // Función 2: Simular trabajo
  void trabajar() {
    print('$nombre está trabajando como $puesto 💼');
  }
}
```

**Salida esperada:**
```
=== Empleado 1 ===
Nombre: Ana García
Puesto: Desarrolladora
Ana García está trabajando como Desarrolladora 💼

=== Empleado 2 ===
Nombre: Carlos López
Puesto: Diseñador
Carlos López está trabajando como Diseñador 💼

=== Después de un ascenso ===
Nombre: Ana García
Puesto: Senior Developer
```

---

## 📌 Explicación para Principiantes

### Estructura básica de una clase:
```dart
class NombreClase {
  // 1. Atributos (datos que guarda el objeto)
  Tipo atributo1;
  Tipo atributo2;
  
  // 2. Constructor (crea el objeto con valores iniciales)
  NombreClase({required this.atributo1, required this.atributo2});
  
  // 3. Funciones/Métodos (acciones que puede hacer el objeto)
  void nombreFuncion() {
    // Código aquí
  }
}
```

### Crear y usar objetos:
```dart
// Crear instancia (objeto)
Clase objeto = Clase(atributo1: valor1, atributo2: valor2);

// Usar atributos
print(objeto.atributo1);

// Usar funciones
objeto.nombreFuncion();
```

### 🔑 Conceptos clave:
- **Clase**: Es el "molde" o "plano" para crear objetos (ej: `Animal`).
- **Objeto/Instancia**: Es un elemento concreto creado a partir de la clase (ej: `perro`).
- **Atributos**: Son las características/características del objeto (ej: `nombre`, `edad`).
- **Métodos/Funciones**: Son las acciones que puede realizar el objeto (ej: `hacerSonido()`).
- **Constructor**: Es el método especial que se usa para crear el objeto con valores iniciales.

💡 **Consejo**: Siempre usa `required` en los parámetros del constructor cuando el atributo es obligatorio (Dart 2.12+ con null safety).
