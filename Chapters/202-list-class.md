---
description: This page provides examples of the Kotlin List class, including how to add and remove elements from a List.
---

<!--
TODO:
- creating
- adding
- updating
- removing
- clearing
- iterating over (for loop)
-->

# The Kotlin List Class

This chapter introduces Kotlin lists. Some issues are:

- Mutable vs. immutable
- Handling null values
- Different types of lists

>Note: This chapter has a number of TODO items, but it currently shows how to create a variety of different list types.



## Creation functions

Use these functions to create lists in Kotlin:

| Function        | Type             |
|-----------------|------------------|
| `arrayListOf`   | `ArrayList<T>`   |
| `emptyList`     | `List<T>`        |
| `listOf`        | `List<T>`        |
| `listOfNotNull` | `List<T>`        |
| `mutableListOf` | `MutableList<T>` |

Examples:

````
val list = listOf(1, 2, 3)
val list = arrayListOf(1, 2, 3)
val list = mutableListOf("a", "b", "c")

// empty lists
val list = listOf<Int>()
val list = arrayListOf<Double>()
val list = mutableListOf<String>()
val list: List<Int> = emptyList()

// nullability (implicit or explicit)
val list = listOf("a", null)                  // [a, null]
val list: List<String?> = listOf("a", null)   // [a, null]

val list = arrayListOf("a", null)             // [a, null]
val list = mutableListOf("a", null)           // [a, null]
val list = listOfNotNull<String>("a", null)   // [a]
val list = listOfNotNull("a", null)           // [a]

// comparison: listOf vs listOfNotNull
val list = listOf("a", null)                  // [a, null]
val list = listOfNotNull("a", null)           // [a]
````

Per the [Kotlin docs](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/index.html), the difference between `listOf` and `listOfNotNull`:

- `listOf`: Returns an immutable list containing only the specified object element.
- `listOfNotNull`: Returns a new read-only list either of single given element, if it is not null, or empty list if the element is null.



## Understanding casting

Some examples of casting and explicitly declaring list types:

````
val a: List<Int>               = listOf(1,2,3)
val b: Collection<Int>         = listOf(1,2,3)
val c: Iterable<Int>           = listOf(1,2,3)

val a: MutableList<Int>        = mutableListOf(1,2,3)
val b: List<Int>               = mutableListOf(1,2,3)
val c: MutableCollection<Int>  = mutableListOf(1,2,3)
val d: Collection<Int>         = mutableListOf(1,2,3)
val e: Iterable<Int>           = mutableListOf(1,2,3)
val f: MutableIterable<Int>    = mutableListOf(1,2,3)

val a: ArrayList<Int>          = arrayListOf(1,2,3)
val b: AbstractList<Int>       = arrayListOf(1,2,3)
val c: MutableList<Int>        = arrayListOf(1,2,3)
val d: AbstractCollection<Int> = arrayListOf(1,2,3)
val e: MutableCollection<Int>  = arrayListOf(1,2,3)
val f: Collection<Int>         = arrayListOf(1,2,3)
val g: MutableIterable<Int>    = arrayListOf(1,2,3)
val h: Iterable<Int>           = arrayListOf(1,2,3)
val i: List<Int>               = arrayListOf(1,2,3)
````






