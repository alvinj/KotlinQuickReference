---
description: This page discusses Kotlin interfaces, including how to write interfaces, and how to extend multiple interfaces in a Kotlin class.
---


# Kotlin Interfaces

If you’re familiar with Java, Kotlin interfaces are similar to Java 8 interfaces. If you know Scala, they also have similarities to Scala traits.



## Key points

What you’ll see in this lesson:

- Interfaces are defined using the `interface` keyword
- Interfaces can declare functions, which can be abstract or concrete
- Interfaces can declare fields (properties):
    - They can be abstract
    - They can provide implementations for accessors
- Interfaces can inherit/derive from other interfaces
- A class or object can implement one or more interfaces
- When you inherit from multiple interfaces that have methods with the same names and signatures, you must manually resolve the conflict

As shown previously, Kotlin also has a concept of abstract classes. Use abstract classes instead of interfaces when:

- You need constructor parameters (interfaces can’t have them)
- You need to define concrete read/write fields
- You need private members



## Interfaces with abstract and concrete functions

This example shows common uses of interfaces, with both abstract and concrete functions in the interfaces, along with overridden functions in the concrete `Dog` class:

````
package interfaces

interface Speaker {
    //abstract function
    fun speak(): String
}

interface TailWagger {
    // concrete implementations
    fun startTail() { println("tail is wagging") }
    fun stopTail() { println("tail is stopped") }
}

class Dog : Speaker, TailWagger {

    // override an abstract function
    override fun speak(): String = "Woof!"

    // override a concrete function
    override fun stopTail() { println("can’t stop the tail!") }

}

fun main(args: Array<String>) {
    val d = Dog()
    println(d.speak())  //"Woof!"
    d.startTail()       //"tail is wagging"
    d.stopTail()        //"can’t stop the tail!"
}
````



## Properties

Key points:

- Interfaces can define properties (fields)
- They can be abstract
- You can define an accessor (getter) for a property

Examples:

````
interface PizzaInterface {
    var numToppings: Int      //abstract
    var size: Int             //abstract
    val maxNumToppings: Int   //concrete
        get() = 10
}

class Pizza : PizzaInterface {

    // simple override
    override var numToppings = 0

    // override with get/set
    override var size: Int = 14  //14"
        get() = field
        set(value) { field = value}

    // override on a `val`
    override val maxNumToppings: Int
        //get() = super.maxNumToppings
        get() = 20
}


fun main(args: Array<String>) {
    val p = Pizza()
    println(p.numToppings)     //0
    println(p.size)            //14
    println(p.maxNumToppings)  //20

    p.numToppings = 5
    p.size = 16
}
````

A note from [the official Kotlin docs](https://kotlinlang.org/docs/reference/interfaces.html): 
“A property declared in an interface can either be abstract, or it can provide implementations for accessors. Properties declared in interfaces can’t have backing fields, and therefore accessors declared in interfaces can’t reference them.”



## Inheritance

Interfaces can extend other interfaces, override their properties and functions, and declare new properties and functions:

````
interface StarTrekCrewMember {
    fun uniformColor(): String
}

interface Officer : StarTrekCrewMember {
    override fun uniformColor(): String = "not red"
}

interface RedShirt : StarTrekCrewMember {
    override fun uniformColor(): String = "red (sorry about your luck)"
    fun diePainfulDeath(): String = "i’m dead"
}

// more code ...
````

Here’s a class that implements three interfaces:

````
interface Starship
interface WarpCore
interface WarpCoreEjector
class Enterprise : Starship, WarpCore, WarpCoreEjector
````



## Resolving inheritance conflicts

When a class extends multiple interfaces and those interfaces have a common method, you must manually handle the situation in the function in your class. This example shows how to handle the functions `foo` and `bar` in the class `C`, where `C` extends both interfaces `A` and `B`:

````
interface A {
    fun foo() { println("foo: A") }
    fun bar(): Unit
}

interface B {
    fun foo() { println("foo: B") }
    fun bar() { println("bar: B") }
}

class C : A, B {
    override fun foo() {
        super<A>.foo()
        super<B>.foo()
        println("foo: C")
    }
    override fun bar() {
        super<B>.bar()
        println("bar: C")
    }
}

fun main(args: Array<String>) {
    val c = C()
    c.foo()
    println()
    c.bar()
}
````

Here’s the output from `main`:

````
foo: A
foo: B
foo: C

bar: B
bar: C
````

>This example is a simplified version of [this kotlinlang.org example](https://kotlinlang.org/docs/reference/interfaces.html).








