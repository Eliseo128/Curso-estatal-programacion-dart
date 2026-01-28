¡Bienvenidos al **Módulo 2**! En esta etapa aprenderemos a darle "cerebro" a nuestros programas. El control de flujo permite que el código tome decisiones (¿hago esto o aquello?) y repita tareas sin que nosotros tengamos que escribir lo mismo mil veces.

---

### 1. Estructuras condicionales: `if`, `else if`, `else`
Es como un camino con varias desviaciones. El programa evalúa una condición y decide por qué camino ir.

#### Ejemplo 1: Calificación de un examen
```dart
int nota = 85;

if (nota >= 90) {
  print("Excelente desempeño");
} else if (nota >= 70) {
  print("Aprobado");
} else {
  print("Necesitas mejorar");
}
```
**Explicación:** El programa revisa primero si la nota es 90 o más. Si no se cumple, pasa a la siguiente instrucción (`else if`) para ver si al menos es 70. Si ninguna es cierta, ejecuta el `else` por defecto.

#### Ejemplo 2: Acceso a una discoteca
```dart
int edad = 16;

if (edad >= 18) {
  print("Puedes pasar");
} else {
  print("Eres menor de edad, no puedes entrar");
}
```
**Explicación:** Aquí solo hay dos opciones. O se cumple la condición de ser mayor de 18, o se ejecuta la acción contraria en el `else`.

#### Ejemplo 3: Estado de un semáforo
```dart
String luz = "Amarillo";

if (luz == "Verde") {
  print("Avanza");
} else if (luz == "Amarillo") {
  print("Precaución, detente");
} else {
  print("Alto total");
}
```
**Explicación:** El programa compara el texto guardado en la variable `luz` para decidir qué mensaje mostrar al conductor.

---

### 2. Operador ternario
Es una forma súper corta de escribir un `if-else` en una sola línea. Se usa mucho para asignar valores rápidos. 
**Estructura:** `condición ? valor_si_es_verdad : valor_si_es_falso`

#### Ejemplo 1: ¿Pasaste o reprobaste?
```dart
double promedio = 6.5;
String resultado = (promedio >= 6.0) ? "Aprobado" : "Reprobado";
print(resultado);
```
**Explicación:** Si el promedio es mayor o igual a 6.0, la variable `resultado` guarda "Aprobado". Si no, guarda "Reprobado". Es mucho más rápido que escribir 5 líneas de `if`.

#### Ejemplo 2: Modo oscuro o claro
```dart
bool esNoche = true;
String tema = esNoche ? "Dark Mode" : "Light Mode";
print("El tema de la app es: $tema");
```
**Explicación:** Dependiendo del valor booleano de `esNoche`, la app decide qué diseño mostrar.

#### Ejemplo 3: ¿Es par o impar?
```dart
int numero = 7;
String tipo = (numero % 2 == 0) ? "Par" : "Impar";
print("El número es $tipo");
```
**Explicación:** Usamos el operador `%` (residuo). Si el residuo de dividir entre 2 es cero, es par; de lo contrario, es impar.

---

### 3. Estructura `switch` y `case`
Se usa cuando tienes muchas opciones posibles para una **misma variable**. Es más organizado que usar diez `else if`.

#### Ejemplo 1: Días de la semana
```dart
int dia = 3;

switch (dia) {
  case 1: print("Lunes"); break;
  case 2: print("Martes"); break;
  case 3: print("Miércoles"); break;
  default: print("Día no válido");
}
```
**Explicación:** El programa busca el `case` que coincida con el número 3. El `break` es importante para que el programa deje de buscar una vez que encuentre el correcto.

#### Ejemplo 2: Menú de cafetería
```dart
String pedido = "Café";

switch (pedido) {
  case "Café": print("Cuesta \$20"); break;
  case "Té": print("Cuesta \$15"); break;
  case "Jugo": print("Cuesta \$25"); break;
  default: print("No tenemos ese producto");
}
```
**Explicación:** El `switch` compara strings. Si pides algo que no está en la lista, el `default` nos ayuda a dar un mensaje de error.

#### Ejemplo 3: Nivel de un jugador
```dart
String rango = "Plata";

switch (rango) {
  case "Bronce": print("Nivel inicial"); break;
  case "Plata": print("Nivel intermedio"); break;
  case "Oro": print("Nivel experto"); break;
}
```
**Explicación:** Permite categorizar al usuario de forma limpia y legible.

---

### 4. Ciclos iterativos: `for`, `while`, `do-while`
Sirven para repetir un bloque de código.

#### Ejemplo 1: El ciclo `for` (Conteo de lanzamientos)
```dart
for (int i = 5; i >= 1; i--) {
  print("Lanzamiento en $i...");
}
print("¡Despegue! 🚀");
```
**Explicación:** El `for` es ideal cuando sabes exactamente cuántas veces quieres repetir algo. Aquí empezamos en 5 y restamos 1 (`i--`) hasta llegar a 1.

#### Ejemplo 2: El ciclo `while` (Cargando batería)
```dart
int bateria = 98;

while (bateria < 100) {
  bateria++;
  print("Cargando... nivel: $bateria%");
}
```
**Explicación:** El `while` se repite **mientras** la condición sea verdadera. Si la batería es menor a 100, sigue sumando. Si ya empieza en 100, nunca entra al ciclo.

#### Ejemplo 3: El ciclo `do-while` (Pedir contraseña)
```dart
int intentos = 0;
do {
  intentos++;
  print("Intento de conexión número $intentos");
} while (intentos < 3);
```
**Explicación:** A diferencia del `while`, el `do-while` **siempre se ejecuta al menos una vez**, y después revisa la condición para ver si se repite.

---

### 5. Uso de `break` y `continue`
Sirven para alterar el comportamiento de los ciclos.

#### Ejemplo 1: `break` (Detener una búsqueda)
```dart
for (int i = 1; i <= 10; i++) {
  if (i == 5) {
    print("Número 5 encontrado, deteniendo búsqueda.");
    break; 
  }
  print("Buscando en el número $i");
}
```
**Explicación:** El `break` rompe el ciclo por completo. Aunque el `for` debía llegar a 10, al encontrar el 5, se sale inmediatamente.

#### Ejemplo 2: `continue` (Saltar números)
```dart
for (int i = 1; i <= 5; i++) {
  if (i == 3) {
    continue; // Salta el resto de esta vuelta
  }
  print("Piso número $i");
}
```
**Explicación:** El `continue` no detiene el ciclo, solo se salta la vuelta actual. En este ejemplo, se imprimen los pisos 1, 2, 4 y 5, pero se salta el 3.

#### Ejemplo 3: `break` en un ciclo infinito
```dart
int segundos = 0;
while (true) { // Ciclo que nunca termina por sí solo
  segundos++;
  if (segundos == 4) {
    print("Tiempo límite alcanzado");
    break;
  }
}
```
**Explicación:** Usamos `while(true)` para crear un ciclo infinito, pero usamos un `if` con un `break` para forzar la salida cuando se cumpla una condición de seguridad.
