# 🐾 Manual Kotlin: Map, Copy, Let

En este pequeño manual vamos a explorar tres conceptos fundamentales en Kotlin: `map`, `copy` y `let`. Utilizaremos una data class de animales para ilustrar cada uno de estos conceptos. 🦁🐢🐶

## 📦 Data Class: Animal

Primero, creamos una data class llamada `Animal`. Esta clase representará diferentes animales, cada uno con un nombre y una edad.

```kotlin
// Definimos la data class Animal
data class Animal(val nombre: String, val edad: Int)

// Creamos una lista de animales
val animales = listOf(
    Animal("León", 8),
    Animal("Tortuga", 120),
    Animal("Perro", 5)
)
```

Ahora que tenemos la clase `Animal` definida y una lista de ejemplos, veamos cómo usar `map`, `copy` y `let`.

## 🗺️ Map

El operador `map` nos permite transformar cada elemento de una colección, aplicando una función a cada uno de ellos. Es muy útil cuando queremos crear una nueva lista a partir de otra, transformando sus elementos.

```kotlin
// Queremos obtener una lista con los nombres de todos los animales
val nombresAnimales = animales.map { it.nombre }
println(nombresAnimales) // Imprime: [León, Tortuga, Perro]
```

En este ejemplo, utilizamos `map` para obtener una lista que contiene únicamente los nombres de los animales. La función lambda `{ it.nombre }` se aplica a cada `Animal` en la lista original.

## 📋 Copy

El método `copy` es útil cuando queremos crear una copia de un objeto, pero cambiando uno o varios de sus atributos. Esto es especialmente relevante cuando trabajamos con objetos inmutables, como nuestras `data class`.

```kotlin
// Creamos una copia del perro pero cambiamos su edad
val perroViejo = animales[2].copy(edad = 10)
println(perroViejo) // Imprime: Animal(nombre=Perro, edad=10)
```

En el ejemplo, copiamos el objeto `Perro` pero cambiamos su edad a `10`. Esto nos permite mantener la inmutabilidad mientras hacemos modificaciones.

## ✨ Let

El operador `let` se usa para realizar operaciones en un objeto dentro de un contexto seguro, especialmente útil para evitar `null` o cuando queremos encadenar varias operaciones sobre un objeto.

```kotlin
// Usamos let para trabajar con un animal específico
animales[0].let {
    println("El animal es: ${it.nombre}")
    println("Tiene ${it.edad} años")
}
```

Con `let`, podemos acceder al objeto `León` y realizar varias operaciones dentro del bloque sin necesidad de repetir el nombre de la variable. Esto hace el código más limpio y conciso.

