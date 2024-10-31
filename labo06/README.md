# 🚽✂️📄 Laboratorio: Piedra, Papel o Tijera con GUI

Os acordáis del laboratorio dónde hicimos el juego de Piedra, papel o tijera??

Pus bien, hoy vamos a desarrollar una versión gráfica. Este proyecto lo iremos desarrollando por versiones, cada una con nueva funcionalidad para que podamos mejorar poco a poco nuestra app. ¡Manos a la obra! 👷‍♂️👷‍♀️

## Versión 1: La Base de la App 🎲

### Objetivo
En esta primera versión, vamos a crear la estructura inicial de nuestra app. El objetivo es familiarizarnos con el layout de Jetpack Compose, pasando el `paddingValues` del `Scaffold` a nuestra función `PiedraPapelTijeraApp`. Además, implementaremos los botones para que el usuario pueda elegir entre Piedra, Papel o Tijera y veremos cómo obtener el resultado del juego.

En esta primera versión debes ser capaz de hacerlo sin problemas, ya que en otros laboratorios ya hemos visto como hacer interfaces gráficas y como manejar eventos de botones. Así que te voy a guiar un poco menos en esta versión.

### Requisitos
1. **Crea tu `MainActivity`**
   Define la actividad principal `MainActivity`. Aquí deberás inicializar el tema y utilizar `Scaffold` para crear la estructura de la app. Recuerda pasar los `paddingValues` a la función `PiedraPapelTijeraApp`:
   
   ```kotlin
   Scaffold(
       modifier = Modifier.fillMaxSize()
   ) { paddingValues ->
       PiedraPapelTijeraApp(modifier = Modifier.padding(paddingValues))
   }
   ```

2. **Diseña la UI de `PiedraPapelTijeraApp`**
   
   Tienes libertad absoluta de hacerlo como quieras, pero te recomiendo es si, hacer un primer diseño en papel.

   Utiliza una columna (`Column`) para organizar los botones verticalmente y permitir al usuario seleccionar una opción.

3. **Lógica del Juego**
   Implementa la lógica básica para que, al pulsar un botón, se genere la elección de la computadora de manera aleatoria y se determine el resultado de la partida. Muestra el resultado debajo de los botones (sin estadísticas aún).
   
   Puedes basarte y usar las funciones que ya hiciste en el laboratorio anterior.

### Código Sugerido
Aquí tienes un pequeño fragmento del código para ayudarte a empezar:

```kotlin
@Composable
fun PiedraPapelTijeraApp(modifier: Modifier) {
    var userChoice by remember { mutableStateOf("") }
    var computerChoice by remember { mutableStateOf("") }
    var result by remember { mutableStateOf("") }

    val options = listOf("Piedra", "Papel", "Tijera")

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
        verticalArrangement = Arrangement.SpaceEvenly,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        options.forEach { choice ->
            Button(onClick = { userChoice = choice }) {
                Text(text = choice)
            }
        }
        // Aquí muestra el resultado
        Text(text = "Tu elección: $userChoice, Elección de la computadora: $computerChoice, Resultado: $result")
    }
}
```

## Versión 2: Añadiendo Estadísticas 📊

### Objetivo
En esta versión, vamos a añadir estadísticas para llevar la cuenta de cuántas veces ha ganado el usuario y cuántas veces ha ganado la computadora.

### Requisitos
- Añade variables para almacenar las victorias del usuario y de la computadora (`userWins` y `computerWins`).
- Actualiza estas variables cada vez que haya un resultado.
- Muestra las estadísticas al final de la columna en la UI.

### Código Sugerido
```kotlin
var userWins by remember { mutableStateOf(0) }
var computerWins by remember { mutableStateOf(0) }

// Muestra las estadísticas
Text(text = "Ganadas por el usuario: $userWins")
Text(text = "Ganadas por la computadora: $computerWins")
```

## Versión 3: Mostrando el Resultado en un Diálogo 🗨️

### Objetivo
En esta versión, vamos a mostrar el resultado del juego en un `AlertDialog` en lugar de mostrarlo en la interfaz principal.

### Explicación
El `AlertDialog` es un componente que se utiliza para mostrar mensajes emergentes. Lo usaremos para mostrar el resultado del juego después de cada partida. La lógica será la siguiente:
- Cuando se termine la partida, se activará el diálogo para mostrar el resultado.
- Usa el composable `AlertDialog` para implementar esta funcionalidad.

### Requisitos
- Añade una variable `showDialog` que controle cuándo mostrar el diálogo (`true` o `false`).
- Al terminar una partida, muestra el diálogo con el resultado.

### Documentación
Puedes revisar la documentación oficial de `AlertDialog` aquí: [AlertDialog - Jetpack Compose](https://developer.android.com/reference/kotlin/androidx/compose/material3/package-summary#AlertDialog)

### Código Sugerido
```kotlin
var showDialog by remember { mutableStateOf(false) }

if (showDialog) {
    AlertDialog(
        onDismissRequest = { showDialog = false },
        title = { Text(text = "Resultado") },
        text = { Text(text = "Tu elección: $userChoice\nElección de la computadora: $computerChoice\nResultado: $result") },
        confirmButton = {
            Button(onClick = { showDialog = false }) {
                Text("Aceptar")
            }
        }
    )
}
```

## Versión 4: Barra de Progreso ⏳

### Objetivo
Añadiremos una barra de progreso para indicar que el resultado está siendo calculado. Esto ayudará a mejorar la experiencia del usuario.

### Explicación
Vamos a usar `LinearProgressIndicator` para simular un tiempo de espera antes de mostrar el resultado. Colocaremos esta barra justo debajo de los botones para que el usuario sepa que el resultado está siendo procesado.

### Requisitos
- Añade una barra de progreso (`LinearProgressIndicator`) que se muestre mientras se calcula el resultado.
- Utiliza `LaunchedEffect` para generar un retraso aleatorio antes de mostrar el resultado.

### Documentación
Puedes encontrar más detalles sobre `LinearProgressIndicator` aquí: [LinearProgressIndicator - Jetpack Compose](https://developer.android.com/reference/kotlin/androidx/compose/material3/package-summary#LinearProgressIndicator)

### Código Sugerido
```kotlin
if (isPlaying) {
    LinearProgressIndicator(modifier = Modifier.fillMaxWidth())
}
```

## Versión 5: Añadiendo Sonidos 🎶

### Objetivo
En la versión final, vamos a añadir sonidos para cuando el usuario gane o pierda, dándole un toque más entretenido a nuestra app.

### Explicación
Para reproducir sonidos, usaremos `MediaPlayer`. Vamos a añadir archivos de sonido (`win_sound.mp3` y `lose_sound.mp3`) en la carpeta `res/raw` de nuestro proyecto.

### Requisitos
- Añade los archivos de sonido en la carpeta `res/raw`.
- Utiliza `MediaPlayer` para reproducir el sonido adecuado cuando el usuario gane o pierda.

### Documentación
Para más información sobre `MediaPlayer`, consulta la documentación oficial: [MediaPlayer - Android Developers](https://developer.android.com/reference/android/media/MediaPlayer)

### Código Sugerido
```kotlin
val mediaPlayer = MediaPlayer.create(context, R.raw.win_sound)
mediaPlayer.setOnCompletionListener { it.release() }
mediaPlayer.start()
```

