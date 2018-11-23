---
description: This page shows how to use Kotlin's try/catch/finally construct, including a complete example.
---

# Kotlin try/catch/finally Expressions

Like Java, Kotlin has a try/catch/finally construct to let you catch and manage exceptions. If you’ve used Java, there’s only one new feature here: a `try` expression is truly an expression, meaning you can assign its result to a variable. (See the “Try is an expression” section below for those details.)



## Basic syntax

Kotlin’s try/catch/finally syntax looks like this:

````
try {
    // some exception-throwing code
}
catch (e: SomeException) {
    // code
}
catch (e: SomeOtherException) {
    // code
}
finally {
    // optional
}
````

As shown in the comment, the `finally` clause is optional. Everything works just like Java.



## Example

Because there are easier ways to read files in Kotlin, this example is a little contrived, but it shows an example of how to use `try` with multiple `catch` clauses and a `finally` clause:

````
import java.io.*

fun main(args: Array<String>) {

    var linesFromFile = listOf<String>()
    var br: BufferedReader? = null

    try {
        br = File("/etc/passwd2").bufferedReader()
        linesFromFile = br.readLines()
    }
    catch (e: IOException) {
        e.printStackTrace()
    }
    catch (e: FileNotFoundException) {
        e.printStackTrace()
    }
    finally {
        br?.close()
    }

    linesFromFile.forEach { println(">  " + it) }

}
````

Don’t worry about the `?` symbols in the code for now, I just wanted to show a complete try/catch/finally example. Just know that the question marks are needed for working with null values in Kotlin.

>Or, if you want to learn about them, jump ahead to the “Nullability” lessons later in this book.



## `Try` is an expression

Try in Kotlin is different than Java because Kotlin’s `try` is an expression, meaning that it returns a value:

````
val s = "1"

// using try as an expression
val i = try {
    s.toInt()
} 
catch (e: NumberFormatException) { 
    0 
}
````

That expression can be read as, “If `s` converts to an `Int`, return that integer value; otherwise, if it throws a `NumberFormatException`, return `0`.”

You can write that try expression more concisely:

````
val i = try { s.toInt() } catch (e: NumberFormatException) { 0 }
````

Try that expression with different values like these to confirm for yourself that it works as expected:

````
val s = "1"
val s = "foo"
````












