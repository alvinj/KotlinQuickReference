---
description: This page shows how to use abstract classes in Kotlin, including when and why you should use abstract classes instead of interfaces.
---

# Abstract Classes

Abstract classes in Kotlin are similar to abstract classes in Java and Scala, but Kotlin makes a clear distinction about which methods are considered “open” to be overridden.


## Key points

- Abstract classes are similar to Java’s abstract classes
- If you declare a class `abstract` it can’t be instantiated
- Abstract classes can have:
     - Abstract and concrete methods
     - Abstract and concrete properties (fields)
- Abstract classes and abstract members don’t have to be annotated with `open`; the fact that they are abstract implies that they are intended to be overridden
- Abstract classes can have private and protected members



## Functions in abstract classes

Functions can be:

- Abstract: function signature only, no body
- Concrete, but closed (i.e., final)
- Concrete, and open to modification

Example:

````
abstract class Pet (name: String) {
    abstract fun comeToMaster(): Unit          //abstract, open by default
    fun walk(): Unit = println("I’m walking")  //concrete, closed (final)
    open fun speak(): Unit = println("Yo")     //concrete, open
}
````



## Working code

Here’s a small, complete example that shows how abstract classes and functions work with inheritance:

````
abstract class Pet (name: String) {
    abstract fun comeToMaster(): Unit          //abstract, open by default
    fun walk(): Unit = println("I’m walking")  //concrete, closed (final)
    open fun speak(): Unit = println("Yo")     //concrete, open
}

class Dog(name: String) : Pet(name) {
    override fun speak() = println("Woof")
    override fun comeToMaster() = println("Here I come!")
}

class Cat(name: String) : Pet(name) {
    override fun speak() = println("Meow")
    override fun comeToMaster() = println("That’s not gonna happen")
}

fun main(args: Array<String>) {

    val d = Dog("Zeus")
    d.walk()
    d.speak()
    d.comeToMaster()

    val c = Cat("Rusty")
    c.walk()
    c.speak()
    c.comeToMaster()

}
````



## Other abstract class features

Abstract classes can also have private properties, abstract properties, and concrete properties, as shown in the last three lines of this example:

````
abstract class Pet (name: String) {
    abstract fun comeToMaster(): Unit          //abstract method
    fun walk(): Unit = println("I’m walking")  //concrete, closed (final)
    open fun speak(): Unit = println("Yo")     //concrete, open

    private var numberOfLegs = 4       //private
    abstract var furColor: String      //abstract (no initial value)
    var actuallyLikesPeople = false    //concrete, must have a value
}
````



## Why use abstract classes (instead of interfaces)?

Interfaces can’t have constructor parameters, initialized properties, or private properties.

You can kind of simulate properties with default values, but interface properties can’t have backing fields:

````
interface Cat {
    private var numLegs: Int
        get() = 4
        set(value) = TODO()   //can’t use `field`
}
````



## A note about designing base classes

[This Reddit post](https://www.reddit.com/r/androiddev/comments/803dq3/kotlin_booby_trap_never_use_init_in_openabstract/) has an interesting discussion about designing base classes. One interesting quote: 

>"Designing a base class, you should therefore avoid using open members in the constructors, property initializers, and init blocks."

See that Reddit link and [this Kotlin link](https://kotlinlang.org/docs/reference/classes.html#derived-class-initialization-order) for more details.











