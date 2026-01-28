¡Bienvenidos al **Módulo 7**! Imagina que estás en una fila para comprar una hamburguesa. Si el cajero se queda parado esperando a que la carne se cocine y no atiende a nadie más, eso es **sincronía** (bloqueo). Pero si te da un ticket, atiende al siguiente y te llama cuando la comida esté lista, eso es **asincronía**.

En Dart, esto es vital para que las aplicaciones no se "traben" mientras descargan datos de internet.

---

### 1. Concepto de asincronía
La asincronía permite que una tarea pesada se ejecute en "segundo plano" mientras el resto del programa sigue funcionando.

#### Ejemplo 1: El proceso de la lavadora
```dart
void main() {
  print("1. Meter ropa a la lavadora");
  
  // Esto simula una tarea que toma tiempo
  Future.delayed(Duration(seconds: 3), () {
    print("3. ¡Ropa limpia! (Terminó después de 3 segundos)");
  });

  print("2. Ver una serie en Netflix mientras espero");
}
```
**Explicación:** El programa no se detiene en el paso 2. Imprime el 1, inicia la lavadora, sigue con el paso 2 y, cuando la lavadora termina (3 segundos después), aparece el mensaje 3.

#### Ejemplo 2: Pedir una Pizza
```dart
void main() {
  print("Llamando a la pizzería...");
  
  Future.delayed(Duration(seconds: 2), () => print("Pizza entregada 🍕"));
  
  print("Poner la mesa y sacar los vasos...");
}
```
**Explicación:** No necesitas quedarte pegado al teléfono para poner la mesa. Dart ejecuta la "entrega de pizza" en el futuro y te permite seguir con tus otras tareas.

#### Ejemplo 3: Descarga de un archivo
```dart
void main() {
  print("Iniciando descarga...");
  Future.delayed(Duration(seconds: 4), () => print("Descarga completa 100%"));
  print("Puedes seguir navegando en la app...");
}
```
**Explicación:** El usuario puede seguir interactuando con la interfaz de la app mientras el archivo se descarga "detrás de escenas".

---

### 2. Uso de `Future`
Un `Future` representa un valor que aún no está disponible, pero que llegará (como una promesa o un ticket de preventa).

#### Ejemplo 1: Obtener nombre de usuario
```dart
Future<String> obtenerUsuario() {
  // Simulamos que el servidor tarda 2 segundos en responder
  return Future.delayed(Duration(seconds: 2), () => "Juan_Perez_99");
}

void main() {
  print("Buscando usuario...");
  obtenerUsuario().then((nombre) {
    print("Usuario encontrado: $nombre");
  });
}
```
**Explicación:** `Future<String>` dice: "Ahorita no tengo el texto, pero te prometo un String en el futuro". Usamos `.then()` para decir qué hacer cuando el valor llegue.

#### Ejemplo 2: Consultar el clima
```dart
Future<int> obtenerTemperatura() {
  return Future.delayed(Duration(seconds: 3), () => 25);
}

void main() {
  print("Consultando clima...");
  obtenerTemperatura().then((temp) => print("La temperatura es de $temp°C"));
}
```
**Explicación:** La función devuelve un "ticket" (`Future`). Cuando pasan los 3 segundos, el ticket se canjea por el número 25.

#### Ejemplo 3: Verificación de edad
```dart
Future<bool> esMayorDeEdad() {
  return Future.delayed(Duration(seconds: 1), () => true);
}

void main() {
  esMayorDeEdad().then((resultado) => print("¿Es mayor?: $resultado"));
}
```
**Explicación:** Muy útil para procesos que requieren consultar una base de datos local o remota.

---

### 3. Palabras clave `async` y `await`
Es la forma moderna y fácil de leer la asincronía. `async` marca una función como asíncrona y `await` hace que el programa espere el resultado de forma ordenada.

#### Ejemplo 1: Comprar un café
```dart
Future<void> prepararCafe() async {
  print("Preparando café...");
  await Future.delayed(Duration(seconds: 2)); // Espera aquí
  print("Café listo ☕");
}

void main() async {
  print("Inicio del día");
  await prepararCafe(); // Esperamos a que el café esté listo para seguir
  print("A trabajar");
}
```
**Explicación:** Con `await`, el código parece que se lee de arriba hacia abajo, lo cual es más fácil de entender que usar `.then()`.

#### Ejemplo 2: Login de usuario
```dart
Future<String> validarDatos() async {
  await Future.delayed(Duration(seconds: 2));
  return "Acceso Concedido";
}

void main() async {
  print("Intentando entrar...");
  String respuesta = await validarDatos();
  print(respuesta);
}
```
**Explicación:** `main` debe ser `async` para poder usar `await`. El programa se pausa en la línea del `await` hasta que `validarDatos` termina.

#### Ejemplo 3: Cargar nivel de un juego
```dart
Future<void> cargarMapa() async {
  await Future.delayed(Duration(seconds: 3));
  print("Mapa cargado");
}

void main() async {
  print("Cargando juego...");
  await cargarMapa();
  print("¡A jugar!");
}
```
**Explicación:** Asegura que el jugador no empiece a caminar hasta que el mapa esté completamente listo.

---

### 4. Manejo de errores con `try`, `catch` y `finally`
En la asincronía muchas cosas pueden fallar (se cae el internet, el servidor no responde). Estas herramientas evitan que la app se cierre.

#### Ejemplo 1: Error de conexión
```dart
Future<void> descargarDatos() async {
  await Future.delayed(Duration(seconds: 2));
  throw "Error 404: No se encontró el archivo"; // Simulamos un error
}

void main() async {
  try {
    await descargarDatos();
  } catch (error) {
    print("Ups, algo salió mal: $error");
  } finally {
    print("Proceso finalizado (con o sin error)");
  }
}
```
**Explicación:** `try` intenta hacer algo. Si falla, el control pasa a `catch`. El bloque `finally` siempre se ejecuta, ideal para cerrar animaciones de "Cargando...".

#### Ejemplo 2: División entre cero
```dart
void calcular() {
  try {
    int resultado = 10 ~/ 0; // Operación imposible
    print(resultado);
  } catch (e) {
    print("Error matemático: No puedes dividir entre cero.");
  }
}

void main() {
  calcular();
}
```
**Explicación:** Aunque no es asíncrono, muestra el uso básico: el programa no "explota", simplemente nos avisa del error de forma amable.

#### Ejemplo 3: Leer una base de datos vacía
```dart
Future<String> leerDB() async {
  throw Exception("Base de datos no encontrada");
}

void main() async {
  print("Iniciando lectura...");
  try {
    String datos = await leerDB();
    print(datos);
  } catch (e) {
    print("Aviso: No pudimos leer los datos.");
  } finally {
    print("Cerrando conexión con el servidor.");
  }
}
```
**Explicación:** `finally` es perfecto aquí para asegurar que, pase lo que pase, la conexión se cierre correctamente y no se gasten recursos.
