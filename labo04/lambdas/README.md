# Funciones **Lambda** en Kotlin

# Fuentes
Adaptado del curso de Android Developers Codelabs: 

[Cómo usar tipos de funciones y expresiones lambda en Kotlin](https://developer.android.com/codelabs/basic-android-kotlin-compose-function-types-and-lambda)

# 📘 1. Introducción

Bienvenido al mundo de las funciones lambda en Kotlin. En este codelab, aprenderás sobre los tipos de funciones, cómo usarlas y la sintaxis específica de las expresiones lambda.

En Kotlin, las funciones se consideran construcciones de primera clase. Esto significa que las funciones se pueden tratar como un tipo de dato. Puedes almacenar funciones en variables, pasarlas a otras funciones como argumentos e incluso retornarlas desde otras funciones.

Al igual que otros tipos de datos que puedes expresar con valores literales, como el tipo `Int` con el valor `10` o el tipo `String` con el valor `"Hello"`, también puedes declarar literales de funciones, que se llaman **expresiones lambda**, o simplemente, **lambdas**. Las lambdas se usan mucho en el desarrollo de Android y, en general, en la programación en Kotlin. Así como otros leguajes de programación modernos, Kotlin permite que las lambdas sean más concisas y fáciles de leer.

## 📚 Qué aprenderás

- Cómo definir una función con sintaxis lambda.
- Cómo almacenar funciones en variables.
- Cómo pasar funciones como argumentos a otras funciones.
- Cómo devolver funciones desde otras funciones.
- Cómo usar tipos de funciones anulables.
- Cómo hacer que las expresiones lambda sean más concisas.
- Qué es una función de **orden superior**.
- Cómo usar la función `repeat()`.

## 🔧 Requisitos

- Android Studio ó
- Un navegador web con acceso a **Playground de Kotlin**.

# 2. Programando un "Truco o Trato" con Lambdas 🎃🍬

En este manual, aprenderás a usar los tipos de funciones y las expresiones lambda para crear un programa sencillo de "truco o trato". Puedes seguir escribiendo el código junto conmigo o simplemente leer y aplicar el conocimiento más tarde. 💡

Para comenzar, abre el **Playground de Kotlin** en [developer.android.com/training/kotlinplayground](https://play.kotlinlang.org/)

o en tu IDE de Android Studio.

## Definiendo la primera función: `trick` 🎃

Hasta ahora, no hemos tenido que declarar funciones usando la palabra clave `fun`. Empecemos activando la primera función para nuestro programa de truco o trato.

Primero, añadimos una nueva función llamada `trick` que mostrará el mensaje "¡No hay golosinas!":

```kotlin
fun trick() {
    println("¡No hay golosinas!")
}


fun main() {
    val trickFunction = trick // OJO! tiene un error
}
```

Ahora, ya que una función es como cualquier otro tipo de dato, deberíamos ser capaces de asignarla a una variable. Definamos una variable `val` llamada `trickFunction` y asignémosle la función `trick` usando el operador de referencia de funciones `::`:

```kotlin
fun main() {
    val trickFunction = ::trick // esta es la forma correcta de hacerlo
}
```

Si ejecutamos el código sin el operador de referencia, obtendremos un error de compilación. Para evitarlo, utilizamos `::trick` para referirnos a la función como valor.

## 💡 Convertir la función a una expresión lambda

Vamos a hacer el código más conciso convirtiendo la función `trick` en una expresión lambda. Para ello, simplemente quitamos la palabra clave `fun` y añadimos `val` en su lugar, quitamos los paréntesis y añadimos un símbolo igual:

```kotlin
val trick = {
    println("¡No hay golosinas!")
}
```

En la función `main`, ya no necesitamos el operador de referencia `::`, ya que ahora `trick` se refiere directamente a una variable. Podemos llamar a `trick` usando paréntesis:

```kotlin

fun main() {
    val trickFunction = trick
    trickFunction()
}

```

Al ejecutar el código, deberíamos ver el mensaje "¡No hay golosinas!".

## Añadiendo la función `treat` 🍬

Ahora que la función `trick` está lista, añadiremos la función `treat` como una expresión lambda. Esta variable será un poco más compleja, ya que recibirá un parámetro.

Podemos definir el tipo de la función de la siguiente manera:

```kotlin
val treat: (Int) -> String = { cantidad ->
    "Aquí tienes $cantidad golosinas!"
}
```

El tipo de la función se declara especificando el parámetro entre paréntesis, seguido por una flecha `->` y el tipo de retorno. En este caso, `treat` toma un parámetro `Int` y devuelve un `String`.

Cuando la función no recibe ningún parámetro los paréntesis irían vacíos, por ejemplo, `val trick: () -> Unit = { ... }`. 

Y cuando no devuelve nada se pondría `Unit` como tipo de retorno, por ejemplo, `val trick: () -> Unit = { println("¡No hay golosinas!") }`. Indicando que no hay devolución. Puedes probar con el siguiente código:

```kotlin
val trick: () -> Unit = {
    println("¡No hay golosinas!")
}
```

## 🔄 Creando una función de orden superior: `trickOrTreat`

Vamos a crear una nueva función llamada `trickOrTreat` que devuelva una función. Esta función aceptará un argumento booleano y retornará `trick` o `treat` dependiendo del valor del argumento:

```kotlin
fun trickOrTreat(esTruco: Boolean): () -> Unit {
    if (esTruco) {
        return trick
    } else {
       treat(8)
       return {}  // Encapsulamos la llamada a treat dentro de un lambda que devuelve Unit
    }
}
```

En la función `main`, podemos usar `trickOrTreat` para obtener una función y luego llamarla:

```kotlin
fun main() {
    val treatFunction = trickOrTreat(false)
    val trickFunction = trickOrTreat(true)
    
    treatFunction()
    trickFunction()
}
```

Al ejecutar el código, veremos la salida correspondiente según el valor pasado a `trickOrTreat`.

## 🎁 Añadiendo extras opcionales

¿No sería genial poder personalizar el programa para dar golosinas extra? Vamos a ampliar la función `trickOrTreat` añadiendo un segundo parámetro llamado `extraTreat`, que será una función que tome un parámetro `Int` y devuelva un `String`.

Podemos modificar la función de la siguiente manera:

```kotlin
fun trickOrTreat(esTruco: Boolean, extraTreat: (Int) -> String): () -> Unit {
    if (esTruco) {
        return trick
    } else {
        println(extraTreat(5))
        return treat
    }
}
```

???? Con este cambio, `extraTreat` se convierte en un parámetro opcional. Si se proporciona, lo usamos para dar golosinas adicionales; si no, mostramos el mensaje predeterminado.

## ✨ Sintaxis más concisa con `it`

Vamos a crear una función lambda en el main que devuelva un mensaje personalizado con la cantidad de monedas que se pasen como argumento.

```kotlin
fun main(){
    val coins: (Int) -> String = {
    cantidad ->"Aquí tienes $cantidad monedas."
    }
}
```

Fíjate que no se usa la palabra reservada `return` porque la función lambda devuelve el último valor que se evalúa.

Esta función lambda toma un parámetro `Int` y devuelve un `String`. Podemos simplificar la función lambda para que sea más concisa, usando la palabra clave `it`

```kotlin
fun main(){
    val coins: (Int) -> String = {
    "Aquí tienes $it monedas."
    }
}
```



Para hacer el código más conciso, podemos usar la palabra clave `it` cuando una lambda tiene un único parámetro. Esto hace que nuestro código sea más legible:

```kotlin
val coins: (Int) -> String = {
    "Aquí tienes $it monedas."
}
```

Vamos a crear otra función lambda llamda `cupcake` que recibe un entero, con el que no se hace nada, y devuelve un mensaje de "¡Aquí tienes una magdalena!".

```kotlin
val cupcake: (Int) -> String = {
    "¡Aquí tienes una magdalena!"
}
```

Podemos pasar esta lambda directamente como un argumento al llamar a la función `trickOrTreat`, con las dos funciones lambda que hemos creado:

```kotlin
val treatFuncion = trickOrTreat(false, coins)()
val trickFuncion = trickOrTreat(true, cupcake)()
```

Al ejecutar el código, veremos que se muestran las monedas correspondientes y el mensaje de la magdalena.

### ¿Se puede hacer que el parámetro se opcional?

En Kotlin, puedes hacer que un parámetro sea opcional añadiendo un valor por defecto. Por ejemplo, si queremos que `extraTreat` sea opcional, podemos añadir un valor por defecto a la función `trickOrTreat`:

```kotlin
fun trickOrTreat(esTruco: Boolean, extraTreat: ((Int) -> String)? = null): () -> Unit {
    if (esTruco) {
        return trick
    } else {
        // OJO! extraTreat puede ser null
        if (extraTreat != null) {
            println(extraTreat(5))
        }
        return treat
    }
}
```

Vamos  a probarlo con el siguiente código en el `main()`:

```kotlin
val treatFunction = trickOrTreat(false, coins)
val trickFunction = trickOrTreat(true, null)
```
### ¿Podemos hacerlo más preciso?

Si, podemos cambiar la declaración de la función `coins` para que sea más precisa. En lugar de usar `cantidad` como parámetro, podemos usar `it` para hacer que la función sea más concisa:

```kotlin
val coins: (Int) -> String = {
    "Aquí tienes $it monedas."
}
```

Si solo vamos a llamar a la función `coins` una vez, podemos hacer que la declaración sea más concisa. En lugar de declarar la función `coins` como una variable, podemos pasar la función directamente como argumento a `trickOrTreat`:

```kotlin
val treatFunction = trickOrTreat(false, { "Aquí tienes $it monedas." })
```
Y segiría funcionando correctamente. Pruébalo en el `main()`.
Y podemos hacerlo más legible todavía, usando la sintaxis de lambda más concisa, llamada **trailing lambda syntax**. 
Cuando es el último argumento de una función, podemos sacar la función lambda fuera de los paréntesis.

En lugar de pasar la función `coins` como argumento, podemos pasarla directamente como un bloque de código. 

```kotlin
val treatFunction = trickOrTreat(false) { "Aquí tienes $it monedas." }
```


## 🔄 Usando la función `repeat()`

La función `repeat()` es otra función de orden superior muy útil en Kotlin. Vamos a usarla para repetir el truco o el trato varias veces. Por ejemplo, si queremos repetir `treat` cuatro veces:

```kotlin
repeat(4) {
    treatFunction()
}
```

Esto ejecutará el `treatFunction()` cuatro veces.

## 7. Conclusión

Aprendiste los conceptos básicos de los tipos de funciones y las expresiones lambda. Estar familiarizado con estos conceptos te ayudará a obtener más información sobre el lenguaje Kotlin. El uso de tipos de funciones, funciones de orden superior y sintaxis abreviada también hace que tu código sea más conciso y fácil de leer.

### Resumen
- Las funciones en Kotlin son construcciones de primer nivel y se pueden tratar como tipos de datos.
- Las expresiones lambda proporcionan una sintaxis abreviada para escribir funciones.
- Puedes pasar tipos de funciones a otras funciones.
- Puedes devolver un tipo de función desde otra.
- Una expresión lambda devuelve el valor de la última expresión.
- Si se omite una etiqueta de parámetro en una expresión lambda con un solo parámetro, se hace referencia a ella con el identificador `it`.
- Las expresiones lambda se pueden escribir intercaladas sin un nombre de variable.
- Si el último parámetro de una función es un tipo de función, puedes usar la sintaxis lambda al final para mover la expresión lambda después del último paréntesis cuando llamas a una función.
- Las funciones de orden superior son funciones que toman otras funciones como parámetros o devuelven una función.
- La función `repeat()` es una función de orden superior que funciona de manera similar a un bucle `for`.


