---
description: This page shows examples of working with class members, including initialization blocks, functions, properties, nested and inner classes, and object declarations.
---


# Class Members

Classes can contain:

- Constructors
- Constructor initializer blocks
- Functions
- Properties
- Nested and Inner Classes
- Object Declarations



## Constructors

Basic constructor syntax:

````
class Person

class Person (name: String, age: Int) {
    // class code here ...
}
````

The `constructor` keyword is only needed if the class has annotations or visibility modifiers:

````
class Person private constructor (name: String) { ... }
class Person public @Inject constructor (name: String) { ... }
class Person @JvmOverloads constructor (name: String, age: Int) { ... }
````

Primary constructor initialization code goes in `init` block:

````
class Person (name: String) {
    init {
        println("Person instance created")
    }
}
````



## Initializer blocks

Classes can have initializer blocks that are called when the class is constructed, and those blocks can access the constructor parameters:

````
// a network socket
class Socket(var timeout: Int, var linger: Int) {
    init {
        println("Entered 'init' ...")
        println("timeout = ${timeout}, linger = ${linger}")
    }
}
````

Here’s what it looks like when a `Socket` is created:

````
> val s = Socket(2000, 3000)
Entered 'init' ...
timeout = 2000, linger = 3000
````

You can have multiple initializer blocks, and the code in those blocks is effectively part of the primary constructor.

<!--
    TODO: show a more complicated example that shows when the init
    block is called
-->



## Methods (functions)

Just like Java and other languages, classes can have methods (which are referred to as functions):

````
class Person(val firstName: String, val lastName: String) {
    fun fullName() = "$firstName $lastName"
}
````

Here’s a REPL example:

````
> val p = Person("Hala", "Cina")
> p.fullName()
Hala Cina
````



## Properties (fields)

Just like Java and other languages, classes can have properties (fields):

````
class Pizza () {
    val toppings = mutableListOf<String>()
    fun addTopping(t: String) { toppings.add(t) }
    fun showToppings() { println(toppings) }
    // more code ...
}
````

Here’s an example in the REPL:

````
> val p = Pizza()
> p.addTopping("Cheese")
> p.addTopping("Pepperoni")
> p.showToppings()
[Cheese, Pepperoni]
````



## Nested and inner classes

Classes can be nested in other classes. Note that a nested class can’t access a parameter in the outer class:

````
class Outer {
    private val x = 1
    class Nested {
        //fun foo() = 2 * x   //this won’t compile
        fun foo() = 2
    }
}
````

In the REPL:

````
> val foo = Outer.Nested().foo()
> foo
2
````



## Inner classes

Mark a class as `inner` if you need to access members of the outer class:

````
class Outer {
    private val x = 1
    inner class Inner {
        fun foo() = x * 2
    }
}
````

In the REPL:

````
> val foo = Outer().Inner().foo()
> foo
2
````

### Syntax

Notice the difference between the syntax when using a nested class versus an inner class:

````
val foo = Outer.Nested().foo()
val foo = Outer().Inner().foo()
               --
````

If you try to create an inner class without first creating an instance of the outer class you’ll see this error:

````
> val foo = Outer.Inner().foo()
error: constructor of inner class Inner can be called only with receiver of containing class
val foo = Outer.Inner().foo()
                ^
````








