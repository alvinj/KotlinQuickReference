---
description: TODO
---

<!--
    TODO `as?`
    TODO `let`
    TODO nullability and generic types
    TODO nullability and java
-->


# Nullability Summary

Examples of working with nullable types:

````
// Nullable type
var s: String? = null


// Safe-call operator
val street2Address = order.customer?.address?.street2


// Elvis operator (1)
fun toUpper(s: String?): String = s?.toUpperCase() ?: "DUDE!"

// Elvis operator (2)
var p: Person? = null
p = Person("Alvin", null, "Alexander")
val mi = p?.mi ?: "<blank>"
println("mi = $mi")


// Force operator (1)
> val s1: String? = "Christina"
> val s2: String = s1!!
> s2
Christina

// Force operator (2)
> val s1: String? = null
> val s2: String = s1!!
kotlin.KotlinNullPointerException
````


## Nullability and collections (TODO)

````
listOfNotNull("a", "b", null)  //[a, b]
listOf("a", "b", null)         //[a, b, null]
````








