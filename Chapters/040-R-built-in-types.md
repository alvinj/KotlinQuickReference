---
description: This page looks at the built-in Kotlin data types, including Int, Double, Float, String, Char, Boolean, BigInteger, and BigDecimal.
---


# Built-In Data Types

Kotlin comes with the standard numeric data types you’d expect, and in Kotlin all of these data types are full-blown objects — not primitive data types.

How to declare variables of the basic numeric types:

````
val b: Byte = 1
val i: Int = 1
val l: Long = 1
val s: Short = 1
val d: Double = 2.0
val f: Float = 3.0f
````

In the first four examples, if you don’t explicitly specify a type, the number `1` will default to an `Int`, so if you want one of the other data types — `Byte`, `Long`, or `Short` — you need to explicitly declare those types, as shown. Numbers with a decimal (like 2.0) will default to a `Double`, so if you want a `Float` you need to declare a `Float`, as shown in the last example. You can also declare `Long` and `Float` types like this:

````
val l = 1L
val f = 3.0f
````

Because `Int` and `Double` are the default numeric types, you typically create them without explicitly declaring the data type:

````
val i = 123   // defaults to Int
val x = 1.0   // defaults to Double
````

All of those data types have the same data ranges as their Java equivalents:

| Type   | Bit width |
| ------ | --------: |
| Byte   |       8   |
| Short  |      16   |
| Int    |      32   |
| Long   |      64   |
| Float  |      32   |
| Double |      64   |

(For more information on those, see my article, [JVM bit sizes and ranges](https://alvinalexander.com/scala/scala-data-types-bits-ranges-int-short-long-float-double).)



## BigInteger and BigDecimal

In Kotlin you can use the *java.math.BigInteger* class:

````
> import java.math.BigInteger
> val x = BigInteger("1")
````

Kotlin also has convenient extension functions to help you convert other data types to `BigInteger`:

````
> val y = 42.toBigInteger()
> val y = 42L.toBigInteger()
````

Kotlin lets you use the Java `BigDecimal` class in similar ways:

````
> import java.math.BigDecimal
> val x = BigDecimal("1.0")
> 1.0.toBigDecimal()
````

See these links for more information:

- [Kotlin BigInteger extension functions](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/java.math.-big-integer/index.html)
- [Kotlin BigDecimal extension functions](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/java.math.-big-decimal/index.html)



## String, Char, and Boolean

Kotlin also has `String`, `Char`, and `Boolean` data types, which I always declare with the implicit form:

````
val name = "Bill"
val c = 'c'
val b = true
````







