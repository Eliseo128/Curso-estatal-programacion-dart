# Módulo 3: Funciones y organización del código
## Propósito: Fomentar la reutilización y estructuración del programa

---

## 1. Definición de funciones y valores de retorno

### Ejemplo 1: Función básica con retorno
```dart
void main() {
  // Llamando a la función
  double resultado = calcularIMC(65.0, 1.70);
  print("IMC calculado: ${resultado.toStringAsFixed(2)}");
  
  // Usando el retorno directamente
  print("Clasificación: ${clasificarIMC(calcularIMC(65.0, 1.70))}");
}

/**
 * Calcula el Índice de Masa Corporal (IMC)
 * @param peso en kilogramos
 * @param altura en metros
 * @return IMC calculado
 */
double calcularIMC(double peso, double altura) {
  // La función realiza el cálculo y RETORNA el resultado
  double imc = peso / (altura * altura);
  return imc; // 'return' envía el valor al lugar donde se llamó la función
}

/**
 * Clasifica el IMC según valores estándar
 * @param imc valor del IMC
 * @return clasificación como String
 */
String clasificarIMC(double imc) {
  if (imc < 18.5) {
    return "Bajo peso";
  } else if (imc < 25) {
    return "Peso normal";
  } else if (imc < 30) {
    return "Sobrepeso";
  } else {
    return "Obesidad";
  }
}
```

### Ejemplo 2: Función con múltiples retornos (usando una colección)
```dart
void main() {
  // La función retorna una lista con múltiples valores
  List<dynamic> resultados = calcularEstadisticas([85, 90, 78, 92, 88]);
  
  // Accediendo a los valores retornados
  print("Promedio: ${resultados[0]}");
  print("Calificación más alta: ${resultados[1]}");
  print("Calificación más baja: ${resultados[2]}");
  
  // Alternativa: usando desestructuración
  var [promedio, maximo, minimo] = calcularEstadisticas([85, 90, 78, 92, 88]);
  print("\nDesestructurando:");
  print("Promedio: $promedio");
  print("Máximo: $maximo");
  print("Mínimo: $minimo");
}

/**
 * Calcula estadísticas básicas de una lista de calificaciones
 * @param calificaciones lista de números
 * @return Lista con [promedio, máximo, mínimo]
 */
List<dynamic> calcularEstadisticas(List<int> calificaciones) {
  if (calificaciones.isEmpty) {
    return [0, 0, 0]; // Retorna valores por defecto
  }
  
  int suma = 0;
  int maximo = calificaciones[0];
  int minimo = calificaciones[0];
  
  for (int calif in calificaciones) {
    suma += calif;
    if (calif > maximo) maximo = calif;
    if (calif < minimo) minimo = calif;
  }
  
  double promedio = suma / calificaciones.length;
  
  // Retornando múltiples valores en una lista
  return [promedio, maximo, minimo];
}
```

### Ejemplo 3: Función sin retorno (void)
```dart
void main() {
  // Funciones void no retornan valores
  mostrarMenu();
  
  imprimirTablaMultiplicar(5);
  
  saludarUsuario("Carlos");
}

/**
 * Función void: No retorna ningún valor, solo ejecuta acciones
 * Útil para mostrar información o realizar efectos secundarios
 */
void mostrarMenu() {
  print("""
  === MENÚ PRINCIPAL ===
  1. Jugar
  2. Configuración
  3. Puntajes altos
  4. Salir
  """);
}

/**
 * Muestra la tabla de multiplicar de un número
 * @param numero del cual mostrar la tabla
 */
void imprimirTablaMultiplicar(int numero) {
  print("=== Tabla del $numero ===");
  for (int i = 1; i <= 10; i++) {
    print("$numero x $i = ${numero * i}");
  }
}

/**
 * Saluda a un usuario
 * @param nombre del usuario a saludar
 */
void saludarUsuario(String nombre) {
  // Esta función realiza una acción (imprimir) pero no calcula nada
  print("¡Hola, $nombre! Bienvenido al sistema.");
  print("Hoy es ${DateTime.now().toString().substring(0, 10)}");
}
```

---

## 2. Parámetros posicionales obligatorios

### Ejemplo 1: Parámetros posicionales básicos
```dart
void main() {
  // Los parámetros se pasan en el ORDEN definido
  double area = calcularAreaRectangulo(5.0, 3.0);
  print("Área del rectángulo: $area m²");
  
  // El orden ES IMPORTANTE
  double areaIncorrecta = calcularAreaRectangulo(3.0, 5.0); // Mismo resultado aquí
  print("Mismo resultado si intercambiamos base y altura: $areaIncorrecta m²");
  
  // Ejemplo donde el orden SÍ importa
  String mensaje = crearMensajePersonalizado("Carlos", 16, "Aprobado");
  print("\nMensaje: $mensaje");
  
  // Si cambiamos el orden, el mensaje no tiene sentido
  String mensajeConfuso = crearMensajePersonalizado("Aprobado", 16, "Carlos");
  print("Mensaje confuso: $mensajeConfuso");
}

/**
 * Calcula el área de un rectángulo
 * PARÁMETROS POSICIONALES OBLIGATORIOS:
 * @param base debe ser el primer argumento
 * @param altura debe ser el segundo argumento
 * Ambos son OBLIGATORIOS
 */
double calcularAreaRectangulo(double base, double altura) {
  return base * altura;
}

/**
 * Crea un mensaje personalizado
 * El ORDEN de los parámetros define su significado
 */
String crearMensajePersonalizado(String nombre, int edad, String estatus) {
  return "El estudiante $nombre, de $edad años, tiene estatus: $estatus";
}
```

### Ejemplo 2: Validación en parámetros posicionales
```dart
void main() {
  // Llamadas correctas
  String resultado1 = convertirUnidades(100.0, "km", "millas");
  print("100 km = $resultado1");
  
  String resultado2 = convertirUnidades(32.0, "C", "F");
  print("32°C = $resultado2");
  
  // Llamada con parámetros en orden incorrecto
  // Esto compilará pero dará resultados erróneos
  String resultado3 = convertirUnidades("km", 100.0, "millas"); // ¡Error! tipos incorrectos
  print("Resultado erróneo: $resultado3");
}

/**
 * Convierte unidades de medida
 * Los parámetros son POSICIONALES y OBLIGATORIOS
 * @param valor cantidad a convertir
 * @param desde unidad origen
 * @param hasta unidad destino
 */
String convertirUnidades(double valor, String desde, String hasta) {
  double resultado;
  
  if (desde == "km" && hasta == "millas") {
    resultado = valor * 0.621371;
    return "${valor.toStringAsFixed(2)} km = ${resultado.toStringAsFixed(2)} millas";
  } 
  else if (desde == "C" && hasta == "F") {
    resultado = (valor * 9/5) + 32;
    return "${valor.toStringAsFixed(1)}°C = ${resultado.toStringAsFixed(1)}°F";
  }
  else {
    return "Conversión no soportada: $desde a $hasta";
  }
}

/**
 * Registra un estudiante en el sistema
 * Parámetros posicionales con validación
 */
bool registrarEstudiante(String nombreCompleto, int edad, String grado) {
  // Validación de parámetros obligatorios
  if (nombreCompleto.isEmpty) {
    print("ERROR: El nombre es obligatorio");
    return false;
  }
  
  if (edad < 15 || edad > 20) {
    print("ERROR: La edad debe estar entre 15 y 20 años");
    return false;
  }
  
  if (grado.isEmpty) {
    print("ERROR: El grado es obligatorio");
    return false;
  }
  
  // Simulación de registro
  print("✅ Estudiante registrado:");
  print("   Nombre: $nombreCompleto");
  print("   Edad: $edad años");
  print("   Grado: $grado");
  
  return true;
}
```

### Ejemplo 3: Parámetros posicionales en funciones matemáticas
```dart
void main() {
  // Funciones matemáticas clásicas con parámetros posicionales
  
  // 1. Ecuación cuadrática
  List<double> soluciones = resolverEcuacionCuadratica(1, -5, 6);
  print("Soluciones de x² - 5x + 6 = 0: $soluciones");
  
  // 2. Distancia entre dos puntos
  double distancia = calcularDistancia(0, 0, 3, 4);
  print("Distancia entre (0,0) y (3,4): $distancia");
  
  // 3. Interés compuesto
  double montoFinal = calcularInteresCompuesto(1000.0, 0.05, 3);
  print("Inversión de \$1000 al 5% por 3 años: \$${montoFinal.toStringAsFixed(2)}");
}

/**
 * Resuelve una ecuación cuadrática: ax² + bx + c = 0
 * Parámetros POSICIONALES obligatorios: a, b, c
 */
List<double> resolverEcuacionCuadratica(double a, double b, double c) {
  double discriminante = b * b - 4 * a * c;
  
  if (discriminante < 0) {
    return []; // No hay soluciones reales
  }
  
  double x1 = (-b + sqrt(discriminante)) / (2 * a);
  double x2 = (-b - sqrt(discriminante)) / (2 * a);
  
  return [x1, x2];
}

/**
 * Calcula la distancia entre dos puntos en el plano
 * Parámetros POSICIONALES: x1, y1, x2, y2
 */
double calcularDistancia(double x1, double y1, double x2, double y2) {
  double dx = x2 - x1;
  double dy = y2 - y1;
  return sqrt(dx * dx + dy * dy);
}

/**
 * Calcula el monto final con interés compuesto
 * Parámetros POSICIONALES: capital, tasa, años
 */
double calcularInteresCompuesto(double capital, double tasa, int años) {
  return capital * pow(1 + tasa, años);
}

// Función auxiliar para raíz cuadrada (simulando math.sqrt)
double sqrt(double x) => x * x;
// Función auxiliar para potencia (simulando math.pow)
double pow(double base, int exponente) {
  double resultado = 1;
  for (int i = 0; i < exponente; i++) {
    resultado *= base;
  }
  return resultado;
}
```

---

## 3. Parámetros nombrados {} y su importancia

### Ejemplo 1: Parámetros nombrados básicos
```dart
void main() {
  // PARÁMETROS NOMBRADOS: Se especifica el nombre del parámetro
  // VENTAJA: El orden no importa, solo los nombres
  
  // Crear configuración de usuario
  crearPerfilUsuario(
    nombre: "Ana García",
    edad: 17,
    esPremium: true,
  );
  
  // Podemos cambiar el orden
  crearPerfilUsuario(
    esPremium: false,
    nombre: "Carlos López",
    edad: 16,
  );
  
  // Parámetros nombrados con valores por defecto
  crearNotificacion(
    titulo: "Nueva tarea asignada",
    mensaje: "Revisa la plataforma",
  );
  
  // Podemos omitir algunos parámetros si tienen valor por defecto
  crearNotificacion(
    titulo: "Recordatorio",
  );
}

/**
 * Crea un perfil de usuario
 * Los parámetros entre {} son NOMBRADOS
 * Pueden tener valores por defecto
 */
void crearPerfilUsuario({
  required String nombre,    // 'required' hace obligatorio este parámetro
  required int edad,         // También obligatorio
  bool esPremium = false,    // Opcional con valor por defecto
  String? email,             // Opcional y nullable
}) {
  print("=== PERFIL DE USUARIO ===");
  print("Nombre: $nombre");
  print("Edad: $edad años");
  print("Premium: ${esPremium ? 'Sí' : 'No'}");
  
  if (email != null) {
    print("Email: $email");
  }
  
  print("");
}

/**
 * Crea una notificación
 * Todos los parámetros tienen valores por defecto
 * IMPORTANTE: El orden no importa al llamar la función
 */
void crearNotificacion({
  String titulo = "Sin título",
  String mensaje = "",
  String tipo = "info",
  bool urgente = false,
}) {
  String icono = "";
  
  switch (tipo) {
    case "info": icono = "ℹ️"; break;
    case "alerta": icono = "⚠️"; break;
    case "error": icono = "❌"; break;
    case "exito": icono = "✅"; break;
  }
  
  if (urgente) {
    icono = "🚨 $icono";
  }
  
  print("$icono $titulo");
  if (mensaje.isNotEmpty) {
    print("   $mensaje");
  }
}
```

### Ejemplo 2: Importancia de parámetros nombrados en configuraciones
```dart
void main() {
  // IMPORTANCIA: Claridad y prevención de errores
  
  // Configuración de conexión a base de datos
  // ¿Qué es cada valor? Con parámetros nombrados es OBVIO
  conectarABaseDeDatos(
    host: "localhost",
    puerto: 5432,
    usuario: "admin",
    contrasena: "segura123",
    nombreBD: "escolar",
  );
  
  // Configuración de juego - mucho más claro
  iniciarJuego(
    nivelDificultad: "medio",
    volumenMusica: 0.7,
    volumenEfectos: 0.8,
    pantallaCompleta: true,
    idioma: "español",
  );
  
  // Comparación: versión con parámetros posicionales sería confusa
  // iniciarJuego("medio", 0.7, 0.8, true, "español"); // ¿Qué significa cada valor?
}

/**
 * Conecta a una base de datos
 * USO DE PARÁMETROS NOMBRADOS: Hace explícito qué es cada valor
 */
void conectarABaseDeDatos({
  required String host,
  required int puerto,
  required String usuario,
  required String contrasena,
  required String nombreBD,
  int timeout = 30,
}) {
  print("🔌 Conectando a la base de datos...");
  print("   Host: $host");
  print("   Puerto: $puerto");
  print("   Usuario: $usuario");
  print("   Base de datos: $nombreBD");
  print("   Timeout: ${timeout}s");
  
  // Simulación de conexión
  print("   ✅ Conexión exitosa!\n");
}

/**
 * Inicia un juego con configuración personalizada
 * LOS PARÁMETROS NOMBRADOS SON AUTO-DOCUMENTADOS
 */
void iniciarJuego({
  String nivelDificultad = "facil",
  double volumenMusica = 1.0,
  double volumenEfectos = 1.0,
  bool pantallaCompleta = false,
  String idioma = "español",
  bool subtitulos = true,
}) {
  print("🎮 Iniciando juego...");
  print("   Dificultad: $nivelDificultad");
  print("   Volumen música: ${(volumenMusica * 100).toInt()}%");
  print("   Volumen efectos: ${(volumenEfectos * 100).toInt()}%");
  print("   Pantalla completa: ${pantallaCompleta ? 'Sí' : 'No'}");
  print("   Idioma: $idioma");
  print("   Subtítulos: ${subtitulos ? 'Activados' : 'Desactivados'}");
  
  // Cálculos basados en dificultad
  int vidas = 3;
  int tiempo = 300;
  
  switch (nivelDificultad) {
    case "facil":
      vidas = 5;
      tiempo = 600;
      break;
    case "dificil":
      vidas = 1;
      tiempo = 180;
      break;
  }
  
  print("   Vidas iniciales: $vidas");
  print("   Tiempo: ${tiempo}s\n");
}
```

### Ejemplo 3: Parámetros nombrados en APIs y constructores
```dart
void main() {
  // USO COMÚN: APIs, constructores de clases, configuración
  
  // 1. Crear producto con múltiples opciones
  Producto laptop = crearProducto(
    nombre: "Laptop Gamer",
    precio: 1200.0,
    categoria: "Electrónica",
    enStock: true,
    descuento: 0.15, // 15% de descuento
  );
  
  // 2. Enviar email - parámetros muy claros
  enviarEmail(
    destinatario: "estudiante@escuela.edu",
    asunto: "Calificaciones publicadas",
    cuerpo: "Tus calificaciones están disponibles en la plataforma.",
    adjuntos: ["calificaciones.pdf"],
    copia: "tutor@escuela.edu",
  );
  
  // 3. Constructor de clase usando parámetros nombrados
  Estudiante estudiante = Estudiante(
    nombre: "María González",
    matricula: "A2023001",
    edad: 16,
    grado: "11°",
    promedio: 9.2,
  );
  
  estudiante.mostrarInformacion();
}

/**
 * Crea un producto con parámetros nombrados
 * Ideal para APIs donde algunos parámetros son opcionales
 */
Map<String, dynamic> crearProducto({
  required String nombre,
  required double precio,
  required String categoria,
  bool enStock = true,
  double descuento = 0.0,
  List<String>? etiquetas,
}) {
  double precioFinal = precio * (1 - descuento);
  
  Map<String, dynamic> producto = {
    "nombre": nombre,
    "precio_original": precio,
    "precio_final": precioFinal,
    "categoria": categoria,
    "en_stock": enStock,
    "descuento": "${(descuento * 100).toInt()}%",
  };
  
  if (etiquetas != null && etiquetas.isNotEmpty) {
    producto["etiquetas"] = etiquetas;
  }
  
  print("📦 Producto creado: $nombre");
  print("   Precio final: \$${precioFinal.toStringAsFixed(2)}");
  
  return producto;
}

/**
 * Simula el envío de un email
 * Parámetros nombrados hacen la función más legible
 */
void enviarEmail({
  required String destinatario,
  required String asunto,
  required String cuerpo,
  String remitente = "sistema@escuela.edu",
  List<String>? adjuntos,
  String? copia,
  bool esUrgente = false,
}) {
  print("📧 ${esUrgente ? 'URGENTE: ' : ''}Enviando email...");
  print("   De: $remitente");
  print("   Para: $destinatario");
  
  if (copia != null) {
    print("   CC: $copia");
  }
  
  print("   Asunto: $asunto");
  print("   Cuerpo: ${cuerpo.substring(0, min(50, cuerpo.length))}...");
  
  if (adjuntos != null && adjuntos.isNotEmpty) {
    print("   Adjuntos: ${adjuntos.length} archivo(s)");
  }
  
  print("   ✅ Email enviado exitosamente!\n");
}

// Clase usando parámetros nombrados en constructor
class Estudiante {
  String nombre;
  String matricula;
  int edad;
  String grado;
  double promedio;
  
  // Constructor con parámetros nombrados
  Estudiante({
    required this.nombre,
    required this.matricula,
    required this.edad,
    required this.grado,
    required this.promedio,
  });
  
  void mostrarInformacion() {
    print("👨‍🎓 Estudiante: $nombre");
    print("   Matrícula: $matricula");
    print("   Edad: $edad años");
    print("   Grado: $grado");
    print("   Promedio: $promedio\n");
  }
}

int min(int a, int b) => a < b ? a : b;
```

---

## 4. Parámetros opcionales []

### Ejemplo 1: Parámetros opcionales posicionales básicos
```dart
void main() {
  // PARÁMETROS OPCIONALES POSICIONALES: Se definen entre []
  // Se pasan en orden, pero pueden omitirse
  
  // Saludo completo
  saludar("Carlos", "Gómez");
  
  // Solo nombre (apellido usa valor por defecto)
  saludar("Ana");
  
  // Con título personalizado
  saludar("Dr.", "Juan", "Pérez");
  
  // Cálculo con parámetros opcionales
  double total1 = calcularTotal(100.0); // Sin impuestos ni descuento
  print("Total 1: \$${total1.toStringAsFixed(2)}");
  
  double total2 = calcularTotal(100.0, 0.16); // Con impuesto 16%
  print("Total 2: \$${total2.toStringAsFixed(2)}");
  
  double total3 = calcularTotal(100.0, 0.16, 0.10); // Con impuesto y descuento
  print("Total 3: \$${total3.toStringAsFixed(2)}");
}

/**
 * Saluda a una persona
 * Los parámetros entre [] son OPCIONALES POSICIONALES
 * IMPORTANTE: Deben ir AL FINAL de la lista de parámetros
 * 
 * @param nombre OBLIGATORIO
 * @param apellido OPCIONAL (tiene valor por defecto)
 * @param titulo OPCIONAL (tiene valor por defecto)
 */
void saludar(String nombre, [String apellido = "", String titulo = ""]) {
  String saludo = "";
  
  if (titulo.isNotEmpty) {
    saludo += "$titulo ";
  }
  
  saludo += nombre;
  
  if (apellido.isNotEmpty) {
    saludo += " $apellido";
  }
  
  print("¡Hola, $saludo!");
}

/**
 * Calcula el total a pagar
 * @param subtotal OBLIGATORIO
 * @param impuesto OPCIONAL (por defecto 0)
 * @param descuento OPCIONAL (por defecto 0)
 */
double calcularTotal(double subtotal, [double impuesto = 0.0, double descuento = 0.0]) {
  double montoDescuento = subtotal * descuento;
  double montoImpuesto = subtotal * impuesto;
  
  double total = subtotal - montoDescuento + montoImpuesto;
  
  print("\nCálculo:");
  print("  Subtotal: \$${subtotal.toStringAsFixed(2)}");
  print("  Descuento (${(descuento * 100).toInt()}%): -\$${montoDescuento.toStringAsFixed(2)}");
  print("  Impuesto (${(impuesto * 100).toInt()}%): +\$${montoImpuesto.toStringAsFixed(2)}");
  
  return total;
}
```

### Ejemplo 2: Uso práctico en cálculos y formatos
```dart
void main() {
  // FORMATO de texto con parámetros opcionales
  String texto1 = formatearTexto("HOLA MUNDO");
  print("Texto 1: $texto1");
  
  String texto2 = formatearTexto("hola mundo", true); // Con capitalización
  print("Texto 2: $texto2");
  
  String texto3 = formatearTexto("texto importante", true, 3); // Con exclamaciones
  print("Texto 3: $texto3");
  
  // CÁLCULO de estadísticas
  print("\n=== Estadísticas ===");
  List<int> numeros = [10, 20, 30, 40, 50];
  
  Map<String, double> stats1 = calcularEstadisticas(numeros);
  print("Básicas: $stats1");
  
  Map<String, double> stats2 = calcularEstadisticas(numeros, true); // Con media
  print("Con media: $stats2");
  
  Map<String, double> stats3 = calcularEstadisticas(numeros, true, true); // Con todo
  print("Completas: $stats3");
}

/**
 * Formatea un texto con opciones
 * @param texto OBLIGATORIO - texto a formatear
 * @param capitalizar OPCIONAL - true para capitalizar primera letra
 * @param exclamaciones OPCIONAL - número de ! al final
 */
String formatearTexto(String texto, [bool capitalizar = false, int exclamaciones = 0]) {
  String resultado = texto.toLowerCase();
  
  if (capitalizar && resultado.isNotEmpty) {
    resultado = resultado[0].toUpperCase() + resultado.substring(1);
  }
  
  resultado += "!" * exclamaciones;
  
  return resultado;
}

/**
 * Calcula estadísticas de una lista
 * Parámetros opcionales controlan qué estadísticas calcular
 */
Map<String, double> calcularEstadisticas(
  List<int> numeros, 
  [bool calcularMedia = false, 
   bool calcularDesviacion = false]
) {
  Map<String, double> resultados = {};
  
  if (numeros.isEmpty) return resultados;
  
  // Siempre calculamos suma y máximo
  int suma = 0;
  int maximo = numeros[0];
  int minimo = numeros[0];
  
  for (int num in numeros) {
    suma += num;
    if (num > maximo) maximo = num;
    if (num < minimo) minimo = num;
  }
  
  resultados["suma"] = suma.toDouble();
  resultados["maximo"] = maximo.toDouble();
  resultados["minimo"] = minimo.toDouble();
  resultados["rango"] = (maximo - minimo).toDouble();
  
  // Estadísticas opcionales
  if (calcularMedia) {
    double media = suma / numeros.length;
    resultados["media"] = media;
    
    if (calcularDesviacion) {
      // Desviación estándar (simplificada)
      double sumaDiferencias = 0;
      for (int num in numeros) {
        double diferencia = (num - media);
        sumaDiferencias += diferencia * diferencia;
      }
      double desviacion = sqrt(sumaDiferencias / numeros.length);
      resultados["desviacion"] = desviacion;
    }
  }
  
  return resultados;
}

double sqrt(double x) {
  // Implementación simple para ejemplo
  return x * x;
}
```

### Ejemplo 3: Combinación con parámetros obligatorios
```dart
void main() {
  // CONFIGURACIÓN del sistema
  configurarSistema("MiApp");
  configurarSistema("MiApp", 8080);
  configurarSistema("MiApp", 8080, "español");
  configurarSistema("MiApp", 8080, "español", true);
  
  // REGISTRO en el sistema
  registrarUsuario("carlos123", "Carlos123!");
  registrarUsuario("ana_g", "Ana456!", "ana@email.com");
  registrarUsuario("maria_x", "Maria789!", "maria@email.com", true);
  
  // MENSAJES del sistema
  String msg1 = crearMensaje("Éxito", "Operación completada");
  print("Mensaje 1: $msg1");
  
  String msg2 = crearMensaje("Error", "No autorizado", 401);
  print("Mensaje 2: $msg2");
  
  String msg3 = crearMensaje("Alerta", "Batería baja", 15, true);
  print("Mensaje 3: $msg3");
}

/**
 * Configura el sistema con parámetros opcionales
 * @param nombreApp OBLIGATORIO
 * @param puerto OPCIONAL
 * @param idioma OPCIONAL
 * @param debug OPCIONAL
 */
void configurarSistema(String nombreApp, 
                      [int puerto = 3000, 
                       String idioma = "inglés",
                       bool debug = false]) {
  print("⚙️ Configurando $nombreApp...");
  print("   Puerto: $puerto");
  print("   Idioma: $idioma");
  print("   Modo debug: ${debug ? 'Activado' : 'Desactivado'}");
  print("");
}

/**
 * Registra un usuario en el sistema
 * @param usuario OBLIGATORIO
 * @param contrasena OBLIGATORIO
 * @param email OPCIONAL
 * @param aceptaTerminos OPCIONAL
 */
bool registrarUsuario(String usuario, String contrasena,
                     [String? email, bool aceptaTerminos = false]) {
  
  print("👤 Registrando usuario: $usuario");
  
  if (!aceptaTerminos) {
    print("   ❌ Debe aceptar los términos y condiciones");
    return false;
  }
  
  if (email != null) {
    print("   📧 Email: $email");
  }
  
  // Validación de contraseña (simple)
  if (contrasena.length < 8) {
    print("   ❌ La contraseña debe tener al menos 8 caracteres");
    return false;
  }
  
  print("   ✅ Usuario registrado exitosamente\n");
  return true;
}

/**
 * Crea un mensaje del sistema
 * @param tipo OBLIGATORIO
 * @param contenido OBLIGATORIO
 * @param codigo OPCIONAL
 * @param urgente OPCIONAL
 */
String crearMensaje(String tipo, String contenido,
                   [int codigo = 200, bool urgente = false]) {
  
  String prefijo = "";
  
  switch (tipo.toLowerCase()) {
    case "éxito":
    case "exito":
      prefijo = "✅";
      break;
    case "error":
      prefijo = "❌";
      break;
    case "alerta":
      prefijo = "⚠️";
      break;
    case "info":
      prefijo = "ℹ️";
      break;
  }
  
  if (urgente) {
    prefijo = "🚨 $prefijo";
  }
  
  String mensaje = "$prefijo [$codigo] $contenido";
  
  return mensaje;
}
```

---

## 5. Arrow Functions (=>)

### Ejemplo 1: Arrow functions básicas
```dart
void main() {
  // ARROW FUNCTIONS (=>): Sintaxis concisa para funciones de una línea
  
  // Funciones matemáticas simples
  print("Suma: ${sumar(5, 3)}");
  print("¿10 es par? ${esPar(10)}");
  print("Cuadrado de 4: ${cuadrado(4)}");
  
  // Uso en cálculos
  List<int> numeros = [1, 2, 3, 4, 5];
  List<int> cuadrados = numeros.map((n) => n * n).toList();
  print("Cuadrados: $cuadrados");
  
  // Arrow functions como parámetros
  ejecutarOperacion(5, 3, (a, b) => a + b);
  ejecutarOperacion(5, 3, (a, b) => a * b);
  
  // Funciones que retornan otras funciones
  var multiplicador = crearMultiplicador(5);
  print("5 × 7 = ${multiplicador(7)}");
}

/**
 * Arrow function: sintaxis '=>' para funciones de una línea
 * Equivalente a: int sumar(int a, int b) { return a + b; }
 */
int sumar(int a, int b) => a + b;

/**
 * Verifica si un número es par
 * => retorna automáticamente la expresión
 */
bool esPar(int numero) => numero % 2 == 0;

/**
 * Calcula el cuadrado de un número
 */
int cuadrado(int n) => n * n;

/**
 * Ejecuta una operación con dos números
 * Recibe una arrow function como parámetro
 */
void ejecutarOperacion(int a, int b, int Function(int, int) operacion) {
  int resultado = operacion(a, b);
  print("$a operación $b = $resultado");
}

/**
 * Arrow function que retorna otra arrow function
 * Crea un multiplicador específico
 */
int Function(int) crearMultiplicador(int factor) => (int numero) => factor * numero;
```

### Ejemplo 2: Arrow functions con colecciones
```dart
void main() {
  // USO COMÚN: Con métodos de colecciones como map, where, etc.
  
  List<int> edades = [15, 22, 12, 30, 17, 25, 16];
  List<String> nombres = ["Ana", "Carlos", "María", "Juan", "Laura"];
  
  // 1. Filtrar con arrow function
  var mayores = edades.where((edad) => edad >= 18).toList();
  print("Mayores de edad: $mayores");
  
  // 2. Transformar con arrow function
  var nombresMayusculas = nombres.map((nombre) => nombre.toUpperCase()).toList();
  print("Nombres en mayúsculas: $nombresMayusculas");
  
  // 3. Combinar operaciones
  var resultado = edades
      .where((edad) => edad >= 16)        // Filtra >= 16
      .map((edad) => edad * 12)          // Convierte a meses
      .where((meses) => meses >= 200)    // Filtra >= 200 meses
      .toList();
  
  print("Edades en meses (>=200): $resultado");
  
  // 4. Arrow functions en funciones de orden superior
  procesarLista(edades, (n) => n * 2, "Duplicado");
  procesarLista(edades, (n) => n ~/ 2, "Mitad entera");
  
  // 5. Validación con arrow function
