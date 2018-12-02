---
description: This lesson demonstrates examples of how to use Kotlin commands at the command line, including 'kotlinc'.
---

<!--
    TODO more command line examples
-->

# Kotlin at the Command Line

This lesson demonstrates examples of how to use Kotlin commands at the command line, including `kotlinc`.



## Compiling a Kotlin file

````
$ kotlinc Hello.kt
````

That command creates a file named *HelloKt.class*.



## Compiling to an executable Jar file

Compiling to an executable Jar file:

````
$ kotlinc Hello.kt -include-runtime -d Hello.jar
````

Then execute the jar file with this `java` command:

````
$ java -jar Hello.jar
Hello, world
````




