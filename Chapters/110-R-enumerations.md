---
description: This page introduces Kotlin enumerations, getting you ready to create a complete Pizza class in the next lesson.
---

<!-- DONE FOR NOW -->


## Summary

- Kotlin enumerations are similar to enumerations in other languages, such as Java
- Enumerations are declared with `enum class`
- Enumerations can have constructor parameters, properties, and functions
- Enumerations can be used in `if` and `when` expressions and `for` loops



# Basic enumerations

Simple enumerations are a useful tool for creating small groups of constants, things like the days of the week, months in a year, suits in a deck of cards, etc., situations where you have a group of related, constant values. Here are the days of the week:

````
enum class DayOfWeek {
    SUNDAY, MONDAY, TUESDAY,
    WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}
````

Here’s an enumeration for the suits in a deck of cards:

````
enum class Suit {
    CLUBS, SPADES, DIAMONDS, HEARTS
}
````



## The full power of enumerations

More than just simple constants, enumerations can have constructor parameters, properties, and functions, just like a regular class. Here’s an example, adapted from [this Oracle Java](https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html) example:

<!-- WORKS -->
````
enum class Planet(val mass: Double, val radius: Double) {
    // just the first three planets
    MERCURY (3.303e+23, 2.4397e6),
    VENUS   (4.869e+24, 6.0518e6),
    EARTH   (5.976e+24, 6.37814e6);  //semi-colon is required

    // universal gravitational constant (m3 kg-1 s-2)
    val G = 6.67300E-11

    fun surfaceGravity(): Double {
        return G * mass / (radius * radius);
    }

    fun surfaceWeight(otherMass: Double): Double {
        return otherMass * surfaceGravity();
    }
}

fun main(args: Array<String>) {
    val earthWeight = 200.0
    val mass = earthWeight / Planet.EARTH.surfaceGravity()
    for (p in Planet.values()) {
        val s = String.format("Your weight on %s is %.2f", p, p.surfaceWeight(mass))
        println(s)
    }
}
````

Here’s the output from that code:

````
Your weight on MERCURY is 75.55
Your weight on VENUS is 181.00
Your weight on EARTH is 200.00
````



## Enumerations with `if`, `when`, and `for`

Enumerations can be used with `if` and `when` expressions and `for` loops, as shown in the following examples.

`if` expressions:

<!-- WORKS -->
````
enum class DayOfWeek {
    SUNDAY, MONDAY, TUESDAY,
    WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}

fun main(args: Array<String>) {
    val today = DayOfWeek.MONDAY

    if (today == DayOfWeek.MONDAY) {
        println("MONDAY")
    }
    else if (today == DayOfWeek.TUESDAY) {
        println("TUESDAY")
    }
}
````

`when` expressions:

<!-- WORKS -->
````
enum class Margin {
    TOP, RIGHT, BOTTOM, LEFT
}

fun getMarginValue(margin: Margin) = when(margin) {
    Margin.TOP    ->  "1em"
    Margin.RIGHT  ->  "12px"
    Margin.BOTTOM ->  "1.5em"
    Margin.LEFT   ->  "6px"
}

fun main(args: Array<String>) {
    println(getMarginValue(Margin.TOP))
}
````

`for` loops:

<!-- WORKS -->
````
for (m in Margin.values()) println(m)
````












