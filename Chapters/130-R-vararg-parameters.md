---
description: This page shows how to use vararg parameters with Kotlin functions, including passing arrays into vararg parameters.
---


# vararg Parameters

A Kotlin function parameter can be defined as a `vararg` parameter so it can be called with zero or more values.



## Key points

- Declare function parameters with the `vararg` keyword
- When arrays are passed in, handle them with the `*` character
- Note: “In Kotlin, a vararg parameter of type `T` is internally represented as an array of type `T` (`Array<T>`) inside the function body.”



## Basic example

Here’s a function that takes a `vararg` parameter:

````
fun printAll(vararg ints: Int) {
    for (i in ints) println(i)
}
````

The REPL shows how it works:

````
> printAll(1)
1

> printAll(1,2,3)
1
2
3

> printAll()
````



## Passing in an array

Passing in an array won’t work:

````
val arr = intArrayOf(1,2,3)

> printAll(arr)
error: type mismatch: inferred type is Array<Int> but Int was expected
printAll(arr)
         ^
````

The solution is that you need to pass the array into your `vararg` parameter with this syntax:

````
printAll(*arr)
````

The `*` character in this use is known as the “spread operator.” The spread operator lets you convert arrays — well, most arrays — so they can be passed into a vararg parameter.



### Not all arrays work (TODO)

The spread operator only works with certain types of arrays with vararg parameters. For example, I just showed that `intArrayOf` works:

````
> val intArray = intArrayOf(1,2,3)

> printAll(*intArray)
1
2
3
````

However, `arrayOf` does not work when it’s given a list of integers:

````
> val arrayOfInt = arrayOf(1,2,3)

> printAll(*arrayOfInt)
error: type mismatch: inferred type is Array<Int> but IntArray was expected
printAll(*arrayOfInt)
          ^
````

To understand this it helps to look at the data types in the Kotlin REPL. Here are some details about the result from `intArrayOf`:

````
> val x = intArrayOf(1,2,3)

> println(x.javaClass.name)
[I

> println(x.javaClass.kotlin)
class kotlin.IntArray

> println(x.javaClass.kotlin.qualifiedName)
kotlin.IntArray
````

Similarly, here are some results for `arrayOf`:

````
> val x = arrayOf(1,2,3)

> println(x.javaClass.name)
[Ljava.lang.Integer;

> println(x.javaClass.kotlin)
class kotlin.Array

> println(x.javaClass.kotlin.qualifiedName)
kotlin.Array
````

As shown by those results, `intArrayOf` creates a type of `kotlin.IntArray`, which works with a vararg parameter of type `Int`, but `arrayOf` creates a type of `kotlin.Array`, which does not work with the same vararg parameter. (This is true as of Kotlin version 1.2.51.)

<!--
val x = arrayOf(1,2,3)
println(x.javaClass.name)
println(x.javaClass.kotlin)
println(x.javaClass.kotlin.qualifiedName)
-->



## Bonus: Make it generic (TODO: NOT WORKING)

````
fun <T> printAll(vararg elems: T) {
    for (e in elems) println(e)
}
````

fun Int.toString() = this
printAll(arrayOf(1,2,3))
printAll(intArrayOf(1,2,3))

val x = arrayOf(1,2,3)
val x = intArrayOf(1,2,3)

















