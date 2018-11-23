---
description: This page shows how to write auxiliary Kotlin class constructors, including several examples of the syntax.
---

# Secondary Class Constructors


## Key points

Here are a few rules to know about Kotlin secondary class constructors:

- A class can have zero or more secondary class constructors
- A secondary constructor must call the primary constructor; this can happen by directly calling the primary constructor, or by calling another secondary constructor that calls the primary constructor
- You call other constructors of the same class with the `this` keyword
- The `@JvmOverloads` annotation lets Kotlin classes that have default parameter values be created in Java code



## Secondary constructor examples

Here’s an example that shows a primary constructor and two different auxiliary constructors:

````
class Pizza constructor (
    var crustSize: String,
    var crustType: String,
    val toppings: MutableList<String> = mutableListOf()
) {

    // secondary constructor (no-args)
    constructor() : this("SMALL", "THIN")

    // secondary constructor (2-args)
    constructor(crustSize: String, crustType: String) : this(crustSize, crustType, mutableListOf<String>())

    override fun toString(): String = "size: ${crustSize}, type: ${crustType}, toppings: ${toppings}"

}
````

This function and its output shows how the constructors work:

````
fun main(args: Array<String>) {
    val p1 = Pizza()
    val p2 = Pizza("LARGE", "THICK")
    val p3 = Pizza("MEDIUM", "REGULAR", mutableListOf("CHEESE", "PEPPERONI"))

    println(p1)
    println(p2)
    println(p3)
}

// output
size: SMALL, type: THIN, toppings: []
size: LARGE, type: THICK, toppings: []
size: MEDIUM, type: REGULAR, toppings: [CHEESE, PEPPERONI]
````



## Notes

Notice how default constructor values eliminate the need for secondary constructors like these. This code with default constructor parameter values produces the same results:

````
class Pizza2 constructor (
    var crustSize: String = "SMALL",
    var crustType: String = "THIN",
    val toppings: MutableList<String> = mutableListOf()
) {
    override fun toString(): String = "size: ${crustSize}, type: ${crustType}, toppings: ${toppings}"
}
````



# @JvmOverloads (Working with Java)

Per [the Kotlin documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.jvm/-jvm-overloads/index.html), the `@JvmOverloads` annotation “Instructs the Kotlin compiler to generate overloads for this function that substitute default parameter values.”

This doesn’t do too much for you when you’re working only in Kotlin, but it’s necessary if you want to generate multiple constructors that will work with Java code. For example, this Kotlin code works just fine:

````
class Person constructor(
    var firstName: String,
    var lastName: String,
    var age: Int = 0
) {
    override fun toString(): String =
        "$firstName $lastName is $age years old"
}

fun main(args: Array<String>) {
    val p1 = Person("Alvin", "Alexander", 40)
    val p2 = Person("Alvin", "Alexander")

    println(p1)
    println(p2)
}
````

But if you try to use the `Person` class constructors in Java you’ll find that the second line won’t compile:

````
Person p1 = new Person("John", "Doe", 30);
Person p2 = new Person("Jane", "Doe");      //won’t compile
````

The solution to work properly with Java is to add the `@JvmOverloads` annotation to the Kotlin class:

````
class Person @JvmOverloads constructor(  //same as before...
             -------------
````

With the rest of the class being the same, this annotation allows the Kotlin class to be used in Java code.





