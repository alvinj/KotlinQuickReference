---
description: This page shares a second Kotlin 'Hello, world' example.
---

# Hello, World (Part 2)

To understand how Kotlin works, let’s take a look at that *Hello.kt* file again:

````
fun main(args: Array<String>) {
    println("Hello, world")
}
````

This time, rather than creating an executable jar file, just compile the code like this:

````
$ kotlinc Hello.kt
````

That command creates a file named *HelloKt.class*. Since this is a normal JVM class file, use the `javap` command to disassemble it and see what’s inside:

````
$ javap HelloKt.class 

Compiled from "Hello.kt"
public final class HelloKt {
  public static final void main(java.lang.String[]);
}
````

As shown, Kotlin creates a class named `HelloKt`, and it contains a normal Java `public static void main` method. Kotlin creates the class with the name `HelloKt` because we didn’t supply a class name. The class file name comes from the filename — *Hello.kt* becomes `HelloKt`.



## A little more fun

Before we move on, let’s have a little more fun. Save this source code to a file named *HelloYou.kt*:

````
fun main(args: Array<String>) {
    if (args.size == 0)
        println("Hello, you")
    else
        println("Hello, ${args[0]}")
}
````

I hope you can see how it works:

- if/else statements work just like Java.
- Kotlin supports String Templates, which are similar to String Interpolation in languages like Scala, Groovy, and Ruby, so `${args[0]}` prints the first command line argument.

Now compile that file and create a new executable jar file:

````
$ kotlinc HelloYou.kt -include-runtime -d HelloYou.jar
````

Then run it with and without a command line argument:

````
$ java -jar HelloYou.jar
Hello, you

$ java -jar HelloYou.jar Alvin
Hello, Alvin
````



## Extra credit

To have a little more fun with this example, run this Java `jar` command on *HelloYou.jar*:

````
$ jar tvf HelloYou.jar 
````

If you know Java and how the JVM works, you can guess that the initial output of that command looks like this:

````
  79 Wed Aug 01 13:54:12 MDT 2018 META-INF/MANIFEST.MF
1249 Wed Aug 01 13:54:12 MDT 2018 HelloYouKt.class
````

The rest of the output is too long to include here — 654 lines total, to be precise — but I encourage you to run that command to get an idea of what’s needed to create an executable jar file.







