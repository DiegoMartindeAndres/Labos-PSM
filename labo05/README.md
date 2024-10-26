# 🚀 Guía sobre la Gestión de Estado

En esta primera guía sobre la gestión de estado, haremos una introducción con un ejemplo sencillo creando un pequeño juego sobre la gestión logística de paquetes, y luego pasaremos a nuestro proyecto sobre la conversión de unidades.

## Tabla de Contenidos 📚

- [🚀 Guía sobre la Gestión de Estado](#-guía-sobre-la-gestión-de-estado)
- [📦 Introducción: Gestión Logística en Jetpack Compose](#-introducción-gestión-logística-en-jetpack-compose)
- [🔄 Continuación con la aplicación de conversión de unidades](#-continuación-con-la-aplicación-de-conversión-de-unidades)


# 📦 Introducción: Gestión Logística en Jetpack Compose

Imagina que eres el gerente de una empresa de logística que entrega paquetes. El estado de los paquetes y las rutas de entrega es crucial para tomar decisiones. Aquí es donde entra en juego la **gestión del estado**. En Jetpack Compose, el manejo del estado es como un sistema de gestión logística que guía la dirección de tu aplicación cuando ocurren eventos, como acciones del usuario o actualizaciones de datos.

Los eventos actúan como señales para ajustar el estado de la aplicación, de la misma manera que un gerente ajusta las rutas de entrega en respuesta a condiciones cambiantes.

---

## 📦 Gestión del Estado y Eventos

### 🚚 ¿Qué es la Gestión del Estado?

La gestión del estado y los eventos trabajan juntos para mantener tu aplicación en curso a través del dinámico paisaje de las interacciones del usuario. La idea principal es que cuando ocurre un evento (por ejemplo, el usuario toca un botón), se actualiza el estado, y esto desencadena una **recomposición** de la interfaz de usuario para reflejar los cambios.

### 🔄 ¿Qué es la Re-composición?

En Jetpack Compose, la interfaz de usuario se representa como un árbol de **Composables**. La **recomposición** es el proceso de regenerar y actualizar la interfaz de usuario para reflejar los cambios en el estado de la aplicación o las interacciones del usuario. Este proceso es eficiente y permite mantener la interfaz siempre actualizada.

---

## 📌 Conceptos Clave en la Gestión del Estado

### 🧠 Función `remember`

La función `remember` se utiliza para crear un estado **persistente y recordado** en Jetpack Compose. Esto permite que un Composable mantenga su estado a través de las recomposiciones, incluso cuando el Composable es recreado. Es crucial para evitar la pérdida de datos y el estado de la interfaz de usuario durante los ciclos de vida de la aplicación.

La función `remember` se recomienda para mantener el estado local de un Composable. Sin embargo, si el estado necesita ser compartido entre múltiples Composables, entonces se debe **elevar el estado** para que sea administrado por un componente superior en la jerarquía.

En otras palabras, `remember` es como un recordatorio interno del Composable. Imagina que estás haciendo una entrega y necesitas recordar cuántos paquetes has entregado. `remember` ayuda al Composable a "recordar" ese número incluso si algo cambia en la interfaz, como si fuera tu lista de paquetes entregados.

```kotlin
val count = remember { mutableStateOf(0) }
```

### 🛠 Delegado de Propiedad `mutableStateOf`

El delegado de propiedad `mutableStateOf` se utiliza para crear un estado mutable que puede ser actualizado y que, cuando cambia, provoca una recomposición del Composable que lo utiliza. Esto garantiza que los cambios en los datos se reflejen automáticamente en la interfaz de usuario.

En general, `mutableStateOf` se usa junto con `remember` para gestionar datos que cambian dentro de un Composable específico. Es como marcar un paquete como "listo para la entrega"; cualquier cambio en el estado de ese paquete (como si ha sido entregado o no) se reflejará automáticamente en tu sistema.

```kotlin
val text = remember { mutableStateOf("Hola, Jetpack Compose!") }
```

### 🔄 Integrando `remember` y `mutableStateOf`

Estos dos conceptos funcionan en conjunto:
- `remember` crea un estado que persiste a través de las recomposiciones.
- `mutableStateOf` permite actualizar el valor del estado y, cuando esto ocurre, se dispara la recomposición del Composable.

### ⬆️ Elevación del Estado

En aplicaciones más complejas, es posible que múltiples Composables necesiten acceder o modificar el mismo estado. En estos casos, es recomendable **elevar el estado** a un componente superior. Esto permite que el estado se administre de manera centralizada, lo cual facilita la sincronización de la interfaz de usuario y la lógica de la aplicación.

Elevación del estado significa mover la información relevante a un nivel más alto para que otros componentes puedan acceder a ella. Imagina que en tu empresa de logística todos necesitan acceso al inventario de paquetes. En lugar de que cada equipo tenga su propio inventario, el estado se eleva para que todos puedan consultar el inventario actualizado y tomar decisiones basadas en la misma información.

La gestión del estado en Jetpack Compose es esencial para crear aplicaciones reactivas y dinámicas. Al entender cómo utilizar `remember`, `mutableStateOf` y cuándo elevar el estado, puedes diseñar interfaces eficientes que se actualicen automáticamente en respuesta a los cambios del usuario o de los datos.

Recuerda que en aplicaciones más grandes y complejas, el estado debe ser manejado cuidadosamente para mantener el flujo de datos limpio y evitar inconsistencias. Jetpack Compose te proporciona herramientas poderosas para que la interfaz de usuario esté siempre sincronizada con el estado actual de la aplicación.


## 👀 Vistazo Rápido a los Estados en Compose

El concepto de **state** (estado) es fundamental en Compose. Este define cómo una interfaz se debe actualizar cuando cambian los datos. Hay dos tipos principales de estados:

- **Immutable State**: No puede cambiar después de ser creado.
- **Mutable State**: Puede cambiar, permitiendo que la interfaz se actualice automáticamente.

Para gestionar el estado mutable, Jetpack Compose ofrece la función `remember` junto con `mutableStateOf`. Esto nos permite guardar y recordar el valor de una variable, permitiendo que los cambios se reflejen automáticamente en la interfaz.

## 🎢 El Juego de los paquetes
En el ejemplo práctico que desarrollamos, se crea un proyecto simple llamado **Juego Paquetes**. La aplicación tiene tres componentes principales:

1. **Un texto que muestra la cantidad de paquetes encontrados**.
2. **Un texto que indica la dirección en la que se estamos navegando**.
3. **Cuatro botones** que permiten cambiar la dirección (norte, sur, este, oeste) y que otorgan una oportunidad de encontrar un paquete o enfrentarse a una tormenta.

## 📜 Código en Jetpack Compose

Para ilustrar cómo funciona el código, se presenta un ejemplo en el cual creamos una función composable para el juego de los paquetes:

```kotlin
@Composable
fun JuegoPaquetes() {
    val packagesFound = remember { mutableStateOf(0) }
    val direction = remember { mutableStateOf("Norte") }

    Column {
        Text(text = "Paquetes encontrados: ${packagesFound.value}")
        Text(text = "Dirección actual: ${direction.value}")

        Button(onClick = {
            direction.value = "Este"
            if (Random.nextBoolean()) { // 50% de probabilidad de encontrar un paquete
                packagesFound.value += 1
            }
        }) {
            Text("Ir al Este")
        }
        // Repetir para los otros botones (Oeste, Norte, Sur)
    }
}
```

### Explicación del Código
- `remember { mutableStateOf(0) }`: Esto nos permite recordar el número de paquetes que hemos encontrado. Utilizamos `remember` y `mutableStateOf` para que el valor se pueda actualizar y se refleje en la interfaz. Aunque pensemos que nos valdría con un `Int` y un `String`, necesitamos usar `remember` y `mutableStateOf` para que Compose sepa cuándo actualizar la interfaz.
- `Button(onClick = {...})`: Cada vez que hacemos clic en un botón, actualizamos la dirección del barco y tenemos una oportunidad de encontrar un paquete usando `Random.nextBoolean()`, que devuelve `true` o `false` al azar.

## 🌐 La Magia de los Estados
Uno de los conceptos clave que se ilustra aquí es cómo **Jetpack Compose se encarga de actualizar la interfaz** cuando los valores cambian. Por ejemplo, al cambiar `packagesFound.value`, Compose detecta este cambio y actualiza el componente `Text` correspondiente sin necesidad de decirle explícitamente a la interfaz que cambie.

Esto se debe a que `mutableStateOf` no solo guarda el valor, sino que también informa a Compose sobre cualquier cambio, lo que permite mantener la interfaz actualizada de manera sencilla.

## 🛡️ Tips Importantes
- **Val vs Var**: En Kotlin, `val` define una constante, mientras que `var` define una variable. Sin embargo, cuando usamos `mutableStateOf` con `val`, lo que no cambia es la referencia al objeto mutable. El valor interno puede cambiar sin problemas.
- **Recuerda Usar `remember`**: Es importante usar `remember` para que Compose pueda guardar y restaurar el estado durante la recomposición.
 
 ---
 
🛠️ **Desafío 1**: Si no encontramos un tesoro, tenemos un 1 probabilidad entre 4 de encontrarnos una tormenta. Añade un nuevo componente que muestre las tormentas que nos hemos ido encontrando.

🛠️ **Desafío 2**: Añade un nuevo componente que muestre si nuestra furgoneta de reparto está en buena o mala condición. Una furgoneta empieza con 100 puntos de vida y cada tormenta que nos encontramos nos quita 5 puntos de vida.


 
## ✨ Recordar y gestionar el estado

En Jetpack Compose, es habitual almacenar el estado de las UI usando la función `remember` junto con `mutableStateOf()`. Estos conceptos son fundamentales para crear componentes que reaccionen de manera dinámica a los cambios.

Por ejemplo:

```kotlin
val paquetesEncontrados = remember { mutableStateOf(0) }
```

La función `remember` se utiliza para almacenar un valor que necesita persistir durante la recomposición de la UI. En este caso, `mutableStateOf(0)` es el valor inicial del estado. Cada vez que este valor cambia, la UI se actualizará de manera automática.

Para acceder al valor del estado, utilizamos `.value`:

```kotlin
val cantidad = paquetesEncontrados.value
```

Y en nuestro código se traduce en:

```kotlin
Text(text = "Paquetes encontrados: ${packagesFound.value}")
```

Pero también podemos utilizar el operador `by`

## ✂️ Simplificando con el operador `by`

Hay una forma más sencilla de escribir este código, utilizando el operador `by`. Esto nos permite evitar el uso constante de `.value` para acceder al valor del estado.

Primero tendremos que importar `import androidx.compose.runtime.setValue` 

```kotlin
val paquetesEncontrados by remember { mutableStateOf(0) }
```

Con `by`, accedemos directamente al valor del estado sin necesidad de usar `.value`. En el ejemplo anterior:

- `paquetesEncontrados` ahora contiene directamente el valor.
- No necesitamos usar `paquetesEncontrados.value` para acceder al número de paquetes encontrados.

Ahora podemos usar directamente:

```kotlin	
Text(text = "Paquetes encontrados: $paquetesEncontrados")
```

### 🎁 Metáfora con los paquetes

Imagina que `paquetesEncontrados` es un paquete con objetos dentro:

- Sin usar `by`, necesitamos abrir el paquete para ver lo que hay dentro (`.value`).
- Usando `by`, el producto está directamente en nuestras manos, sin necesidad de abrir el paquete.


# 🔄 Continuación con la aplicación de conversión de unidades

Vamos a retomar nuestra aplicación de conversión de unidades. Hasta ahora, hemos trabajado en la interfaz gráfica (GUI), pero en los siguientes apartados implementaremos la lógica necesaria para que funcione correctamente.

Nota: aunque en clase hemos visto el MVC y la evolución al MVVC, de momento no vamos a usar ningún patrón de diseño concreto. En futuros laboratorios, profundizaremos en el concepto MVVC y cómo aplicarlo en aplicaciones de Android.

## 📌 Variables de Estado Necesarias
Vamos a pensar por un momento las variables que vamos a necesitar para que nuestra aplicación funcione correctamente. 

Serías capaz de pensar en las variables de estado necesarias para que nuestra aplicación funcione correctamente?

<details>
  <summary>Pincha aquí para ver esas variables.</summary>
<br>
Para crear un conversor de unidades usando Compose, necesitaremos definir varias variables de estado 🔧:

- **Valor de entrada**: representa el valor que el usuario introduce para convertir (se ingresa en el cuadro de texto).
- **Valor de salida**: resultado de la conversión (no se puede modificar).
- **Unidad de entrada**: la unidad de origen (seleccionada en el primer desplegable).
- **Unidad de salida**: la unidad de destino (seleccionada en el segundo desplegable).

⚠️ ¡Ojo! Estas no son todas las variables necesarias. Hay otras que se requieren para que la interfaz y la lógica funcionen correctamente. Son menos evidentes ahora, pero las iremos añadiendo a medida que las necesitemos. Si ya puedes identificar algunas, ¡enhorabuena! Eso significa que tienes una visión más amplia de lo que necesitamos para que nuestra aplicación funcione.
</details>
<br>


Ahora vamos a pensar como definir esas variables usando `remember`, `mutableStateOf` y si queremos la palabra clave `by`:

<details>
  <summary>Pincha aquí para ver la definición de dichas varibles.</summary>
  
```kotlin
var inputValue by remember { mutableStateOf("") }
var outputValue by remember { mutableStateOf("") }
// Inicializamos el valor inicial de la unidad de entrada y salida
var inputUnit by remember { mutableStateOf("Centímetro") }  
var outputUnit by remember { mutableStateOf("Metros") }
// Habrá más varibles, pero de momento son difíciles de intuir  
```
</details>
<br>

Nota 1: ¿Dónde las definimos? - Al principio de la función `@Composable` que contiene la interfaz gráfica. En mi caso la llamé `ConversorUnidades`.	

Nota 2: Es posible que tengas que hacer importacines para poder usar `remember` y `mutableStateOf`.

Con estas varibles podemos controlar los datos de entrada que introduce el usuario, la unidad de entrada y salida, y el resultado de la conversión. Ahora lo que tenemos es que enlazarlo con la interfaz gráfica.

## 🖊️ OutlinedTextField que nunca cambia su valor

En la interfaz gráfica, tenemos un `OutlinedTextField` que debería mostrar lo que el usuario introduce por teclado. Sin embargo, este campo siempre aparece vacío, sin importar lo que escribamos. 

Aunque puede resultar sorprendente, este comportamiento es normal, ya que no hemos programado nada para que el valor cambie. Tampoco hemos vinculado nuestro modelo (por ahora, solo una variable) con la interfaz gráfica.

Hemos creado una variable `inputValue` que almacena el valor introducido por el usuario. Es momento de enlazarla con la GUI.

¿Cómo lo haremos? Primero, debemos indicar que el `value` del `OutlinedTextField` es `inputValue` y asegurarnos de que cuando `inputValue` cambie, se actualice la interfaz gráfica.

```kotlin	
OutlinedTextField(
    value = inputValue,
    onValueChange = { inputValue = it },
    label = { Text("Introduce el valor") }
)
```

¿Pero qué significa `onValueChange = { inputValue = it }`?

Recuerda, es una función lambda que se ejecuta cada vez que hay un cambio de valor. De este modo, `inputValue` tomará el valor de `it`, que es el nuevo valor pasado a la función lambda.

Nota: Esto no funcionará en la vista previa, solo en la aplicación en ejecución.

Con esto, hemos enlazado el valor del modelo y el de la interfaz gráfica. Ahora, cada vez que el usuario introduzca un valor, se actualizará automáticamente en el modelo y en la interfaz gráfica.

## 🔄 Sincronización del Estado
El estado debe mantenerse sincronizado entre diferentes componentes. Por ejemplo, al cambiar el valor en el campo de texto, debe actualizarse automáticamente en el resto de la interfaz. Esta es una de las ventajas de usar Compose, ya que hace que la interfaz de usuario sea reactiva y siempre coherente.

## 🎛️ Creación de botones y menús desplegables

Comencemos con la configuración básica de los botones. Tenemos dos botones: uno para la **entrada** (input) y otro para la **salida** (output). Cada botón está asociado a un **dropdown** que se debería expandir o colapsar según la interacción del usuario.
Aunque en realidad no hace nada. Está ocurriendo lo mismo que el OutlineTextField, no tenemos nada programado y debemos enlazar las variables.

Ahora nos deberíamos dar cuenta que necesitamos una variable adicional para cada botón, necesitamos definir un estado que controle si el menú desplegable está expandido o no.

```kotlin
// Definición de estados para los menús desplegables
var inputExpanded by remember { mutableStateOf(false) }
var outputExpanded by remember { mutableStateOf(false) }
```

Hemos creado dos variables booleanas, `inputExpanded` y `outputExpanded`, que almacenan los valores de como debería estar el estado de cada **dropdown**

## 🏰 Implementación del botón de entrada

¿Cuando queremos que se explanda el primer **dropdown**? - Cuando hacemos clic en el botón de entrada. Para ello, necesitamos que al hacer clic en el botón de unidades de origen, cambie el estado de `inputExpanded` a `true`.

```kotlin
Button(onClick = { inputExpanded = true }) {
    Text("Mostrar menú de entrada")
}
```

Pero no basta con esto. Al **Dropdown** correspondiente, debemos decirle que `expanded` es igual a `inputExpanded` .

```kotlin
DropdownMenu(
    expanded = inputExpanded,
...
)
```
Prueba a ver que pasa. Y verás que se expande el primer menú al hacer clic en el botón.	

Antes de continuar, vamos a implementar el otro **dropdown** de entrada. Usando la variable `outputExpanded` para controlar el estado del menú. Si lo pruebas, verás que hace cosas un poco extrañas porque aún no hemos implementado el colapso del menú. Verás que se expande el menú de entrada al hacer clic en el botón. Pero si vuelves a pulsar, no ocurre nada, sigue expandido.

Para colapsar el menú, necesitamos controlar el evento `onDismissRequest`. El evento `onDismissRequest` se activa cuando el usuario hace clic fuera del menú.


```kotlin
DropdownMenu(
    expanded = inputExpanded,
    onDismissRequest = { inputExpanded = false }
) {
    // Elementos del menú
}
```

Haz esto para los dos **dropdown**

Si lo pruebas, verás que si pulsamos fuera del **dropdown** el menú se colapsa.


## Implementación del `onClick` en los `DropdownMenuItem`

Cuando el usuario selecciona una opción del menú, debemos hacer varias cosas:

1. Actualizar el valor de la unidad de entrada o de salida.
2. Colapsar el menú desplegable.

Ahora nos damos cuenta, que si cambiamos las unidades de origen y las unidades de destino, podemos calcular una cosa que llamaremos **factor de conversión**, es decir, si la unidad de origen es **centímetros** y la de destino es **metros**, el factor de conversión será 0.01. Si la unidad de origen es **metros** y la de destino es **centímetros**, el factor de conversión será 100. 

Por lo tanto podemos hacer un paso nuevo:

3. Podemos calcular el factor de conversión. (Poniendo como unidad de referencia los metros.) NOTA: aunque claro, esto nos supone crear una variable nueva que no habíamos contado con ella: `var convertionFactor by remember { mutableStateOf(0.01) }`	

```kotlin
DropdownMenuItem(onClick = {
    inputExpanded = false
    inputUnit = "Centímetros"
    convertionFactor = 0.01
}) {
    Text("Centímetros")
}
```

Si lo pruebas, verás que en el primer **dropdown** al seleccionar **Centímetros**, se colapsa el menú (y se actualiza el valor de la unidad de entrada.) Si pulsas cualquier otra opción, no pasa nada.



## ⚙️ Conversión de Unidades

En este ejemplo, se realiza la conversión de diferentes unidades, como centímetros y metros. Para ello, se utiliza una función que actualiza el valor de conversión basado en la opción seleccionada.

```kotlin
fun convertirUnidades(unidadSeleccionada: String): Double {
    return when (unidadSeleccionada) {
        "Centímetros" -> 0.01
        "Metros" -> 1.0
        "Pies" -> 0.3048
        "Milímetros" -> 0.001
        else -> 1.0
    }
}
```

### 🚀 Ejecutar la Conversión

Cada vez que el usuario selecciona una opción en el menú, se actualiza el valor de la conversión y se colapsa el menú desplegable.

```kotlin
DropdownMenuItem(onClick = {
    val factorConversion = convertirUnidades("Centímetros")
    inputExpanded = false // Cierra el menú desplegable
    // Realiza la conversión con el factor correspondiente
}) {
    Text("Centímetros")
}
```

## 🚀 Creando una función de conversión de unidades

Vamos a implementar la función `convertUnits`, que se encargará de la lógica para convertir valores entre diferentes unidades.


### 📄 Implementación de `convertUnits`

La función `convertUnits` manejará la lógica de conversión de unidades en nuestra aplicación. La lógica es sencilla: multiplicar el valor de entrada y el factor de conversión.

### Ubicación de la función
Existen dos opciones:

1. Colocarla en la misma clase, pasando los parámetros necesarios, ya que no se podría acceder a las variables del `@Composable` directamente.  
2. Definirla como una función anidada dentro del `@Composable`, lo cual es posible en Kotlin y permite encapsular la lógica específica.

Para mayor conveniencia, colocaremos la función en el componente `@Composable` para encapsularla en el contexto adecuado.
Vamos a pensar, que debería hacer nuestro función? ¿Puedes pensar en el código que debería implementarse?


### ¿Qué debe hacer la función?
En pseudocódigo, los pasos serían:

- Tomar el valor de entrada.
- Intentar convertirlo a un Double, manejando errores si el valor no es un número.
- Multiplicarlo por el factor de conversión.
- Redondear el resultado a dos decimales.
- Almacenar el resultado en una variable para mostrarlo en la interfaz.

¿Te atreves a realizar la función?

<details>
  <summary>Pincha aquí para ver esas variables.</summary>
<br>

```kotlin
@Composable
fun ConversorUnidades() {
    var inputValue by remember { mutableStateOf("") }
    var outputValue by remember { mutableStateOf("") }

fun convertUnits() {
        // Aquí tomamos el valor de entrada, intentamos convertir a un Double, si no puede, devolverá un null, pero con el operador Elvis, si es null, se le asigna un 0.0
        val inputValueDouble = inputValue.toDoubleOrNull() ?: 0.0
        
        // Hacemos el cálculo, redondeamos y guardamos el resultado
        val result = (inputValueDouble * convertionFactor * 100).roundToInt() / 100.0
        
        // Queremos que se muestre en la GUI, por lo tanto tenemos que convertirlo a String y asignarlo a la variable que es un mutableStateOf
        outputValue = result.toString()
    }

    // Aquí se implementa la interfaz
}
```

</details>
<br>

### 🧠 Lógica de redondeo

Para evitar resultados con demasiados decimales, se utiliza una técnica de redondeo:

```kotlin
val result = (inputValueDouble * conversionFactor * 100).roundToInt() / 100.0
```

Este código primero multiplica el valor de entrada por el factor de conversión y por `100`. Luego redondea el valor usando `roundToInt()`, y finalmente lo divide por `100` para obtener el resultado con dos decimales.

## 🎨 Modificando los elementos de la interfaz

Es importante llamar la función `convertUnits()` en los eventos `onClick` de **TODOS** los `DropdownMenuItem` de entrada. Así, cada vez que se seleccione una unidad diferente, se recalculará el valor convertido.

Ejemplo para el caso de los centímetros:

```kotlin
DropdownMenuItem(
    text = { Text("Centímetros") },
    onClick = {
        inputExpanded = false
        inputUnit = "Centímetros"
        convertionFactor = 0.01
        convertUnits()
    })
```

Es necesario ajustar los valores de conversión y las unidades según corresponda. Por ejemplo, los metros tienen un factor de `1.0` ya que suponemos que el destino es metros, por lo tanto la conversión es la unidad. Pero cuando queremos convertir de pies a metros, el factor de conversión será `0.3048`

### 🏹 Ajustando el Factor de Conversión
En el código de la aplicación, comenzamos definiendo los factores de conversión para las unidades:

- Para metros (💪), el valor predeterminado es `1`.
- Para centímetros, el valor será `0.01` ya que hay 100 cm en un metro.
- Para pies (🥾), utilizaremos un factor de `0.3048`, ya que un pie equivale a 0.3048 metros.
- Para milímetros, el valor será `0.001`, ya que hay 1000 mm en un metro.

### Houston tenemos un problema!!

Ya te debes estar dando cuenta que con un solo factor de conversión no es suficiente, ya que si queremos convertir de un origen a un destino, el factor de conversión no es el mismo que de metros a pies. Por lo tanto, necesitamos dos factores de conversión, uno para la unidad de entrada y otro para la unidad de salida.

Por lo tanto, vamos a refactorizar renombrando la variable `convertionFactor` a `inputConvertionFactor` y crearemos una nueva variable llamada `outputConvertionFactor`.

Para hacerlo más sencillo, vamos a inicializar las variables `inputConvertionFactor` y `outputConvertionFactor` con el valor `1.0` y eso nos forzará a inicializar `inputUnit` y `outputUnit` a Metros.

### 🔬 Retocar la función de los Cálculos de Conversión
Para realizar una conversión, donde hacemos la operación, debemos multiplicar por el factor de conversión de entrada (esto ya lo teníamos) y dividir por el factor de conversión de salida.

<details>
  <summary>¿Puedes hacerlo sin ayuda?</summary>
<br>

```kotlin
val result = (inputValueDouble * inputConvertionFactor * 100 / outputConvertionFactor).roundToInt() / 100.0
```

</details>
<br>


### 🌱 Drop-Down Menús para las unidades de salida.
Usamos menús desplegables para seleccionar las unidades de origen y destino. Es el momento de cambiar el código para cuando se selecciona una unidad de destino y que la aplicación recalcule automáticamente el valor convertido para mantener la coherencia y usabilidad de la interfaz. El código es muy parecido al evento onClick de los DropdownItem de las unidades de origen.

<details>
  <summary>¿Te atreves a realizar la función?</summary>

Aunque solo te voy a dar la función onClick, de dropdownMenuItem de metros.

```kotlin
onClick = {
    outputExpanded = false
    outputUnit = "Centímetros"
    inputConvertionFactor = 0.01
    convertUnits()
}
```

Tendrás que hacer lo mismo para las otras unidades.
</details>
<br>

## 💡 Cambio del texto de los botones.

Como te habrás fijado, al seleccionar una unidad de origen o destino, el texto de los botones no cambia y es un problema de usabilidad. ¿No sería deseable que cambiara cuando se selecciona las unidades? 

Vamos a cambiar el texto de los botones para que muestren la unidad seleccionada.

<details>
  <summary>¿Te atreves?</summary>

Te pongo el ejemplo de solo un botón.

```kotlin
Button(onClick = { inputExpanded = true }) {
    Text(text = inputUnit)
    //....
}

```

</details>
<br>


## 🚀 Prueba la aplicación.

¿Hace bien los cálculos? ¿Cambia correctamente las unidades de origen y destino? ¿Cambia el texto de los botones?

Debe de haber un pequeño problema aún. Si seleccionas una unidad de origen y destino, y cambias el valor de entrada, el valor de salida no cambia. ¿Por qué crees que es?

¿Qué habría que hacer?

<details>
  <summary>Solución</summary>
<br> 

Debemos llamar a la función `convertUnits()` en el final del evento `onValueChange` del `OutlinedTextField`. De esta forma, cada vez que se cambie el valor de entrada, se recalculará el valor convertido.

```kotlin
onValueChange = {
    inputValue = it
    convertUnits()
}
```
</details>
<br>

## ✨ Modificando el Estilo de la App

Vamos a cambiar la aparencia gráfica de nuestra aplicación, ya que los textos que tenemos son un poco pequeños.

Para cambiar la apariencia de un texto en Jetpack Compose, puedes usar la propiedad `style` del componente **Text**.

Por ejemplo, si tienes un resultado que deseas mostrar más grande, puedes usar una de las opciones de tipografía disponibles en **MaterialTheme**.

Por ejemplo, vamos a modificar el tamaño del texto del resultado:

```kotlin
Text(
    text = outputValue,
    style = MaterialTheme.typography.headlineMedium
)
```
En este ejemplo, estamos usando `headlineMedium` para agrandar el texto y hacerlo más grande. Puedes probar otros estilos.

---

## 📐 Tipografía con MaterialTheme

**MaterialTheme** tiene una serie de estilos predefinidos para textos, tales como:

- **headlineSmall**, **headlineMedium**, **headlineLarge**: Tamaños para titulares.
- **labelSmall**, **labelMedium**, **labelLarge**: Tamaños para etiquetas.

Puedes usar estos estilos según el contexto de tu aplicación.

Por ejemplo, para un título principal podrías usar:

```kotlin
Text(
    text = "Conversor de Unidades",
    style = MaterialTheme.typography.headlineLarge
)
```
Esto hará que el título sea más grande y destacado.

---

## 🎨 Creando un Estilo de Texto Personalizado

Si deseas tener un estilo más específico, puedes crear un estilo personalizado usando **TextStyle**.

```kotlin
val customTextStyle = TextStyle(
    fontFamily = FontFamily.Monospace,
    fontSize = 32.sp,
    color = Color.Red
)
```

Nota: Seguramente tendrás que hacer muchas importaciones aquí.

Puedes colocar este valor justo después donde declaramos las variables de nuestro Composable y antes de la función para convertir las unidades.

Aunque lo puede sacar de la función.

Luego puedes aplicarlo a un componente **Text** de la siguiente manera:

```kotlin
Text(
    text = "Conversor de Unidades Personalizado",
    style = customTextStyle
)
```
Este ejemplo usa una fuente monoespaciada, con un tamaño de 32 SP y color rojo. Puedes experimentar con diferentes propiedades para obtener el estilo deseado.

---

## 📘 Recomendaciones sobre los estilos

[Hecho] No somos artistas ni diseñadores

- Siempre es buena idea seguir el lenguaje de diseño de **Material Theme** para mantener una apariencia consistente en tu aplicación.
- Puedes experimentar con distintos estilos y ver cuál se adapta mejor a la UX que quieres ofrecer.
- Es buena idea preguntar a una IA como `chatGPT` para que nos ayude con estas tareas de diseño.



