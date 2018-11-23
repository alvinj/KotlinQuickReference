---
description: This page introduces Kotlin enumerations, and further shows how to create a complete OOP 'Pizza' class that uses those enumerations.
---

<!-- WORKING, EARLY -->


# Create Singletons with Object



## Key points

- Use `object` instead of `class` to create a singleton
- Useful for “utility” classes
- Combines a class declaration with a single instance of that class

Rules:

- No constructor parameters
- Can contain:
    - Properties
    - Methods
    - Initializer blocks
- Can inherit from interfaces and classes



## Examples

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



object PizzaUtils {
    def addTopping(p: Pizza, t: Topping): Pizza = ...
    def removeTopping(p: Pizza, t: Topping): Pizza = ...
    def removeAllToppings(p: Pizza): Pizza = ...
}

Or this one:

object FileUtils {
    def readTextFileAsString(filename: String): Try[String] = ...
    def copyFile(srcFile: File, destFile: File): Try[Boolean] = ...
    def readFileToByteArray(file: File): Try[Array[Byte]] = ...
    def readFileToString(file: File): Try[String] = ...
    def readFileToString(file: File, encoding: String): Try[String] = ...
    def readLines(file: File, encoding: String): Try[List[String]] = ...
}
