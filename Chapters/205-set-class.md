---
description: This page provides examples of the Kotlin 'Set' class, including how to add and remove elements from a Set, and iterate over Set elements.
---

# Set

This chapter contains examples of how to create and use sets in Kotlin.



## Creating sets

Use these functions to create sets:

| Function       | Type               |
|----------------|--------------------|
| `setOf`        | `Set<T>`           |
| `hashSetOf`    | `HashSet<T>`       |
| `linkedSetOf`  | `LinkedHashSet<T>` |
| `sortedSetOf`  | `TreeSet<T>`       |
| `mutableSetOf` | `MutableSet<T>`    |

Kotlin also has `linkedStringSetOf` and `stringSetOf` functions for JavaScript.

Examples:

````
val set = setOf(3, 5, 1)          // [3, 5, 1]
val set = hashSetOf(3, 5, 1)      // [5, 1, 3]
val set = linkedSetOf(3, 5, 1)    // [3, 5, 1]
val set = sortedSetOf(3, 5, 1)    // [1, 3, 5]
val set = mutableSetOf(3, 5, 1)   // [3, 5, 1]
````



## TODO

Need examples of:

- adding elements
- updating elements
- removing elements
- clearing the set
- iterating over (for-loop)






