---
description: This page provides an introduction to the Kotlin 'for' loop, including how to iterate over Scala collections.
---


# Kotlin `for` Loops

- `for` loops are similar to Java, but the syntax is different
- Unlike in Scala, Kotlin `for` loops are not expressions



## Basic syntax

Kotlin `for` loops have this basic syntax:

````
for (e in elements) { // do something with e ...}
````

For example, given a list:

````
val nums = listOf(1,2,3)
````

here’s a single-line algorithm:

````
for (n in nums) println(n)
````

The REPL shows how it works:

````
>>> for (n in nums) println(n)
1
2
3
````

You can also use multiple lines of code in your algorithm:

````
for (n in 1..3) {
    println(n)
}
````

Here are a couple of other examples:

````
// directly on listOf
for (n in listOf(1,2,3)) println(n)

// 1..3 creates a range
for (n in 1..3) println(n)
````



## Using `for` with Maps

You can also use a `for` loop with a Kotlin `Map` (which is similar to a Java `HashMap`). This is how you create a `Map` of movie names and ratings:

````
val ratings = mapOf(
    "Lady in the Water"  to 3.0, 
    "Snakes on a Plane"  to 4.0, 
    "You, Me and Dupree" to 3.5
)
````

Given that map, you can print the movie names and ratings with this `for` loop:

````
for ((name,rating) in ratings) println("Movie: $name, Rating: $rating")
````

Here’s what that looks like in the REPL:

````
>>> for ((name,rating) in ratings) println("Movie: $name, Rating: $rating")
Movie: Lady in the Water, Rating: 3.0
Movie: Snakes on a Plane, Rating: 4.0
Movie: You, Me and Dupree, Rating: 3.5
````

In this example, `name` corresponds to each *key* in the map, and `rating` is the name I assign for each *value* in the map.



## `for` is not an expression

If you’re coming to Kotlin from Scala, it’s important to note that `for` is NOT an expression. That means that code like this does not work:

````
// error
val x = for (n in 1..3) {
    return n * 2
}
````

<!-- TODO verify that (though it obviously fails in the repl) -->




