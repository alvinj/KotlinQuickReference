---
description: This page shares a Kotlin 'Hello, world' example.
---

<!-- A GOOD FIRST DRAFT -->

# Hello, World

Since the release of [C Programming Language](http://amzn.to/2xRas2r), most programming books have begun with a simple “Hello, world” example, and in keeping with tradition, here’s the source code for a Kotlin “Hello, world” example:

````
fun main(args: Array<String>) {
    println("Hello, world")
}
````

Using a text editor, save that source code in a file named *Hello.kt*.

This code is similar to Java (and Scala), but notice a few things about it:

- A Kotlin function is declared with the `fun` keyword
- Compared to Java, you only have to write `println` as opposed to `System.out.println`
- In Kotlin, functions don’t have to be inside classes, so it’s perfectly legal to put a function like this in a file by itself

A fun thing about Kotlin is that you can easily create a jar file with the `kotlinc` compiler, so run this command at your command line prompt to compile that source code and create a jar file named *Hello.jar*:

````
$ kotlinc Hello.kt -include-runtime -d Hello.jar
````

Then execute the jar file with this `java` command:

````
$ java -jar Hello.jar
Hello, world
````

Welcome to the Kotlin world!












