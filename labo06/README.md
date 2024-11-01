# 🚽✂️📄 Laboratorio: Piedra, Papel o Tijera con GUI

Os acordáis del laboratorio dónde hicimos el juego de Piedra, papel o tijera??

Pus bien, hoy vamos a desarrollar una versión gráfica. Este proyecto lo iremos desarrollando por versiones, cada una con nueva funcionalidad para que podamos mejorar poco a poco nuestra app. 

Y para terminar vamos a ejecutar nuestra aplicación en nuestro teléfono físico Android. 

¡Manos a la obra! 👷‍♂️👷‍♀️

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
- Añade una variable `showDialog` que controle cuándo mostrar el diálogo (`true` o `false`). Esta variable se actualiza a `true` al finalizar una partida. Y se actualiza a `false` al hacer clic en el botón de aceptar del diálogo y también cuando ocurre el evento `onDismissRequest`. del própio diálogo, es decir, pinchan fuera del dialogo. 
- Al terminar una partida, muestra el diálogo con el resultado dependiendo del valor `showDialog`

### Documentación
Puedes revisar la documentación oficial de `AlertDialog` aquí: [AlertDialog - Jetpack Compose](https://developer.android.com/develop/ui/compose/components/dialog#alert)

En este enlace se pueden revisar todos los `Dialogs` que se pueden hacer con Jetpack Compose, ya que sugerimos usar el `AlertDialog` pero hay otros tipos de dialogos que se pueden usar.

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
Añadiremos una barra de progreso para indicar que el resultado está siendo calculado. En realidad, mientras se mueve esta barra de progreso, **NO SE ESTÁ CALCULANDO EL RESULTADO!** Esto ayudará a mejorar la experiencia del usuario. 

### Explicación
Vamos a usar `LinearProgressIndicator` para simular un tiempo de espera antes de mostrar el resultado. Colocaremos esta barra justo debajo de los botones para que el usuario sepa que el resultado está siendo procesado.

### Requisitos
- Añade una barra de progreso (`LinearProgressIndicator`) que se muestre mientras se calcula el resultado, en la parte de la GUI que quieras que se vea.
- Utiliza `LaunchedEffect` para generar un retraso aleatorio antes de mostrar el resultado.
- Crearemos otra variable `isPlaying` que controlará cuándo mostrar la barra de progreso, tomará los valores `true` o `false` dependiendo de si se está **simulando** el calculo del resultado.
- Debemos crear la barra de progreso cuando se está **jugando** y no mostrarla cuando ya se ha terminado de jugar. Por lo tanto, `isPlaying` debe ser `true` cuando se está jugando y `false` cuando ya se ha terminado de jugar.

### Documentación
Puedes encontrar más detalles sobre los [`Progress Indicators`](https://developer.android.com/develop/ui/compose/components/progress) hay varios tipos de indicadores de progreso, pero en este caso sugerimos usar el `LinearProgressIndicator`.

Si quires saber más [`LinearProgressIndicator`] (https://developer.android.com/reference/com/google/android/material/progressindicator/LinearProgressIndicator)


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
Para reproducir sonidos, usaremos `MediaPlayer`. Vamos a añadir archivos de sonido (`win_sound.mp3` y `lose_sound.mp3`) en la carpeta `res/raw` de nuestro proyecto. `MediaPlayer` es una clase que nos permite reproducir audio en Android y es ideal para este propósito.

### Qué es `MediaPlayer`
`MediaPlayer` es una clase en Android que se utiliza para la reproducción de archivos de audio y video. Proporciona métodos para controlar la reproducción, pausar, detener y liberar recursos cuando ya no se necesitan. Es especialmente útil para reproducir sonidos cortos

[Descripción general ](https://developer.android.com/media/platform/mediaplayer?hl=es-419)

[Documentación](https://developer.android.com/reference/android/media/MediaPlayer)

### Cómo Usar `MediaPlayer`
1. **Añadir los Archivos de Sonido**  
   Primero, asegúrate de tener los archivos de sonido (`win_sound.mp3` y `lose_sound.mp3`) en la carpeta `app/res/raw` de tu proyecto. Si la carpeta `raw` no existe, deberás crearla dentro del directorio `res` de tu proyecto. Para crear esta carpeta en Android Studio:
   - Haz clic derecho en la carpeta `res`.
   - Selecciona **New > Android Resource Directory**.
   - En **Resource type**, selecciona `raw` y presiona **OK**.
   - Ahora puedes añadir los archivos de sonido (`wav`, `mp3`, `ogg`) en esta carpeta. OJO!! no puedes tener dos ficheros que se llamen igual pero con distinta extensión. Es decir, no puedes tener `win_sound.mp3` y `win_sound.wav` en la misma carpeta. Bueno, puedes tenerlo pero Android Studio no te dejará compilar el proyecto.
   
   Puedes buscar y descargar los sonidos en cualquier página de stock de sonidos y samples, o te los puedes descargar aquí:
   - Sonido de victoria: 
  
    <audio controls>
      <source src="res/win_sound.mp3" type="audio/mpeg">
      Tu navegador no soporta reproducción de audio.
    </audio>
  
    - [Descargar el sonido win_sound.mp3](res/win_sound.mp3)
    - Cuidado al descargar, te abrirá el archivo en el repositorio, deberás después pulsar el botón de descarga que está arriba a la derecha y que es un icono de una flecha hacia abajo. Y ojo!! poner el nombre correcto del fichero `win_sound.mp3`
 
   - Sonido de derrota: 
  
    <audio controls>
      <source src="res/lose_sound.mp3" type="audio/mpeg">
      Tu navegador no soporta reproducción de audio.
    </audio>
  
    - [Descargar el sonido lose_sound.mp3](res/lose_sound.mp3)
    - Cuidado al descargar, te abrirá el archivo en el repositorio, deberás después pulsar el botón de descarga que está arriba a la derecha y que es un icono de una flecha hacia abajo. Y ojo!! poner el nombre correcto del fichero `lose_sound.mp3`

1. **Crear y Configurar `MediaPlayer`**  
   `MediaPlayer` se debe crear dentro del contexto en el que se vaya a reproducir el sonido. En nuestro caso cuando llamamos a la función que ejecuta nuestra GUI le pasamos una función lambda para el evento `onPlaySound` que recibe un recurso de sonido y ahí creamos un `MediaPlayer` para reproducir el sonido y le mandamos reproducir el sonido que recibe por el parámetro `soundRes`. 

   Por lo tanto, cuando llamamos a nuestra función con la interfaz gráfica deberíamos configurar el `MediaPlayer` en el evento `onPlaySound` para que reproduzca el sonido adecuado.

   Código sugerido:
   
   ```kotlin
   PiedraPapelTijeraVisualTheme {
                Scaffold(
                    modifier = Modifier.fillMaxSize()
                ) { paddingValues -> 
                    // Renombramos `it` a `paddingValues` para mayor claridad
                    // Aplicamos el padding en el contenedor o componente hijo
                    PiedraPapelTijeraApp(modifier = Modifier.padding(paddingValues), onPlaySound = { soundRes ->
                        val mediaPlayer = MediaPlayer.create(this, soundRes)
                        mediaPlayer.setOnCompletionListener { it.release() }
                        mediaPlayer.start()
                    })
                }
            }
   ```
   ¿Cómo funciona?

   - **`MediaPlayer.create(context, resId)`**: Esta función se utiliza para inicializar `MediaPlayer` con el contexto actual y el recurso de audio. Es importante pasar el contexto adecuado para que el `MediaPlayer` pueda acceder a los recursos.
   - **`setOnCompletionListener`**: Configura un listener para liberar el `MediaPlayer` una vez que el sonido ha terminado de reproducirse. Esto es crucial para evitar fugas de memoria.
   - **`start()`**: Inicia la reproducción del sonido.

2. **Reproducir Sonidos**
   Ahora lo único que queda es reproducir el sonido adecuado cuando el usuario gane o pierda. Debes colocar la lógica de reproducción del sonido justo después de determinar el resultado de la partida. Por ejemplo, si el resultado es "Ganaste", reproducimos un sonido de victoria, y si es "Perdiste", reproducimos un sonido de derrota.
   
   Código Sugerido
   ```kotlin
    if (result == "Ganaste") {
                userWins++
                onPlaySound(R.raw.win_sound) // Reproduce sonido alegre si gana el usuario
            } else if (result == "Perdiste") {
                computerWins++
                onPlaySound(R.raw.lose_sound) // Reproduce sonido triste si pierde el usuario
            }
    ```
    **¿Qué significa `R.raw.win_sound` o `R.raw.lose_sound`?**  
   `R.raw.win_sound` hace referencia al recurso de audio que está ubicado en la carpeta `res/raw` de tu proyecto. `R` es una clase generada automáticamente por Android que contiene referencias (Resources) a todos los recursos del proyecto. `raw` es la subcarpeta que creamos al inicio y donde se encuentran los archivos de sonido, y `win_sound` `lose_sound` es el nombre del archivo sin su extensión.

# Es hora de probar nuestra aplicación en un dispositivo físico Android 📱

Para ello recomiendo seguir la documentación oficial de Android Studio para [ejecutar aplicaciones en un dispositivo físico](https://developer.android.com/studio/run/device?hl=es-419).