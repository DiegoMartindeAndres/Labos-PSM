# Colecciones para Manejar Datos Dinámicos en el Mundo Real 🏭

## Introducción a las Colecciones en Kotlin 🛠✨

En Kotlin, una **colección** es una estructura de datos que nos permite **almacenar y manipular grupos de elementos** de manera eficiente. Estas colecciones pueden ser **mutables** o **inmutables**, dependiendo de si queremos permitir modificaciones después de su creación.

Exploraremos los diferentes tipos de colecciones en Kotlin y cómo se pueden utilizar para resolver diversos problemas. Veremos las colecciones principales: **listas**, **conjuntos** y **mapas**; además de algunas **colecciones especializadas**.

### 💾 Tipos de Colecciones en Kotlin
Las colecciones en Kotlin se dividen en varias categorías, cada una con sus propias características y usos. Las colecciones principales incluyen:
- **Listas (List)**: Almacenan elementos ordenados y pueden contener duplicados. Son útiles cuando se necesita un acceso secuencial o por índice a los elementos.
- **Conjuntos (Set)**: Almacenan elementos únicos, sin duplicados. Ideales para garantizar la unicidad de los elementos.
- **Mapas (Map)**: Almacenan pares clave-valor, permitiendo asociar información y acceder rápidamente a valores mediante claves.

Además, en Kotlin encontramos versiones **mutables** e **inmutables** de cada tipo de colección:
- **Colecciones Inmutables**: No pueden ser modificadas después de su creación, lo cual aumenta la seguridad y la consistencia de los datos.
- **Colecciones Mutables**: Permiten agregar, modificar o eliminar elementos después de la creación, siendo útiles cuando se requiere flexibilidad.

### 🛍️ Listas, Conjuntos y Mapas
- **Listas**: Permiten almacenar elementos en un orden específico y permiten duplicados. Son útiles cuando se necesita mantener un orden en los datos.
- **Conjuntos**: Almacenan elementos únicos, sin duplicados. Existen variantes como `HashSet` (sin orden específico) y `LinkedHashSet` (mantiene el orden de inserción).
- **Mapas**: Almacenan pares clave-valor, lo cual es ideal para asociar información entre claves y valores. Existen variantes como `HashMap` (sin orden específico) y `TreeMap` (mantiene las claves ordenadas).

### 🛠️ Colecciones Especializadas
Kotlin también ofrece colecciones especializadas que permiten manejar datos de manera eficiente para casos específicos:
- **ArrayList**: Una lista basada en un array dinámico, eficiente para acceso por índice y para colecciones que cambian frecuentemente de tamaño.
- **HashSet**: Un conjunto que utiliza una tabla hash, ideal para almacenar elementos únicos sin preocuparse del orden.
- **LinkedHashSet**: Similar a `HashSet`, pero mantiene el orden de inserción de los elementos.

### 📌 Colecciones Mutables e Inmutables
Como mencionamos, las colecciones en Kotlin pueden ser **mutables** o **inmutables**:
- Las **colecciones inmutables** son ideales cuando no queremos que los datos cambien, lo cual aumenta la seguridad y la consistencia.
- Las **colecciones mutables** son útiles cuando necesitamos modificar los elementos a lo largo del tiempo.

Elegir entre una colección mutable o inmutable dependerá de los requisitos del problema que estés resolviendo.


### Diferencia entre `val`/`var` y Colecciones Mutables/Inmutables ⚠️

Es importante aclarar que la diferencia entre **colecciones mutables e inmutables** no es lo mismo que declarar una variable como **`val`** o **`var`**. Aunque ambas características están relacionadas con la mutabilidad, se refieren a conceptos distintos en Kotlin.

#### `val` y `var`
- **`val`**: Una variable declarada con `val` es **inmutable**, lo que significa que la **referencia** a la colección no puede ser reasignada. Sin embargo, si la colección es mutable, los elementos dentro de la colección pueden ser modificados.
- **`var`**: Una variable declarada con `var` es **mutable**, lo que significa que se puede **reasignar** la referencia de la colección, permitiendo cambiar la colección por completo.

#### Colecciones Mutables e Inmutables
- **Colecciones Inmutables**: No permiten agregar, eliminar o modificar sus elementos una vez creadas. Son ideales cuando se necesita asegurar la **consistencia** de los datos y evitar modificaciones accidentales.
- **Colecciones Mutables**: Permiten agregar, eliminar o modificar elementos en cualquier momento. Son útiles cuando necesitamos flexibilidad y los elementos de la colección van a cambiar a lo largo del tiempo.

#### Ejemplo para Aclarar la Diferencia
Supongamos que tenemos una lista de nombres de estudiantes:

```kotlin
val listaMutable = mutableListOf("Héctor", "Pablo")
listaMutable.add("Diego")  // Esto está permitido, ya que la lista es mutable

val listaInmutable = listOf("Matías", "Diego")
// listaInmutable.add("Pablo")  // Esto no está permitido, ya que la lista es inmutable

var listaReasignable = listOf("César")
listaReasignable = listOf("Alfredo", "Dimitar")  // Esto está permitido, ya que `var` permite reasignación
```
En este ejemplo:
- **`listaMutable`**: Es una lista mutable que se declara con `val`. Podemos modificar los elementos (agregar/eliminar) de la lista, pero no podemos reasignar `listaMutable` a otra lista.
- **`listaInmutable`**: Es una lista inmutable, por lo que no permite modificaciones de sus elementos.
- **`listaReasignable`**: Es una lista inmutable declarada con `var`. No podemos modificar los elementos de la lista, pero sí podemos reasignar la variable a otra lista completamente diferente.

Esta distinción es crucial para entender cómo gestionar correctamente la **inmutabilidad** y la **reasignación** en Kotlin, y elegir la mejor opción según las necesidades de tu aplicación.

--------------------

## Listas
Vamos a aprender cómo usar **listas en Kotlin** para gestionar datos de manera dinámica y flexible. Imaginemos que Pablo, un desarrollador de Android, está en una tienda comprando componentes para construir su PC de ensueño. A medida que Pablo va encontrando nuevos componentes, puede agregarlos o reemplazarlos en su lista de compras. Este ejemplo ilustra perfectamente la utilidad y flexibilidad de las listas en Kotlin. Vamos a recrear la aventura de Pablo en Kotlin, modelando su lista de compras.

## 🛋️ Creando una Lista Inmutable
Primero, vamos a ver cómo crear una lista básica en Kotlin. Las listas **inmutables** no se pueden modificar después de su creación, lo cual puede ser útil si no queremos que la información cambie:

``` kotlin
val shoppingList = listOf("Processor", "RAM", "Graphics Card", "SSD")

println(shoppingList)
```

- **`listOf`** crea una lista inmutable.
- Al ser **inmutable**, no podemos añadir, quitar o modificar elementos de la lista después de su creación.

Por ejemplo, si intentamos hacer `shoppingList.add("Cooling System")`, obtendremos un error porque la lista no se puede modificar. Puedes probarlo tú mismo.


[👀 Revisa la documentación de las listas.](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-list/)

## 🔥 Listas Mutables: Añadiendo y Modificando Elementos
Para resolver esta limitación, podemos usar una **lista mutable** que nos permita añadir o eliminar elementos según sea necesario:

``` kotlin
val shoppingList = mutableListOf("Processor", "RAM", "Graphics Card", "SSD")

// Añadir un nuevo componente
shoppingList.add("Cooling System")

// Reemplazar la tarjeta gráfica con una mejor
shoppingList.remove("Graphics Card")
shoppingList.add("RTX 4090")

println(shoppingList)
```

### Explicación del Código
- **`mutableListOf`** nos permite crear una lista que **puede ser modificada** después de su creación.
- **`add()`** se utiliza para añadir un nuevo elemento a la lista.
- **`remove()`** elimina un elemento de la lista. Podemos eliminarlo por su valor o por su índice.

## 🤖 Métodos de las Listas
En Kotlin, los métodos para manipular listas (como `add()`, `remove()`, etc.) son conocidos como **métodos de instancia** o **métodos de objeto**. Esto se debe a que, en Kotlin, todo es un **objeto**, y los métodos son funciones que pertenecen a esos objetos. 

Pero OJO! estos son los métodos básicos, obviamente una lista mutable tiene muchos más métodos que podemos utilizar. ¿Dónde podemos encontrar esa información?

<details>
  <summary>Pincha aquí para conocer la solución.</summary>

Pues en la documentación oficial de Kotlin, en la sección de [Listas](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/). Allí encontrarás todos los métodos disponibles para las listas mutables en Kotlin.

</details>
<br>

### Imprimiendo la Lista
Podemos imprimir la lista de compras para ver los cambios realizados:

``` kotlin
println(shoppingList)
```

Esto mostrará:
```
[Processor, RAM, SSD, Cooling System, RTX 4090]
```
Notarás que los elementos se agregan al final de la lista de forma predeterminada.
 
# Trabajando con Índices en Listas 📋

## Introducción
Nos vamos a enfocar en los **índices** dentro de las listas, que nos permiten acceder y manipular elementos específicos de manera más precisa. Vamos a aprender cómo funcionan los índices en Kotlin y cómo se pueden utilizar para manipular nuestra lista de compras de componentes de PC.

## 🔢 ¿Qué es un Índice?
En programación, un **índice** representa la posición de un elemento dentro de una lista o un array. En Kotlin, al igual que en la mayoría de los lenguajes de programación, los índices comienzan desde **cero**. Esto significa que el primer elemento de una lista está en la posición 0, el segundo en la posición 1, y así sucesivamente.

### Ejemplo de Índices
Consideremos la siguiente lista:

```kotlin
val shoppingList = mutableListOf("Processor", "RAM", "SSD", "Cooling System", "Graphics Card")
```

En esta lista:
| Índice | Componente        |
|--------|-------------------|
| 0      | Processor         |
| 1      | RAM               |
| 2      | SSD               |
| 3      | Cooling System    |
| 4      | Graphics Card     |


## 🔍 Accediendo a Elementos por Índice
Podemos acceder a un elemento específico de la lista utilizando su índice. Por ejemplo, si queremos obtener el segundo elemento (`RAM`), podemos hacerlo de la siguiente manera:

```kotlin
val item = shoppingList[1]
println(item)  // Salida: RAM
```

### Modificando un Elemento por Índice
También podemos **modificar** un elemento de la lista usando su índice. Supongamos que queremos actualizar el `SSD` a `NVMe SSD`:

```kotlin
shoppingList[2] = "NVMe SSD"
println(shoppingList)  // Salida: [Processor, RAM, NVMe SSD, Cooling System, Graphics Card]
```

## 🗑️ Eliminando Elementos con `removeAt()`
Si necesitamos eliminar un elemento en una posición específica, podemos utilizar el método `removeAt()`, que elimina el elemento en el índice dado. Por ejemplo, eliminemos el `SSD`:

```kotlin
shoppingList.removeAt(2)
println(shoppingList)  // Salida: [Processor, RAM, Cooling System, Graphics Card]
```

Como podemos ver, el elemento en el índice `2` (`SSD`) ha sido eliminado de la lista.

## ➕ Añadiendo Elementos en una Posición Específica
Podemos añadir un elemento en una **posición específica** utilizando el método `add(index, element)`. Si queremos añadir `RAM` nuevamente después del `Cooling System`, podemos hacerlo de la siguiente manera:

```kotlin
shoppingList.add(3, "RAM")
println(shoppingList)  // Salida: [Processor, RAM, Cooling System, RAM, Graphics Card]
```

## 🧠 Buenas Prácticas con Índices
- **Comienza a Contar desde Cero**: Es importante recordar siempre que los índices empiezan desde `0`. Esto es fundamental para evitar errores de "índice fuera de rango".
- **Uso de Métodos de Lista**: Métodos como `add()`, `removeAt()`, y la asignación directa (`shoppingList[index] = elemento`) son herramientas poderosas para manipular listas. Utilízalos sabiamente para mantener un código claro y conciso.

## Dudas existenciales. 🤔
¿Qué ocurre si tienes una lista de 5 elementos y tratas de añadir en la posición 10?

¿Qué ocurre si tienes una lista de 5 elementos y tratas de eliminar el elemento de la posición 10?


<details>
  <summary>Solo hay una manera de averiguarlo.</summary>

Pruébalo tú mismo y observa qué sucede. ¡La práctica es la mejor manera de aprender!

</details>
<br>


[👀 Revisa la documentación de las listas mutables.](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/)
 
# Modificando Listas con el Método `set()` 🛠️

## Introducción
Hemos visto como acceder y modificar elementos en listas utilizando índices. Ahora vamos a ver otra manera de modificar nuestras listas: el método **`set()`**. Este método nos permite reemplazar un elemento existente en una posición específica de la lista con un nuevo valor. Aprenderemos cómo usarlo y cuándo puede ser útil.

Primero de todo mira la documentación del método [set](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/set.html).

## 🔄 ¿Qué es el Método `set()`?
El método **`set()`** de Kotlin nos permite actualizar un elemento en una lista mutable. Con `set()`, podemos reemplazar el valor en un índice específico por otro nuevo. Es otra forma de modificar listas, similar al uso de la notación de corchetes (`[]`), pero con una sintaxis ligeramente diferente.

### Ejemplo Básico del Método `set()`
Consideremos la siguiente lista de compras de componentes de PC:

```kotlin
val shoppingList = mutableListOf("Processor", "Cooling System", "RAM", "Graphics Card")
```

Supongamos que queremos reemplazar el `Cooling System` por `Water Cooling`. Podemos usar el método `set()` para hacerlo:

```kotlin
shoppingList.set(1, "Water Cooling")
println(shoppingList)  // Salida: [Processor, Water Cooling, RAM, Graphics Card]
```

En este ejemplo, el elemento en el índice `1` (`Cooling System`) ha sido reemplazado por **`Water Cooling`**.

## 🔄 Modificando Elementos con la Notación de Corchetes
Otra forma de modificar elementos en una lista es utilizando la **notación de corchetes (`[]`)**. Por ejemplo, para cambiar el `Graphics Card` por `Radeon RX 7800 XT`:

```kotlin
shoppingList[3] = "Radeon RX 7800 XT"
println(shoppingList)  // Salida: [Processor, Water Cooling, RAM, Radeon RX 7800 XT]
```

Kotlin permite ambas formas de modificar listas, pero según la versión y el estilo de código, la notación de corchetes suele ser preferida por su simplicidad. Sin embargo, ambas son igualmente válidas y efectivas.

## 🤔 ¿Cuál Usar: `set()` o `[]`?
- **`set()`** y **`[]`** son funcionalmente equivalentes. Ambos permiten reemplazar un elemento de la lista en un índice específico.
- La elección entre uno u otro depende del **estilo de programación** y las **preferencias del equipo**. Kotlin tiende a preferir la notación de corchetes (`[]`) por ser más concisa, pero `set()` puede ser útil cuando se busca mayor claridad en el propósito de la función.

## 📝 Ejercicio: Modificando Elementos con `set()`
Prueba modificar los elementos de una lista usando ambos métodos. Por ejemplo, considera la lista `shoppingList` e intenta:
1. Reemplazar `Processor` por `AMD Ryzen 9` usando `set()`.
2. Cambiar `RAM` por `32GB DDR5` usando la notación de corchetes.

 
# Verificando Elementos en una Lista con `contains()` 🔍

## Introducción
Vamos a aprender sobre el método **`contains()`** en Kotlin. Este método nos permite verificar si una lista contiene un elemento particular. Es una función extremadamente útil cuando necesitamos validar la presencia de un elemento antes de realizar alguna acción. Vamos a explorar cómo usar `contains()` y qué tipo de resultados podemos esperar.

No olvides revisar la documentación del método [contains](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/contains.html).

## 🔎 ¿Qué es el Método `contains()`?
El método **`contains()`** se utiliza para comprobar si una lista contiene un elemento específico. Devuelve un **valor booleano** (`true` o `false`), dependiendo de si el elemento está presente en la lista o no.

### Sintaxis del Método `contains()`
Consideremos la siguiente lista de compras de componentes de PC:

``` kotlin
val shoppingList = mutableListOf("Processor", "RAM", "SSD", "Cooling System", "Graphics Card")
```

Supongamos que queremos verificar si el elemento `RAM` está presente en la lista:

```kotlin
val hasRAM = shoppingList.contains("RAM")
println(hasRAM)  // Salida: true
```

En este ejemplo, el método `contains()` verifica si **`RAM`** está en `shoppingList`. Como `RAM` está presente, el resultado es **`true`**.

## 🚪 Uso del Método `contains()` en una Condición
Podemos usar `contains()` dentro de una estructura condicional para tomar decisiones basadas en la presencia de un elemento:

```kotlin
if (shoppingList.contains("RAM")) {
    println("RAM is in the shopping list!")
} else {
    println("No RAM in the shopping list.")
}
```

En este ejemplo, el programa verificará si `RAM` está en la lista y, dependiendo del resultado, imprimirá el mensaje correspondiente.

## 🔮 Simplificando con `contains()` en Condiciones
En lugar de almacenar el resultado en una variable, también podemos usar `contains()` directamente en la condición:

```kotlin
if (shoppingList.contains("Graphics Card")) {
    println("Graphics Card is in the shopping list!")
} else {
    println("No Graphics Card in the shopping list.")
}
```

Esto nos permite hacer el código más conciso y directo.

## 👉 Ejercicio: Verificando Elementos en la Lista
Prueba utilizar el método `contains()` para verificar la presencia de otros componentes en la lista. Por ejemplo, intenta:
1. Verificar si `Processor` está presente.
2. Verificar si `Water Cooling` está presente y mostrar un mensaje acorde.

 
# Iterando Sobre Listas con Bucles `for` ➡️

## Introducción
Vamos a utilizar bucles `for` para **iterar sobre listas** en Kotlin. Un bucle `for` nos permite realizar una acción sobre cada elemento de una lista, lo cual es útil cuando necesitamos procesar o manipular datos de manera repetitiva. Aprenderemos cómo utilizar `for` para recorrer una lista y ejecutar código sobre cada uno de sus elementos.

## 🔁 Bucles `for` en Kotlin
Los bucles `for` se utilizan para **recorrer** los elementos de una lista. En cada iteración, el bucle selecciona un elemento y ejecuta el bloque de código asociado. La sintaxis es muy simple y directa.

Consideremos la siguiente lista de componentes para armar una PC:

```kotlin
val shoppingList = mutableListOf("Processor", "Cooling System", "RAM", "Graphics Card")
```

Podemos usar un bucle `for` para imprimir cada elemento de la lista:

```kotlin
for (item in shoppingList) {
    println(item)
}
// Salida:
// Processor
// Cooling System
// RAM
// Graphics Card
```

En este ejemplo, el bucle **itera** sobre cada elemento de `shoppingList` y lo imprime en la consola.

## 🏒 Interrumpiendo el Bucle con `break`
Podemos utilizar la palabra clave **`break`** para **interrumpir** el bucle cuando se cumpla una condición determinada. Por ejemplo, si deseamos imprimir los elementos hasta encontrar `RAM`:

```kotlin
for (item in shoppingList) {
    if (item == "RAM") {
        break
    }
    println(item)
}
// Salida:
// Processor
// Cooling System
```

En este ejemplo, el bucle se detendrá cuando encuentre `RAM`, dejando de imprimir el resto de los elementos.

## ➔ Eliminando Elementos Dentro de un Bucle
También podemos realizar otras acciones dentro del bucle, como eliminar elementos de la lista. Por ejemplo, si queremos **eliminar el último elemento** una vez que encontremos `RAM`:

```kotlin
for (item in shoppingList) {
    if (item == "RAM") {
        shoppingList.removeLast()
        break
    }
}
println(shoppingList)
// Salida: [Processor, Cooling System, RAM]
```

Aquí, el bucle recorre la lista y, una vez que encuentra `RAM`, elimina el último elemento de la lista (`Graphics Card`).

## 🎓 Ejercicio: Iterando y Modificando
Intenta recorrer la lista `shoppingList` y realiza las siguientes acciones:
1. Imprime cada elemento hasta encontrar `Cooling System`.
2. Cuando encuentres `Cooling System`, agrega `Water Cooling` después de él.

 
# Obteniendo el Índice de un Elemento en un Bucle `for` 🌐

## Introducción
Vamos a obtener el índice de un elemento en un bucle `for` en Kotlin. Conocer el índice de un elemento puede ser útil cuando necesitamos hacer referencia a su posición o modificar la lista en función de esa información. Exploraremos diferentes formas de usar bucles `for` para acceder tanto a los elementos como a sus índices.

## 🔎 Iterando con Índices
Una forma de recorrer una lista y obtener el índice de cada elemento es usando un bucle `for` que utilice el rango de índices de la lista. Veamos un ejemplo con una lista de compras:

```kotlin
val shoppingList = mutableListOf("Processor", "Cooling System", "RAM", "Graphics Card")

for (index in 0 until shoppingList.size) {
    println("Item \${shoppingList[index]} está en el índice \${index}")
}
// Salida:
// Item Processor está en el índice 0
// Item Cooling System está en el índice 1
// Item RAM está en el índice 2
// Item Graphics Card está en el índice 3
```

En este ejemplo, utilizamos **`0 until shoppingList.size`** para iterar sobre los índices desde `0` hasta el tamaño de la lista (excluyendo el valor final). Esto nos permite acceder a cada elemento de la lista a través de su índice.

## 🔒 Entendiendo `shoppingList.size`
El método **`shoppingList.size`** devuelve la cantidad de elementos que hay en la lista. Si nuestra lista tiene cuatro elementos, `shoppingList.size` devolverá `4`. Sin embargo, como los índices comienzan desde `0`, el último índice será `3`. Por eso utilizamos `until` para asegurarnos de no acceder a un índice fuera de rango.

## ✅ Modificando Elementos Usando Índices
Obtener el índice de un elemento también nos permite modificar elementos específicos dentro de la lista. Por ejemplo, si queremos cambiar el valor del elemento en el índice `1`:

```kotlin
shoppingList[1] = "Water Cooling"
println(shoppingList)
// Salida: [Processor, Water Cooling, RAM, Graphics Card]
```

En este ejemplo, reemplazamos **"Cooling System"** por **"Water Cooling"** usando su índice.

## ➕ Iterando con `indices`
Otra forma conveniente de recorrer los índices de una lista es usando la propiedad **`indices`** de la lista.
Puede parecer que la propiedad **`indices`** suene a español, pero el plural de **index** en inglés es **indices** o **indexes**.

```kotlin
for (index in shoppingList.indices) {
    println("Item \${shoppingList[index]} está en el índice \${index}")
}
```

Este enfoque es más legible y nos permite evitar calcular manualmente el rango de índices.


## Conjuntos (Sets): Una Colección Sin Duplicados 🧑‍🥥🧑‍🥥

Ahora vamos a explorar cómo utilizar **conjuntos en Kotlin**. A diferencia de las listas, los conjuntos no permiten elementos duplicados, lo que los hace ideales cuando necesitamos garantizar que cada elemento sea único. Vamos a ver cómo funcionan los conjuntos inmutables y mutables en Kotlin, ilustrándolo con ejemplos.

### 🎲 Creando un Conjunto Inmutable
Un **conjunto inmutable** es una colección cuyos elementos no se pueden modificar una vez que ha sido creada. Imagina que Héctor está organizando una conferencia y necesita mantener una lista única de asistentes sin permitir duplicados.

```kotlin
val attendees = setOf("Héctor", "Pablo", "Matías", "Diego")

println(attendees)
```

### Explicación del Código
- **`setOf()`** crea un conjunto inmutable.
- Los elementos del conjunto no están ordenados y no se pueden modificar después de su creación.

Este conjunto garantizará que cada asistente se registre una única vez. Si intentamos añadir a un asistente duplicado, Kotlin lo ignorará silenciosamente.

### 🔍 Verificando la Presencia de un Elemento
Podemos utilizar el método **`contains()`** para verificar si un elemento está presente en el conjunto:

```kotlin
val isDiegoAttending = attendees.contains("Diego")
println(isDiegoAttending)  // Salida: true
```

### Métodos Adicionales en los Conjuntos Inmutables
Los conjuntos inmutables comparten muchos métodos con las listas, pero con la restricción de no permitir modificaciones. Métodos como **`size`**, **`isEmpty()`**, y **`contains()`** son comunes y útiles para trabajar con conjuntos.


[👀 Revisa la documentación de los conjuntos inmutables.](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-set/)

---

## Conjuntos Mutables: Añadiendo y Eliminando Elementos 🚀

Si necesitamos un conjunto que permita la **modificación** de sus elementos, podemos usar un **conjunto mutable** (`MutableSet`). Sigamos con el ejemplo anterior, pero ahora permitamos que Héctor pueda agregar y quitar asistentes de la lista de manera dinámica.

```kotlin
val mutableAttendees = mutableSetOf("Héctor", "Pablo", "Matías")

// Añadir un nuevo asistente
mutableAttendees.add("Daniel")

// Intentar añadir un asistente que ya está en el conjunto
mutableAttendees.add("Pablo")  // Esto no añadirá un duplicado

// Eliminar un asistente
mutableAttendees.remove("Matías")

println(mutableAttendees)
```

### Explicación del Código
- **`mutableSetOf()`** crea un conjunto **mutable** que puede ser modificado después de su creación.
- **`add()`** permite agregar nuevos elementos al conjunto, siempre y cuando no sean duplicados.
- **`remove()`** elimina un elemento del conjunto.

Al imprimir el conjunto, observarás que no hay duplicados y que los elementos se han modificado según las operaciones realizadas:

```
[Héctor, Pablo, Daniel]
```

### 🛠️ Métodos Útiles de `MutableSet`
- **`add()`**: Añade un nuevo elemento si no está presente.
- **`remove()`**: Elimina un elemento del conjunto si está presente.
- **`clear()`**: Elimina todos los elementos del conjunto, dejándolo vacío.
- **`isEmpty()`**: Verifica si el conjunto está vacío.

Los conjuntos mutables son muy útiles cuando necesitamos garantizar la **unicidad** de los elementos y, al mismo tiempo, permitir modificaciones en la colección.

### 🎓 Ejercicio: Trabajando con `MutableSet`
1. Crea un conjunto mutable con los nombres de "Andrés", "Diego" y "Mario".
2. Añade a "Dimitar" al conjunto.
3. Intenta añadir nuevamente a "Diego" y observa qué sucede.
4. Elimina a "Mario" del conjunto y verifica el resultado.

Practicar con conjuntos te ayudará a entender mejor cómo funcionan las colecciones en Kotlin y cómo elegir la estructura adecuada según el problema que necesites resolver.

[👀 Revisa la documentación de los conjuntos mutables.](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-set/)


---

## Recorrer los Elementos de un Conjunto 🔄

Al igual que en las listas, podemos **recorrer los elementos de un conjunto** en Kotlin utilizando un bucle `for`. Veamos cómo hacerlo y algunas consideraciones importantes.

### 🔁 Iterando Sobre un Conjunto
Podemos utilizar un bucle `for` para recorrer todos los elementos de un conjunto y realizar alguna acción sobre cada uno de ellos. Supongamos que queremos imprimir la lista de asistentes al evento de Héctor:

```kotlin
val attendees = setOf("Héctor", "Pablo", "Matías", "Diego")

for (attendee in attendees) {
    println(attendee)
}
```

### Explicación del Código
- El bucle **`for (attendee in attendees)`** recorre cada elemento del conjunto `attendees` y lo imprime.
- A diferencia de las listas, los elementos del conjunto no tienen un **orden garantizado**, por lo que el orden de impresión puede variar.

### ❓ ¿Por Qué No Podemos Usar un `for` con Índices?
A diferencia de las listas, los conjuntos **no tienen índices**. Esto se debe a que los conjuntos son una colección **no ordenada**, es decir, no se garantiza un orden específico para los elementos. Mientras que en una lista podemos acceder a un elemento usando su posición (índice), en un conjunto no hay una posición fija para los elementos. Por esta razón, no podemos usar un bucle `for` con índices para recorrer un conjunto.

En su lugar, simplemente iteramos sobre cada elemento sin necesidad de conocer su posición. Esto asegura que trabajamos correctamente con la naturaleza **no ordenada** de los conjuntos.

### 🎓 Ejercicio: Recorrer un `MutableSet`
1. Crea un `mutableSet` con los nombres de "Alfredo", "Dimitar", "Daniel" y "César".
2. Utiliza un bucle `for` para imprimir cada elemento del conjunto.
3. Observa que el orden de los elementos puede variar cada vez que ejecutes el programa.


## Mapas en Kotlin: Colecciones Clave-Valor 💻🛠

En Kotlin, los **mapas** (tambén conocidos como **diccionarios**) son una colección de pares **clave-valor**. Son útiles cuando necesitamos almacenar relaciones entre objetos, como asociar los nombres de alumnos con sus notas o roles. Vamos a explorar cómo funcionan los mapas inmutables y mutables en Kotlin, y cómo aprovecharlos para resolver problemas prácticos.

### 🛂 Creando un Mapa Inmutable
Primero, vamos a crear un **mapa inmutable**. Supongamos que Diego quiere asociar a cada alumno con el rol que tendrá durante una actividad en clase.

```kotlin
val roles = mapOf(
    "Héctor" to "Líder",
    "Pablo" to "Secretario",
    "Matías" to "Gestor",
    "Diego" to "Moderador"
)

println(roles)
```

### Explicación del Código
- **`mapOf()`** crea un mapa inmutable, lo que significa que no podemos modificar los pares clave-valor una vez que se han definido.
- Cada par se especifica utilizando la sintaxis **`clave to valor`**.

Al imprimir el mapa, veremos todos los pares clave-valor:
```
{Héctor=Líder, Pablo=Secretario, Matías=Gestor, Diego=Moderador}
```

[👀 Revisa la documentación de los mapas inmutables.](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-map/)

### 🔍 Accediendo a Valores por su Clave
Podemos acceder a los valores de un mapa utilizando la clave correspondiente. Por ejemplo, si queremos saber el rol de Pablo:

```kotlin
val roleOfPablo = roles["Pablo"]
println(roleOfPablo)  // Salida: Secretario
```

---

## Mapas Mutables: Modificando Claves y Valores 🚀

Si necesitamos un mapa que permita **modificar** los pares clave-valor, podemos usar un **mapa mutable** (`MutableMap`). Ahora imaginemos que Diego decide actualizar algunos roles durante la actividad.

```kotlin
val mutableRoles = mutableMapOf(
    "Héctor" to "Líder",
    "Pablo" to "Secretario",
    "Matías" to "Gestor"
)

// Añadir un nuevo rol
mutableRoles["Daniel"] = "Observador"

// Cambiar el rol de Matías
mutableRoles["Matías"] = "Ayudante"

// Eliminar un rol
mutableRoles.remove("Pablo")

println(mutableRoles)
```

### Explicación del Código
- **`mutableMapOf()`** crea un mapa **mutable**, lo que nos permite modificar los pares clave-valor.
- Podemos usar la sintaxis **`mapa[clave] = valor`** para añadir o modificar un par clave-valor.
- **`remove()`** se utiliza para eliminar un par clave-valor del mapa.

Al imprimir el mapa, veremos los cambios realizados:
```
{Héctor=Líder, Matías=Ayudante, Daniel=Observador}
```

### 🛠️ Métodos útiles de `MutableMap`
- **`put(clave, valor)`**: Añade un nuevo par clave-valor o modifica el existente.
- **`remove(clave)`**: Elimina un par del mapa.
- **`clear()`**: Elimina todos los pares clave-valor del mapa.
- **`isEmpty()`**: Verifica si el mapa está vacío.

Los mapas mutables son útiles cuando necesitamos actualizar constantemente las relaciones entre datos, como los roles de los alumnos en una actividad.

[👀 Revisa la documentación de los mapas mutables.](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-map/)

---

## Recorrer los Elementos de un Mapa 🐞

Podemos **recorrer** todos los pares clave-valor de un mapa para realizar alguna acción sobre cada uno de ellos. Por ejemplo, si queremos imprimir los roles de cada alumno:

```kotlin
val roles = mapOf(
    "Héctor" to "Líder",
    "Pablo" to "Secretario",
    "Matías" to "Gestor",
    "Diego" to "Moderador"
)

for ((alumno, rol) in roles) {
    println("$alumno tiene el rol de $rol")
}
```

### Explicación del Código
- Utilizamos un bucle **`for ((clave, valor) in mapa)`** para recorrer cada par clave-valor.
- En cada iteración, se imprimen el nombre del alumno y su rol correspondiente.

Salida:
```
Héctor tiene el rol de Líder
Pablo tiene el rol de Secretario
Matías tiene el rol de Gestor
Diego tiene el rol de Moderador
```

---

## Complejidad Algorítmica de los Mapas 🤖

Los mapas en Kotlin ofrecen una **complejidad algorítmica** muy eficiente para las operaciones de inserción, búsqueda y eliminación de elementos.

### 📊 Complejidad de Operaciones
- **Inserción (`put`)**: La complejidad promedio es **O(1)**, ya que los mapas están implementados generalmente usando una **tabla hash** que permite acceder directamente a la ubicación de cada par clave-valor.
- **Búsqueda (`get`)**: La complejidad promedio también es **O(1)**, lo cual hace que la búsqueda de un valor a partir de una clave sea muy rápida.
- **Eliminación (`remove`)**: La complejidad promedio es **O(1)**, ya que también se basa en la localización rápida proporcionada por la tabla hash.

### ⚠️ Comparación con Listas y Conjuntos
- En una **lista**, para buscar o eliminar un elemento, la complejidad en el peor caso es **O(n)**, ya que se debe recorrer toda la lista para encontrar el elemento deseado.
- En un **conjunto** (`Set`), la complejidad para añadir, buscar o eliminar un elemento también suele ser **O(1)** en promedio, si está implementado con una tabla hash, como en el caso de **`HashSet`**.
- Sin embargo, los mapas son especialmente útiles cuando necesitamos asociar **pares clave-valor**, algo que no se puede hacer con una lista o un conjunto de forma directa.

### 🔥 Ventajas de los Mapas
Gracias a su **complejidad O(1)**, los mapas son muy eficientes para almacenar y recuperar datos cuando las **claves** son únicas y se necesita acceso rápido a los valores asociados. Esto los hace ideales para aplicaciones donde la rapidez y la unicidad de las claves son esenciales.

---

### 🎓 Ejercicio: Trabajando con `Map`
1. Crea un `mutableMap` con los nombres de "Manuel", "Alfredo", "Dimitar" y "David", asignando a cada uno un rol diferente.
2. Añade un nuevo alumno "Mario" con el rol de "Asistente".
3. Cambia el rol de "Dimitar" a "Coordinador".
4. Elimina a "Manuel" del mapa y verifica el resultado.

Practicar con mapas te ayudará a entender mejor las relaciones entre los elementos y cómo utilizar colecciones clave-valor en Kotlin.


## Colecciones Especializadas en Kotlin: Características y Usos 🛠️🌐

En este manual, vamos a explorar algunas de las colecciones especializadas en Kotlin. Estas colecciones ofrecen diferentes características y beneficios, según el problema que queramos resolver. A continuación, veremos una descripción breve de cada estructura: **ArrayList**, **HashSet**, **LinkedHashSet**, **SortedSet**, y **TreeMap**.

### 🛍️ ArrayList
**ArrayList** es una implementación de una lista mutable que utiliza un array dinámico como estructura subyacente.

- **Características**: Permite **duplicados** y mantiene el **orden de inserción** de los elementos.
- **Usos**: Es muy útil cuando necesitamos acceder a los elementos mediante índices o cuando se requiere una colección que cambie frecuentemente de tamaño.
- **Complejidad**: La inserción y la búsqueda por índice tienen una complejidad de **O(1)**, pero la inserción en cualquier índice que no sea el final tiene **O(n)**.
- **Ejemplo**:
  ```kotlin
  val students = arrayListOf("Héctor", "Pablo", "Matías")
  students.add("Diego")  // Añadir un nuevo alumno
  students.removeAt(1)    // Eliminar a "Pablo" según su índice
  println(students)       // Salida: [Héctor, Matías, Diego]
  ```

[👀 Revisa la documentación de los ArrayList](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-array-list/)

### 🥇 HashSet
**HashSet** es una implementación de un conjunto sin elementos duplicados, utilizando una **tabla hash** como estructura interna.

- **Características**: No permite **duplicados** y no garantiza el **orden de los elementos**.
- **Usos**: Ideal cuando necesitamos una colección de elementos únicos y el **orden no es importante**.
- **Complejidad**: Las operaciones de inserción, eliminación y búsqueda son generalmente **O(1)**.
- **Ejemplo**:
  ```kotlin
  val uniqueNames = hashSetOf("Héctor", "Pablo", "Matías")
  uniqueNames.add("Diego")
  uniqueNames.add("Héctor")  // No se añade porque ya está presente
  println(uniqueNames)          // Salida: [Héctor, Pablo, Matías, Diego]
  ```


[👀 Revisa la documentación de los HashSet](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-hash-set/)

### 📌 LinkedHashSet
**LinkedHashSet** es una variante de `HashSet` que mantiene el **orden de inserción** de los elementos.

- **Características**: No permite **duplicados** y **mantiene el orden** en el que los elementos se agregaron.
- **Usos**: útil cuando necesitamos almacenar elementos únicos y mantener el orden de inserción.
- **Complejidad**: Las operaciones de inserción, eliminación y búsqueda son **O(1)** en promedio.
- **Ejemplo**:
  ```kotlin
  val orderedNames = linkedSetOf("Matías", "Pablo", "Diego")
  orderedNames.add("Alfredo")
  println(orderedNames)  // Salida: [Matías, Pablo, Diego, Alfredo]
  ```

[👀 Revisa la documentación de los LinkedHashSet](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-linked-hash-set/)


---

### 🎓 Resumen
Estas colecciones especializadas en Kotlin nos permiten elegir la estructura adecuada según nuestras necesidades específicas:
- **ArrayList** para listas ordenadas y con acceso por índice.
- **HashSet** para conjuntos únicos sin preocuparse del orden.
- **LinkedHashSet** para conjuntos únicos con un orden de inserción.

Elegir la colección adecuada nos ayuda a escribir un código más eficiente y fácil de mantener. ¡Prueba cada una para ver cuál se adapta mejor a tus necesidades!