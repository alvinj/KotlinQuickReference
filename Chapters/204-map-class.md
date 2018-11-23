---
description: This page provides examples of the Kotlin 'Map' class, including how to add and remove elements from a Map, and iterate over Map elements.
---

<!--
TODO:
- adding
- updating
- removing
- clearing
- iterating over (for loop)
-->


# The Kotlin Map Class

This chapter introduces maps in Kotlin.



## Kotlin Map functions

Use these functions to create Maps in Kotlin:

| Function       | Type                  |
|----------------|-----------------------|
| `mapOf`        | `Map<K,V>`            |
| `hashMapOf`    | `HashMap<K, V>`       |
| `linkedMapOf`  | `LinkedHashMap<K, V>` |
| `sortedMapOf`  | `SortedMap<K, V>`     |
| `mutableMapOf` | `MutableMap<K, V>`    |

Kotlin also has `linkedStringMapOf` and `stringMapOf` functions for JavaScript.

Examples:

````
val map = mapOf("b" to 2, "a" to 1)          // {b=2, a=1}
val map = hashMapOf("b" to 2, "a" to 1)      // {a=1, b=2}
val map = linkedMapOf("b" to 2, "a" to 1)    // {b=2, a=1}
val map = sortedMapOf("b" to 2, "a" to 1)    // {a=1, b=2}
val map = mutableMapOf("b" to 2, "a" to 1)   // {b=2, a=1}
````


## Iterating over a map

Iterating over a map with `for`:

````
val map = mapOf("a" to 1, "b" to 2, "c" to 3)

for ((k,v) in map) {
     println("value of $k is $v")
}

// output
value of a is 1
value of b is 2
value of c is 3
````












