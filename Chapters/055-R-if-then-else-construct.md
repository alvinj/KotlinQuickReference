---
description: This page demonstrates Kotlin's if/then/else construct, including several examples you can try in the REPL.
---


# if/then/else

`if` statements in Kotlin are just like Java, with one exception: they are an expression, so they always return a result.



## Basic syntax

A basic Kotlin `if` statement:

````
if (a == b) doSomething()
````

You can also write that statement like this:

````
if (a == b) {
    doSomething()
}
````


## if/else

The `if`/`else` construct:

````
if (a == b) {
    doSomething()
} else {
    doSomethingElse()
}
````


## if/else-if/else

The complete Kotlin if/else-if/else expression looks like this:

````
if (test1) {
    doX()
} else if (test2) {
    doY()
} else {
    doZ()
}
````


## `if` expressions always return a result

The `if` construct always returns a result, meaning that you can use it as an expression. This means that you can assign its result to a variable:

````
val minValue = if (a < b) a else b
````

This means that Kotlin doesn’t require a special [ternary operator](https://alvinalexander.com/java/edu/pj/pj010018).





