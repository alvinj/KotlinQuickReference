---
description: This page introduces Kotlin enumerations, and further shows how to create a complete OOP 'Pizza' class that uses those enumerations.
---

<!-- 
    TODO this lesson needs work, such as showing a Factory pattern example
-->


# Create Singletons with Object



## Key points

- Use `object` instead of `class` to create a singleton (single instance of that class)
- Useful for “utility” classes

Rules:

- No constructor parameters
- Can contain:
    - Properties
    - Functions
    - Initializer blocks
- Objects can inherit from interfaces and classes
- There is a difference between object *expressions* and *declarations*
    - Expressions are used on the right hand side of expressions
    - Declarations are when you use `object` to create a singleton or companion object



## Singleton example

````
object MathUtils {
    init {
        println("MathUtils init was called")
    }
    val ONE = 1
    fun plus1(i: Int) = i + 1
}

fun main(args: Array<String>) {
    val x = MathUtils.plus1(MathUtils.ONE)
    println(x)
}
````

Prints:

````
MathUtils init was called
2
````



## Inheritance

This is from the Kotlin Language Reference (TODO: write my own example):

````
// objects can have supertypes:
object DefaultListener : MouseAdapter() {
    override fun mouseClicked(e: MouseEvent) { ... }
    override fun mouseEntered(e: MouseEvent) { ... }
}
````


<!--
## Object expressions (TODO)

There are a few things you can do with the `object` keyword on the right hand side of an expression.

TODO: Write my own. This is from the Kotlin Language Reference:

````
// “just an object, with no trivial supertypes”
fun foo() {
    val adHoc = object {
        var x: Int = 0
        var y: Int = 0
    }
    print(adHoc.x + adHoc.y) 
}
````
-->







