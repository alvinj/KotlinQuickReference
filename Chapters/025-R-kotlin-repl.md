---
description: This page provides an introduction to the Kotlin REPL, i.e., its command-line interpreter.
---


# The Kotlin REPL

The Kotlin REPL (“Read-Evaluate-Print-Loop”) is a command-line interpreter that you use as a “playground” area to test your Kotlin code. To start a REPL session, just type `kotlinc` at your operating system command line, and you’ll see this:

````
> kotlinc
Welcome to Kotlin version 1.2.51 (JRE 1.8.0_181-b13)
Type :help for help, :quit for quit
>>> _
````

>The prompt for the Kotlin REPL is `>>>`, but because I don’t like that I only show one `>` character for the prompt in this book.

Because the REPL is a command-line interpreter, it just sits there waiting for you to type something. Once you’re in the REPL, you can type Kotlin expressions to see how they work:

````
> 1 + 1
2

> 4 / 2
2

> 4 % 2
0
````

As those examples show, when you type simple expressions, the Kotlin REPL shows the result of the expression on the line after the prompt. For other expressions you may have to type the variable name you created to see its value:

````
> val x = 1 + 1

> x
2
````

>You can also try Kotlin online at [try.kotlinlang.org/](https://try.kotlinlang.org/)



## Take the REPL for a spin

You’re going to use the Kotlin REPL a lot in this book, so go ahead and start it (with `kotlinc`) and experiment with it. Here are a few expressions you can try to see how it all works:

````
1 + 1
4 / 2
5 / 2
4 % 2
5 % 2
5 / 2.0
1 + 2 * 3
(1 + 2) * 3
val name = "John Doe"
"hello"[0]
"hello"[1]
"hello, world".take(5)
println("hi")
if (2 > 1) println("greater") else println("lesser")
for (i in 1..3) println(i)
listOf(1,2,3).forEach { println(it) }
````

As a little more advanced exercise, here’s how to define a class named `Person`, create an instance of it, and then show the value of the `name` field:

````
class Person(var name: String)
val p = Person("Kim")
p.name
````

Notice that you don’t need the `new` keyword when creating an instance of a class.



## Use `javaClass` to see an object’s type

To see an object’s type in the REPL, call `.javaClass` on the instance:

````
> "foo".javaClass
class java.lang.String

> 1.javaClass
int

> 1.0.javaClass
double
````

Here’s a map:

````
// paste this into the repl
val map = mapOf(
    1 to "one",
    2 to "two"
)

> map.javaClass
class java.util.LinkedHashMap
````

Here’s a list:

````
> listOf(1,2,3).javaClass
class java.util.Arrays$ArrayList
````

The following examples on the result of `intArrayOf` show other calls you can make after `javaClass`:

````
> val x = intArrayOf(1,2,3)

> println(x.javaClass.name)
[I

> println(x.javaClass.kotlin)
class kotlin.IntArray

> println(x.javaClass.kotlin.qualifiedName)
kotlin.IntArray
````










