# Módulo 4: Colecciones (Manejo de Datos)
## Cómo manipular grupos de información

---

## 1. Listas (Lists)

### Ejemplo 1: Creación e indexación básica
```dart
void main() {
  // Creación de listas de diferentes formas
  List<String> nombres = ["Ana", "Carlos", "María"];
  var numeros = <int>[1, 2, 3, 4, 5];
  List<double> notas = List.empty(growable: true); // Lista vacía que puede crecer
  
  // Indexación (acceso por posición)
  print("Primer nombre: ${nombres[0]}"); // Ana
  print("Último número: ${numeros[4]}"); // 5
  
  // Modificar un elemento por índice
  nombres[1] = "Carlos Alberto";
  print("Nombres actualizados: $nombres");
}
```

### Ejemplo 2: Métodos comunes de listas
```dart
void main() {
  List<String> tareas = ["Estudiar Dart", "Hacer ejercicio"];
  
  // add() - Agregar elementos al final
  tareas.add("Leer un libro");
  print("Después de add: $tareas");
  
  // addAll() - Agregar múltiples elementos
  tareas.addAll(["Comprar víveres", "Llamar a mamá"]);
  print("Después de addAll: $tareas");
  
  // insert() - Insertar en posición específica
  tareas.insert(0, "Desayunar"); // Inserta al inicio
  print("Después de insert: $tareas");
  
  // remove() - Eliminar por valor
  tareas.remove("Hacer ejercicio");
  print("Después de remove: $tareas");
  
  // removeAt() - Eliminar por índice
  tareas.removeAt(2);
  print("Después de removeAt: $tareas");
  
  // length - Obtener tamaño
  print("Total de tareas: ${tareas.length}");
  
  // isEmpty / isNotEmpty
  print("¿Lista vacía? ${tareas.isEmpty}");
  print("¿Lista con elementos? ${tareas.isNotEmpty}");
}
```

### Ejemplo 3: Más métodos útiles
```dart
void main() {
  List<int> puntajes = [85, 90, 78, 92, 88, 90, 85];
  
  // indexOf() - Encontrar posición
  int posicion = puntajes.indexOf(92);
  print("El 92 está en posición: $posicion");
  
  // contains() - Verificar si existe
  print("¿Hay algún 100? ${puntajes.contains(100)}");
  print("¿Hay algún 90? ${puntajes.contains(90)}");
  
  // sort() - Ordenar
  puntajes.sort();
  print("Puntajes ordenados: $puntajes");
  
  // reversed - Invertir orden
  var invertidos = puntajes.reversed;
  print("Puntajes invertidos: ${invertidos.toList()}");
  
  // sublist() - Obtener parte de la lista
  var primeros3 = puntajes.sublist(0, 3);
  print("Primeros 3: $primeros3");
  
  // clear() - Vaciar lista
  puntajes.clear();
  print("Lista después de clear: $puntajes (tamaño: ${puntajes.length})");
}
```

### Ejemplo 4: Iteración con for-in
```dart
void main() {
  List<String> materias = ["Matemáticas", "Historia", "Programación", "Química", "Inglés"];
  
  // Iteración básica con for-in
  print("=== Materias del semestre ===");
  for (var materia in materias) {
    print("- $materia");
  }
  
  // Iteración con índice usando for-in y asMap()
  print("\n=== Materias con índice ===");
  for (var entrada in materias.asMap().entries) {
    print("${entrada.key + 1}. ${entrada.value}");
  }
  
  // Iteración con condición
  print("\n=== Materias que contienen 'a' ===");
  for (var materia in materias) {
    if (materia.toLowerCase().contains('a')) {
      print("✓ $materia");
    }
  }
}
```

### Ejemplo 5: Listas de objetos complejos
```dart
void main() {
  // Lista de Mapas (objetos)
  List<Map<String, dynamic>> estudiantes = [
    {"nombre": "Juan", "edad": 16, "promedio": 8.5},
    {"nombre": "María", "edad": 17, "promedio": 9.2},
    {"nombre": "Carlos", "edad": 16, "promedio": 7.8},
    {"nombre": "Ana", "edad": 18, "promedio": 9.8},
  ];
  
  // Iterar lista de objetos
  print("=== Lista de Estudiantes ===");
  for (var estudiante in estudiantes) {
    print("${estudiante['nombre']} - Edad: ${estudiante['edad']} - Prom: ${estudiante['promedio']}");
  }
  
  // Buscar elementos específicos
  print("\n=== Estudiantes con promedio > 9 ===");
  for (var estudiante in estudiantes) {
    if (estudiante['promedio'] > 9.0) {
      print("🌟 ${estudiante['nombre']}: ${estudiante['promedio']}");
    }
  }
}
```

---

## 2. Mapas (Maps)

### Ejemplo 1: Creación y estructura Clave-Valor
```dart
void main() {
  // Diferentes formas de crear Mapas
  
  // Método 1: Literal de mapa (recomendado)
  Map<String, dynamic> estudiante = {
    "nombre": "Carlos Pérez",
    "edad": 17,
    "grado": "11°",
    "activo": true,
    "materias": ["Matemáticas", "Física"]
  };
  
  // Método 2: Constructor
  Map<String, int> calificaciones = Map();
  calificaciones["Matemáticas"] = 85;
  calificaciones["Historia"] = 92;
  
  // Método 3: Con tipo explícito
  var configuracion = <String, String>{
    "idioma": "español",
    "tema": "oscuro",
    "notificaciones": "activadas"
  };
  
  print("Estudiante: $estudiante");
  print("Calificaciones: $calificaciones");
  print("Configuración: $configuracion");
  
  // Acceso a valores
  print("\n=== Acceso a datos ===");
  print("Nombre del estudiante: ${estudiante['nombre']}");
  print("Primera materia: ${estudiante['materias'][0]}");
}
```

### Ejemplo 2: Acceso y manipulación de Mapas
```dart
void main() {
  Map<String, dynamic> producto = {
    "id": "P001",
    "nombre": "Laptop Gamer",
    "precio": 1200.50,
    "stock": 15,
    "categorias": ["Tecnología", "Computación"]
  };
  
  // Acceder valores
  print("Producto: ${producto['nombre']}");
  print("Precio: \$${producto['precio']}");
  print("Stock disponible: ${producto['stock']} unidades");
  
  // Modificar valores
  producto['precio'] = 1150.99;
  producto['stock'] = producto['stock'] - 3; // Vendimos 3 unidades
  producto['descuento'] = 0.15; // Agregar nueva clave
  
  print("\n=== Después de modificaciones ===");
  print("Nuevo precio: \$${producto['precio']}");
  print("Nuevo stock: ${producto['stock']}");
  print("Descuento: ${producto['descuento'] * 100}%");
  
  // Verificar si existe una clave
  print("\n=== Verificación de claves ===");
  print("¿Tiene 'nombre'? ${producto.containsKey('nombre')}");
  print("¿Tiene 'garantia'? ${producto.containsKey('garantia')}");
}
```

### Ejemplo 3: Métodos comunes de Mapas
```dart
void main() {
  Map<String, int> inventario = {
    "manzanas": 50,
    "naranjas": 30,
    "plátanos": 25,
    "uvas": 40
  };
  
  // Obtener todas las claves
  print("Productos disponibles:");
  for (var producto in inventario.keys) {
    print("- $producto");
  }
  
  // Obtener todos los valores
  print("\nCantidades disponibles:");
  for (var cantidad in inventario.values) {
    print("- $cantidad unidades");
  }
  
  // Recorrer clave-valor juntos
  print("\n=== Inventario completo ===");
  inventario.forEach((producto, cantidad) {
    print("$producto: $cantidad unidades");
  });
  
  // Actualizar un valor con función
  inventario.update("manzanas", (valor) => valor + 10);
  print("\nManzanas después de reabastecer: ${inventario['manzanas']}");
  
  // Eliminar elementos
  inventario.remove("uvas");
  print("\nInventario sin uvas: $inventario");
  
  // Limpiar todo el mapa
  inventario.clear();
  print("Inventario después de clear: $inventario");
}
```

### Ejemplo 4: Mapas anidados y complejos
```dart
void main() {
  // Mapa de mapas (diccionario de estudiantes)
  Map<String, Map<String, dynamic>> sistemaEscolar = {
    "A001": {
      "nombre": "María González",
      "edad": 16,
      "calificaciones": [8.5, 9.0, 8.0],
      "contacto": {"telefono": "555-1234", "email": "maria@email.com"}
    },
    "A002": {
      "nombre": "Juan Rodríguez",
      "edad": 17,
      "calificaciones": [7.5, 8.5, 9.5],
      "contacto": {"telefono": "555-5678", "email": "juan@email.com"}
    },
    "A003": {
      "nombre": "Ana Martínez",
      "edad": 16,
      "calificaciones": [9.0, 9.5, 10.0],
      "contacto": {"telefono": "555-9012", "email": "ana@email.com"}
    }
  };
  
  // Acceso a datos anidados
  print("=== Sistema Escolar ===");
  sistemaEscolar.forEach((matricula, datos) {
    print("\nMatrícula: $matricula");
    print("Nombre: ${datos['nombre']}");
    print("Edad: ${datos['edad']}");
    print("Promedio: ${_calcularPromedio(datos['calificaciones'])}");
    print("Teléfono: ${datos['contacto']['telefono']}");
  });
  
  // Buscar estudiante por matrícula
  String buscarMatricula = "A002";
  if (sistemaEscolar.containsKey(buscarMatricula)) {
    print("\n=== Estudiante encontrado ===");
    var estudiante = sistemaEscolar[buscarMatricula];
    print("Nombre: ${estudiante!['nombre']}");
    print("Email: ${estudiante['contacto']['email']}");
  }
}

double _calcularPromedio(List<dynamic> calificaciones) {
  double suma = 0;
  for (var calif in calificaciones) {
    suma += calif;
  }
  return suma / calificaciones.length;
}
```

### Ejemplo 5: Operaciones avanzadas con Mapas
```dart
void main() {
  Map<String, double> ventasDiarias = {
    "Lunes": 1250.75,
    "Martes": 980.50,
    "Miércoles": 1575.25,
    "Jueves": 1120.00,
    "Viernes": 2100.50,
    "Sábado": 1850.75,
    "Domingo": 950.25
  };
  
  // Calcular total de ventas
  double totalVentas = 0;
  ventasDiarias.forEach((dia, venta) {
    totalVentas += venta;
  });
  print("Total de ventas semanales: \$${totalVentas.toStringAsFixed(2)}");
  
  // Encontrar día con más ventas
  String diaTop = "";
  double maxVenta = 0;
  
  ventasDiarias.forEach((dia, venta) {
    if (venta > maxVenta) {
      maxVenta = venta;
      diaTop = dia;
    }
  });
  print("Día con más ventas: $diaTop (\$${maxVenta.toStringAsFixed(2)})");
  
  // Filtrar días con ventas > 1500
  print("\n=== Días destacados (ventas > \$1500) ===");
  var diasDestacados = ventasDiarias.entries.where((entry) => entry.value > 1500);
  for (var dia in diasDestacados) {
    print("${dia.key}: \$${dia.value.toStringAsFixed(2)}");
  }
  
  // Crear nuevo mapa con descuento aplicado
  print("\n=== Precios con 20% de descuento ===");
  Map<String, double> ventasConDescuento = {};
  ventasDiarias.forEach((dia, venta) {
    ventasConDescuento[dia] = venta * 0.8;
  });
  
  ventasConDescuento.forEach((dia, venta) {
    print("$dia: \$${venta.toStringAsFixed(2)} (original: \$${ventasDiarias[dia]!.toStringAsFixed(2)})");
  });
}
```

---

## 3. Sets: Colecciones de elementos únicos

### Ejemplo 1: Creación y propiedades básicas
```dart
void main() {
  // Creación de Sets
  Set<String> nombresEstudiantes = {"Ana", "Carlos", "María", "Ana", "Carlos"};
  Set<int> numerosUnicos = {1, 2, 3, 4, 5, 5, 5, 5};
  var colores = <String>{"rojo", "azul", "verde", "rojo", "azul"};
  
  print("Nombres estudiantes: $nombresEstudiantes");
  print("Números únicos: $numerosUnicos");
  print("Colores: $colores");
  
  // Los Sets automáticamente eliminan duplicados
  print("\n=== Propiedades ===");
  print("Tamaño del set de nombres: ${nombresEstudiantes.length}");
  print("¿Contiene 'Ana'? ${nombresEstudiantes.contains('Ana')}");
  print("¿Está vacío? ${nombresEstudiantes.isEmpty}");
  
  // Convertir Lista a Set (para eliminar duplicados)
  List<int> numerosConDuplicados = [1, 2, 2, 3, 3, 3, 4, 4, 4, 4];
  Set<int> numerosSinDuplicados = numerosConDuplicados.toSet();
  print("\nLista original: $numerosConDuplicados");
  print("Set sin duplicados: $numerosSinDuplicados");
}
```

### Ejemplo 2: Métodos comunes de Sets
```dart
void main() {
  Set<String> materiasCursadas = {"Matemáticas", "Historia", "Programación"};
  
  // add() - Agregar elementos
  materiasCursadas.add("Química");
  materiasCursadas.add("Programación"); // No se agregará (duplicado)
  print("Después de add: $materiasCursadas");
  
  // addAll() - Agregar múltiples
  materiasCursadas.addAll({"Inglés", "Física", "Matemáticas"});
  print("Después de addAll: $materiasCursadas");
  
  // remove() - Eliminar elemento
  materiasCursadas.remove("Historia");
  print("Después de remove: $materiasCursadas");
  
  // contains() - Verificar existencia
  print("\n=== Verificaciones ===");
  print("¿Cursa Programación? ${materiasCursadas.contains('Programación')}");
  print("¿Cursa Biología? ${materiasCursadas.contains('Biología')}");
  
  // Iteración
  print("\n=== Materias cursadas ===");
  int contador = 1;
  for (var materia in materiasCursadas) {
    print("$contador. $materia");
    contador++;
  }
  
  // Convertir a Lista
  List<String> listaMaterias = materiasCursadas.toList();
  listaMaterias.sort();
  print("\nMaterias ordenadas: $listaMaterias");
}
```

### Ejemplo 3: Operaciones entre Sets
```dart
void main() {
  Set<String> materiasPrimerSemestre = {"Matemáticas", "Historia", "Programación", "Inglés"};
  Set<String> materiasSegundoSemestre = {"Programación", "Física", "Química", "Inglés"};
  
  print("Primer semestre: $materiasPrimerSemestre");
  print("Segundo semestre: $materiasSegundoSemestre");
  
  // Unión (todos los elementos de ambos)
  Set<String> todasMaterias = materiasPrimerSemestre.union(materiasSegundoSemestre);
  print("\nUnión (todas las materias): $todasMaterias");
  
  // Intersección (elementos comunes)
  Set<String> materiasComunes = materiasPrimerSemestre.intersection(materiasSegundoSemestre);
  print("Intersección (materias comunes): $materiasComunes");
  
  // Diferencia (elementos en A pero no en B)
  Set<String> soloPrimerSemestre = materiasPrimerSemestre.difference(materiasSegundoSemestre);
  print("Diferencia (solo primer semestre): $soloPrimerSemestre");
  
  // Diferencia (elementos en B pero no en A)
  Set<String> soloSegundoSemestre = materiasSegundoSemestre.difference(materiasPrimerSemestre);
  print("Diferencia (solo segundo semestre): $soloSegundoSemestre");
  
  // Verificar subconjunto
  Set<String> materiasBasicas = {"Matemáticas", "Inglés"};
  print("\n¿Basicas es subconjunto de primer semestre? ${materiasBasicas.isSubsetOf(materiasPrimerSemestre)}");
  print("¿Primer semestre contiene a básicas? ${materiasPrimerSemestre.containsAll(materiasBasicas)}");
}
```

### Ejemplo 4: Sets con objetos complejos
```dart
void main() {
  // Set con objetos (usando Map para simular objetos)
  Set<Map<String, dynamic>> productosUnicos = {
    {"id": 1, "nombre": "Laptop", "precio": 1000},
    {"id": 2, "nombre": "Mouse", "precio": 25},
    {"id": 1, "nombre": "Laptop", "precio": 1000}, // Duplicado (mismo id)
    {"id": 3, "nombre": "Teclado", "precio": 50},
  };
  
  print("Productos únicos: ${productosUnicos.length} elementos");
  for (var producto in productosUnicos) {
    print("ID: ${producto['id']}, Nombre: ${producto['nombre']}, Precio: \$${producto['precio']}");
  }
  
  // Ejemplo práctico: Sistema de votación sin duplicados
  print("\n=== Sistema de Votación ===");
  Set<String> votantesRegistrados = {"A001", "A002", "A003", "A004"};
  Set<String> votantesQueYaVotaron = {};
  
  // Simulación de votos
  List<String> intentosVoto = ["A001", "A002", "A001", "A003", "A005", "A002"];
  
  for (var voto in intentosVoto) {
    if (votantesRegistrados.contains(voto)) {
      if (votantesQueYaVotaron.add(voto)) {
        print("Voto aceptado para: $voto");
      } else {
        print("Voto rechazado: $voto ya votó");
      }
    } else {
      print("Voto inválido: $voto no está registrado");
    }
  }
  
  print("\nTotal votantes registrados: ${votantesRegistrados.length}");
  print("Total que ya votaron: ${votantesQueYaVotaron.length}");
  print("Faltan por votar: ${votantesRegistrados.difference(votantesQueYaVotaron)}");
}
```

### Ejemplo 5: Aplicación real con Sets
```dart
void main() {
  // Sistema de etiquetas para artículos de blog
  Set<String> etiquetasDisponibles = {
    "programación", "dart", "flutter", "tutorial", 
    "beginners", "mobile", "web", "backend"
  };
  
  // Artículos con sus etiquetas
  Map<String, Set<String>> articulos = {
    "Introducción a Dart": {"dart", "programación", "beginners"},
    "Flutter para móvil": {"flutter", "mobile", "tutorial"},
    "Backend con Dart": {"dart", "backend", "programación"},
    "Web con Flutter": {"flutter", "web", "tutorial"},
  };
  
  // Mostrar artículos por etiqueta
  print("=== Artículos por etiqueta ===");
  for (var etiqueta in etiquetasDisponibles) {
    Set<String> articulosConEtiqueta = {};
    
    articulos.forEach((titulo, etiquetasArt) {
      if (etiquetasArt.contains(etiqueta)) {
        articulosConEtiqueta.add(titulo);
      }
    });
    
    if (articulosConEtiqueta.isNotEmpty) {
      print("\n$etiqueta:");
      for (var articulo in articulosConEtiqueta) {
        print("  • $articulo");
      }
    }
  }
  
  // Encontrar artículos relacionados (comparten etiquetas)
  print("\n=== Artículos relacionados ===");
  String articuloBuscado = "Introducción a Dart";
  Set<String> etiquetasBuscado = articulos[articuloBuscado]!;
  
  print("Artículos relacionados con '$articuloBuscado':");
  articulos.forEach((titulo, etiquetasArt) {
    if (titulo != articuloBuscado) {
      Set<String> etiquetasComunes = etiquetasBuscado.intersection(etiquetasArt);
      if (etiquetasComunes.isNotEmpty) {
        print("  • $titulo (etiquetas comunes: $etiquetasComunes)");
      }
    }
  });
}
```

---

## 4. Métodos funcionales básicos

### Ejemplo 1: Introducción a .map()
```dart
void main() {
  List<int> numeros = [1, 2, 3, 4, 5];
  
  // .map() transforma cada elemento
  print("=== Ejemplo básico de .map() ===");
  
  // Transformar números a sus cuadrados
  var cuadrados = numeros.map((numero) {
    return numero * numero;
  });
  print("Cuadrados: ${cuadrados.toList()}");
  
  // Versión con arrow function
  var cubos = numeros.map((n) => n * n * n);
  print("Cubos: ${cubos.toList()}");
  
  // Transformar números a strings
  var strings = numeros.map((n) => "Número: $n");
  print("Strings: ${strings.toList()}");
  
  // Ejemplo práctico: Aplicar descuento
  List<double> precios = [100.0, 200.0, 300.0, 400.0];
  double descuento = 0.20; // 20%
  
  var preciosConDescuento = precios.map((precio) => precio * (1 - descuento));
  print("\nPrecios originales: $precios");
  print("Precios con 20% descuento: ${preciosConDescuento.toList()}");
}
```

### Ejemplo 2: Más usos de .map()
```dart
void main() {
  List<Map<String, dynamic>> estudiantes = [
    {"nombre": "Ana", "edad": 16, "promedio": 8.5},
    {"nombre": "Carlos", "edad": 17, "promedio": 7.8},
    {"nombre": "María", "edad": 16, "promedio": 9.2},
    {"nombre": "Juan", "edad": 18, "promedio": 8.0},
  ];
  
  // Extraer solo los nombres
  var nombres = estudiantes.map((est) => est["nombre"]).toList();
  print("Nombres: $nombres");
  
  // Crear lista de strings con información formateada
  var infoEstudiantes = estudiantes.map((est) {
    return "${est['nombre']} (${est['edad']} años) - Prom: ${est['promedio']}";
  }).toList();
  
  print("\nInformación de estudiantes:");
  for (var info in infoEstudiantes) {
    print("- $info");
  }
  
  // Transformar datos numéricos
  var edadesEnMeses = estudiantes.map((est) => est["edad"] * 12).toList();
  print("\nEdades en meses: $edadesEnMeses");
  
  // Ejemplo con índice
  print("\nEstudiantes numerados:");
  var numerados = estudiantes.asMap().entries.map((entry) {
    int idx = entry.key + 1;
    var est = entry.value;
    return "$idx. ${est['nombre']}";
  }).toList();
  
  for (var item in numerados) {
    print(item);
  }
}
```

### Ejemplo 3: Introducción a .where() para filtrado
```dart
void main() {
  List<int> edades = [15, 22, 12, 30, 17, 25, 16, 18, 14];
  
  // Filtrar mayores de edad (>= 18)
  var mayores = edades.where((edad) => edad >= 18).toList();
  print("Mayores de edad: $mayores");
  
  // Filtrar menores de edad
  var menores = edades.where((edad) => edad < 18).toList();
  print("Menores de edad: $menores");
  
  // Filtrar edades pares
  var edadesPares = edades.where((edad) => edad % 2 == 0).toList();
  print("Edades pares: $edadesPares");
  
  // Ejemplo práctico: Sistema de calificaciones
  List<double> calificaciones = [6.5, 8.0, 5.0, 9.5, 7.0, 10.0, 4.5, 8.5];
  
  var aprobados = calificaciones.where((calif) => calif >= 7.0).toList();
  var excelencia = calificaciones.where((calif) => calif >= 9.0).toList();
  
  print("\nCalificaciones: $calificaciones");
  print("Aprobados (>=7.0): $aprobados");
  print("Excelencia (>=9.0): $excelencia");
  print("Cantidad de aprobados: ${aprobados.length}");
}
```

### Ejemplo 4: .where() con objetos complejos
```dart
void main() {
  List<Map<String, dynamic>> productos = [
    {"nombre": "Laptop", "precio": 1200.0, "stock": 5, "categoria": "electrónica"},
    {"nombre": "Mouse", "precio": 25.0, "stock": 20, "categoria": "electrónica"},
    {"nombre": "Libro", "precio": 15.0, "stock": 0, "categoria": "libros"},
    {"nombre": "Silla", "precio": 150.0, "stock": 3, "categoria": "muebles"},
    {"nombre": "Tablet", "precio": 300.0, "stock": 8, "categoria": "electrónica"},
    {"nombre": "Lámpara", "precio": 45.0, "stock": 0, "categoria": "hogar"},
  ];
  
  // Productos en stock
  var enStock = productos.where((p) => p["stock"] > 0).toList();
  print("=== Productos en stock ===");
  for (var p in enStock) {
    print("${p['nombre']} - \$${p['precio']} (${p['stock']} unidades)");
  }
  
  // Productos electrónicos
  var electronicos = productos.where((p) => p["categoria"] == "electrónica").toList();
  print("\n=== Productos electrónicos ===");
  for (var p in electronicos) {
    print("${p['nombre']} - \$${p['precio']}");
  }
  
  // Productos baratos (< 50)
  var baratos = productos.where((p) => p["precio"] < 50.0).toList();
  print("\n=== Productos baratos (< \$50) ===");
  for (var p in baratos) {
    print("${p['nombre']} - \$${p['precio']}");
  }
  
  // Combinar condiciones
  var electronicosEnStock = productos.where((p) {
    return p["categoria"] == "electrónica" && p["stock"] > 0;
  }).toList();
  
  print("\n=== Electrónicos disponibles ===");
  for (var p in electronicosEnStock) {
    print("${p['nombre']} - \$${p['precio']} (${p['stock']} unidades)");
  }
}
```

### Ejemplo 5: Combinación de .map() y .where()
```dart
void main() {
  List<Map<String, dynamic>> empleados = [
    {"nombre": "Ana", "departamento": "Ventas", "salario": 25000, "antiguedad": 2},
    {"nombre": "Carlos", "departamento": "TI", "salario": 35000, "antiguedad": 5},
    {"nombre": "María", "departamento": "Ventas", "salario": 28000, "antiguedad": 3},
    {"nombre": "Juan", "departamento": "RH", "salario": 22000, "antiguedad": 1},
    {"nombre": "Laura", "departamento": "TI", "salario": 40000, "antiguedad": 7},
    {"nombre": "Pedro", "departamento": "Ventas", "salario": 24000, "antiguedad": 2},
  ];
  
  // 1. Empleados de TI con salario > 30000
  print("=== Empleados de TI con salario > \$30,000 ===");
  var tiAltos = empleados
      .where((emp) => emp["departamento"] == "TI" && emp["salario"] > 30000)
      .map((emp) => "${emp['nombre']}: \$${emp['salario']}")
      .toList();
  
  for (var emp in tiAltos) {
    print(emp);
  }
  
  // 2. Aumento del 10% a empleados con antigüedad > 2 años
  print("\n=== Salarios con aumento del 10% (antigüedad > 2 años) ===");
  var conAumento = empleados
      .where((emp) => emp["antiguedad"] > 2)
      .map((emp) {
        double nuevoSalario = emp["salario"] * 1.10;
        return {
          "nombre": emp["nombre"],
          "salario_anterior": emp["salario"],
          "salario_nuevo": nuevoSalario,
          "aumento": nuevoSalario - emp["salario"]
        };
      })
      .toList();
  
  for (var emp in conAumento) {
    print("${emp['nombre']}: \$${emp['salario_anterior']} -> \$${emp['salario_nuevo'].toStringAsFixed(2)} (+ \$${emp['aumento'].toStringAsFixed(2)})");
  }
  
  // 3. Resumen por departamento
  print("\n=== Resumen por departamento ===");
  
  // Obtener departamentos únicos
  var departamentos = empleados
      .map((emp) => emp["departamento"])
      .toSet()
      .toList();
  
  for (var depto in departamentos) {
    // Empleados del departamento
    var empsDepto = empleados.where((emp) => emp["departamento"] == depto);
    
    // Calcular promedio de salario
    double totalSalario = 0;
    for (var emp in empsDepto) {
      totalSalario += emp["salario"];
    }
    double promedio = totalSalario / empsDepto.length;
    
    print("$depto: ${empsDepto.length} empleados, Salario promedio: \$${promedio.toStringAsFixed(2)}");
  }
  
  // 4. Top 3 salarios más altos
  print("\n=== Top 3 salarios más altos ===");
  var top3 = empleados
      .map((emp) => {"nombre": emp["nombre"], "salario": emp["salario"]})
      .toList()
      ..sort((a, b) => b["salario"].compareTo(a["salario"]))
      .sublist(0, 3);
  
  for (var i = 0; i < top3.length; i++) {
    print("${i + 1}. ${top3[i]['nombre']}: \$${top3[i]['salario']}");
  }
}
```

### Ejemplo adicional: Flujo completo con .toList()
```dart
void main() {
  // Ejemplo completo: Procesamiento de datos
  List<int> numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
  
  // Pipeline de procesamiento
  var resultado = numeros
      .where((n) => n %
