---
description: This page provides examples of the Kotlin Array class, including how to add and remove elements from a List.
---

<!--
    TODO multidimensional arrays
    TODO null/nullable types and arrays
-->


# Array

Arrays are created with various `arrayOf` functions. Here are two ways to create arrays (implicit and explicit syntax):

````
val x = arrayOf(1,2,3)
val x: Array<Int> = arrayOf(1,2,3)

val y = arrayOf("a", "b", "c")
val y: Array<String> = arrayOf("a", "b", "c")
````


## Array creation functions

Kotlin has these array-creation functions that are listed in *kotlin.Library.kt*:

````
fun <reified @PureReifiable T> arrayOfNulls(size: Int): Array<T?>
fun doubleArrayOf(vararg elements: Double): DoubleArray
fun floatArrayOf(vararg elements: Float): FloatArray
fun longArrayOf(vararg elements: Long): LongArray
fun intArrayOf(vararg elements: Int): IntArray
fun charArrayOf(vararg elements: Char): CharArray
fun shortArrayOf(vararg elements: Short): ShortArray
fun byteArrayOf(vararg elements: Byte): ByteArray
fun booleanArrayOf(vararg elements: Boolean): BooleanArray
````



## Warning: Array<Int> is not the same as IntArray

Note: `arrayOf(1,2,3)` and `intArrayOf(1,2,3)` are not the same:

````
> val b: Array<Int> = arrayOf(1,2,3)
> b.javaClass
class [Ljava.lang.Integer;
> b.javaClass.name
[Ljava.lang.Integer;
> b.javaClass.kotlin
class kotlin.Array

> val c: IntArray = intArrayOf(1,2,3)
> c.javaClass
class [I
> c.javaClass.name
[I
> c.javaClass.kotlin
class kotlin.IntArray
````

TODO: Briefly discuss this.








