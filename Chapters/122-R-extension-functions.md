---
description: This page provides a first look at how to write Kotlin functions, including how to test them in the REPL.
---

<!-- 
    TODO where to define extension functions
    TODO how to import them
    TODO what is `this` in an extension function?
-->


# Extension Functions

Extension functions let you add new methods to existing classes (like `String`, `Int`, etc.). If you’ve used *implicit classes* in Scala, extension functions are just like those.



## Example

In the years before Kotlin, I wanted an Android method that would let me write code like this:

````
if (x.between(1, 10)) ...
````

I couldn’t do that with Java, so I had to settle for less-readable code that looked like this:

````
if (between(x, 1, 10)) { ...
````

But these days with Kotlin I can get what I want with an *extension function*:

````
fun Int.between(a: Int, b: Int): Boolean {
    return if (this >= a && this <= b) true else false
}
````

The REPL shows how to use that function:

````
>>> 5.between(1, 10)
true

>>> 22.between(1, 10)
false
````



## How to declare an extension function

The key to writing an extension function is that you declare that you want to add a function to a specific data type:

````
fun Int.between(a: Int, b: Int): Boolean {
    ---
````

You also specify that you want the function to have this name:

````
fun Int.between(a: Int, b: Int): Boolean {
        -------
````

these parameters:

````
fun Int.between(a: Int, b: Int): Boolean {
                ------  ------
````

and this return type:

````
fun Int.between(a: Int, b: Int): Boolean {
                                 -------
````

In fact, an extension function is just like a normal function, except that it’s preceded by the name of the data type you want the function to be added to, as shown in this example.



## An extension function on `Any`

Here’s an extension function that I add to the `Any` type:

````
fun Any.printMe(): Unit = println("I am ${this}")
````

Because `Any` is the root of all Kotlin objects — like `java.lang.Object` in Java — it works on all Kotlin types:

````
1.printMe()
"Hello".printMe()
true.printMe()
````

Here’s what those examples look like in the REPL:

````
>>> 1.printMe()
I am 1

>>> "Hello".printMe()
I am Hello

>>> true.printMe()
I am true
````












