---
description: This page shares a complete Kotlin `Pizza` class that you might use in a pizza store POS system.
---

<!-- DONE FOR NOW -->


# A Complete Kotlin Class

In this lesson you’ll create a `Pizza` class in Kotlin that might be used in a pizza-store point of sales system. The class will be written in an object-oriented programming (OOP) style, and will use enumerations, constructor parameters, and class properties and functions.



## Pizza-related enumerations

I’ll start creating a pizza class by first creating some enumerations that will be helpful:

````
enum class Topping {
    CHEESE, PEPPERONI, SAUSAGE, MUSHROOMS, ONIONS
}

enum class CrustSize {
    SMALL, MEDIUM, LARGE
}

enum class CrustType {
    REGULAR, THIN, THICK
}
````

Those enumerations provide a nice way to work with pizza toppings, crust sizes, and crust types.



## A sample Pizza class

Given those enumerations I can define a `Pizza` class like this:

````
class Pizza (
    var crustSize: CrustSize = CrustSize.MEDIUM,
    var crustType: CrustType = CrustType.REGULAR
) {
    val toppings = mutableListOf<Topping>()

    fun addTopping(t: Topping): Boolean = toppings.add(t)
    fun removeTopping(t: Topping): Boolean = toppings.remove(t)
    fun removeAllToppings(): Unit = toppings.clear()
}
````

>`toppings` can be a constructor parameter, but I wrote it this way to show a class property.

When you save the enumerations and that class in a file named *Pizza.kt*, you can compile it with `kotlinc`:

````
$ kotlinc Pizza.kt
````

That command creates the following class files:

````
CrustSize.class
CrustType.class
Pizza.class
Topping.class
````

There’s nothing to run yet because this class doesn’t have a `main` method, but ... 



## A complete Pizza class with a main method

To see how this class works, replace the source code in *Pizza.kt* with the following code:

<!-- THIS WORKS -->
````
enum class Topping {
    CHEESE, PEPPERONI, SAUSAGE, MUSHROOMS, ONIONS
}

enum class CrustSize {
    SMALL, MEDIUM, LARGE
}

enum class CrustType {
    REGULAR, THIN, THICK
}

class Pizza (
    var crustSize: CrustSize = CrustSize.MEDIUM,
    var crustType: CrustType = CrustType.REGULAR
) {

    val toppings = mutableListOf<Topping>()

    fun addTopping(t: Topping): Boolean = toppings.add(t)
    fun removeTopping(t: Topping): Boolean = toppings.remove(t)
    fun removeAllToppings(): Unit = toppings.clear()

    override fun toString(): String {
        return """
        |Pizza:
        |  Crust Size: $crustSize
        |  Crust Type: $crustType
        |  Toppings:   $toppings
        """.trimMargin()
    }
}

fun main(args: Array<String>) {
    val p = Pizza()
    p.addTopping(Topping.CHEESE)
    p.addTopping(Topping.PEPPERONI)
    p.addTopping(Topping.MUSHROOMS)
    p.addTopping(Topping.ONIONS)
    println(p)
    p.removeTopping(Topping.MUSHROOMS)
    p.removeTopping(Topping.ONIONS)
    println(p)
    p.removeAllToppings()
    println(p)
}
````

Notice that I added a `toString` function to the `Pizza` class, and added a `main` function to test everything in the `Pizza` class. 

When you compile the code with this command:

````
$ kotlinc Pizza.kt -include-runtime -d Pizza.jar
````

then execute the jar file with this `java` command:

````
$ java -jar Pizza.jar
````

you’ll see this output:

````
Pizza:
  Crust Size: MEDIUM
  Crust Type: REGULAR
  Toppings:   [CHEESE, PEPPERONI, MUSHROOMS, ONIONS]
Pizza:
  Crust Size: MEDIUM
  Crust Type: REGULAR
  Toppings:   [CHEESE, PEPPERONI]
Pizza:
  Crust Size: MEDIUM
  Crust Type: REGULAR
  Toppings:   []
````

This is a good start for creating an OOP-style class that uses enumerations, constructor parameters, and class properties and functions.










