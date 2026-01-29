# Ejemplos de Funciones en Dart (Nivel Principiante)

Aquí tienes **2 ejemplos completos** para cada tipo de función solicitado, todos incluyen el método `main()` y son ideales para principiantes.

---

## 1. Función simple sin parámetros ni valor de retorno

### Ejemplo 1:
```dart
void main() {
  saludar();
  despedirse();
}

void saludar() {
  print('¡Hola! Bienvenido al programa.');
}

void despedirse() {
  print('¡Adiós! Gracias por usar el programa.');
}
```

### Ejemplo 2:
```dart
void main() {
  mostrarMenu();
  print('---');
  mostrarInstrucciones();
}

void mostrarMenu() {
  print('Menú Principal');
  print('1. Opción A');
  print('2. Opción B');
}

void mostrarInstrucciones() {
  print('Selecciona una opción del menú');
}
```

---

## 2. Función con parámetros posicionales sin retorno

### Ejemplo 1:
```dart
void main() {
  imprimirSuma(5, 3);
  imprimirSuma(10, 20);
}

void imprimirSuma(int a, int b) {
  int resultado = a + b;
  print('La suma de $a + $b es: $resultado');
}
```

### Ejemplo 2:
```dart
void main() {
  saludarPersona('Ana', 25);
  saludarPersona('Carlos', 30);
}

void saludarPersona(String nombre, int edad) {
  print('Hola $nombre, tienes $edad años.');
}
```

---

## 3. Función con parámetros con nombre

### Ejemplo 1:
```dart
void main() {
  crearUsuario(nombre: 'María', edad: 28);
  crearUsuario(nombre: 'Juan', edad: 35, ciudad: 'Madrid');
}

void crearUsuario({required String nombre, required int edad, String ciudad = 'Desconocida'}) {
  print('Usuario creado:');
  print('- Nombre: $nombre');
  print('- Edad: $edad');
  print('- Ciudad: $ciudad');
}
```

### Ejemplo 2:
```dart
void main() {
  configurarApp(idioma: 'es', modoOscuro: true);
  print('---');
  configurarApp(idioma: 'en'); // modoOscuro usará valor por defecto
}

void configurarApp({required String idioma, bool modoOscuro = false}) {
  print('Configuración:');
  print('- Idioma: $idioma');
  print('- Modo oscuro: ${modoOscuro ? 'Activado' : 'Desactivado'}');
}
```

---

## 4. Función con parámetros posicionales con retorno

### Ejemplo 1:
```dart
void main() {
  int resultado1 = sumar(4, 6);
  print('El resultado es: $resultado1');
  
  int resultado2 = sumar(15, 25);
  print('El resultado es: $resultado2');
}

int sumar(int a, int b) {
  return a + b;
}
```

### Ejemplo 2:
```dart
void main() {
  double area1 = calcularAreaRectangulo(5, 3);
  print('El área es: $area1 metros cuadrados');
  
  double area2 = calcularAreaRectangulo(10, 4);
  print('El área es: $area2 metros cuadrados');
}

double calcularAreaRectangulo(double ancho, double alto) {
  return ancho * alto;
}
```

---

## 5. Función flecha (Arrow Function)

### Ejemplo 1:
```dart
void main() {
  int resultado = duplicar(7);
  print('El doble de 7 es: $resultado');
  
  int otroResultado = duplicar(12);
  print('El doble de 12 es: $otroResultado');
}

int duplicar(int numero) => numero * 2;
```

### Ejemplo 2:
```dart
void main() {
  String mensaje1 = saludar('Sofía');
  print(mensaje1);
  
  String mensaje2 = saludar('Luis');
  print(mensaje2);
}

String saludar(String nombre) => '¡Hola $nombre! ¿Cómo estás?';
```

---

## 6. Función anónima

### Ejemplo 1:
```dart
void main() {
  // Asignamos una función anónima a una variable
  var saludar = (String nombre) {
    print('Hola $nombre, buenos días');
  };
  
  // Usamos la función
  saludar('Pedro');
  saludar('Laura');
}
```

### Ejemplo 2:
```dart
void main() {
  // Lista de números
  List<int> numeros = [1, 2, 3, 4, 5];
  
  // Usamos una función anónima con forEach
  print('Números originales:');
  numeros.forEach((numero) {
    print(numero);
  });
  
  print('\nNúmeros al cuadrado:');
  numeros.forEach((numero) {
    print(numero * numero);
  });
}
```

---

## 📌 Resumen Visual para Principiantes

| Tipo de función | Sintaxis clave | ¿Retorna valor? |
|-----------------|----------------|-----------------|
| Sin parámetros | `void funcion()` | ❌ No |
| Parámetros posicionales | `void funcion(int a, String b)` | ❌ No |
| Parámetros con nombre | `void funcion({String nombre})` | ❌ No |
| Con retorno | `int funcion(int a) { return a; }` | ✅ Sí |
| Flecha | `int funcion(int a) => a * 2;` | ✅ Sí (una línea) |
| Anónima | `var f = (x) { print(x); };` | ✅/❌ Opcional |

💡 **Consejo para principiantes**: 
- Usa `void` cuando la función **no retorna** nada.
- Usa `=>` solo para funciones de **una sola línea**.
- Los parámetros con nombre siempre van entre **llaves `{}`** y son opcionales a menos que uses `required`.
