---
description: This page shows how to use imports and packaging statements in Kotlin.
---


# Imports and Packages

Import and package statements are very similar to Java, with just a few additions/improvements.


## Key points

Packages:

- Package statements are just like Java, but they don’t have to match the directory the file is in

Import statements:

- There is no `import static` syntax
- You can rename a class when you import it
- The `import` statement is not restricted to only importing class

You can also import:

- Top-level functions and properties
- Functions and properties declared in object declarations
- Enum constants

Finally, a collection of classes and functions are imported for you by default, such as _kotlin.*_



## Package statements

Put package statements at the top of a file:

````
package foo.bar.baz

// the rest of your code here ...
````

The only real difference with Java is that the package name doesn’t have to match the name of the directory that the file is in.


### Files don’t have to contain class declarations

Because a Kotlin file doesn’t have to contain a class, it’s perfectly legal to put one or more functions in a file:

````
package foo.bar

fun plus1(i: Int) = i + 1
fun double(i: Int) = i * 2
````

Because of the package name, you can now refer to the function `plus1` in the rest of your code as `foo.bar.plus1`. Or, as you’ll see in the `import` examples that follow, you can import the function into the scope of your other code like this:

````
import foo.bar.plus1
````



## Import statements

Import statements work just like Java, with only a few differences:

- There is no `import static` syntax
- You can rename a class when you import it
- The `import` statement is not restricted to only importing class


### No “import static”

Kotlin doesn’t have a separate `import static` syntax. Just use a regular `import` declaration to import static methods and fields:

````
>>> import java.lang.Math.PI
>>> PI
3.141592653589793

>>> import java.lang.Math.pow
>>> pow(2.0, 2.0)
4.0
````


### Renaming a class when you import it

To avoid namespace collisions you can rename a class when you import it:

````
import java.util.HashMap as JavaHashMap
````

The REPL shows how it works:

````
>>> import java.util.HashMap as JavaHashMap

>>> val map = JavaHashMap<String, String>();

>>> map.put("first_name", "Alvin")
null

>>> map
{first_name=Alvin}
````

Here’s a combination of the two techniques just shown, (a) importing a static field and (b) renaming it during the import process:

````
import java.lang.Integer.MAX_VALUE as MAX_INT
import java.lang.Long.MAX_VALUE as MAX_LONG
````

Here are the values in the REPL:

````
>>> MAX_INT
2147483647

>>> MAX_LONG
9223372036854775807
````


### Things you can import

Per [the official Kotlin documentation](https://kotlinlang.org/docs/reference/packages.html), in addition to importing classes, you can also import:

- Top-level functions and properties
- Functions and properties declared in object declarations
- Enum constants



## Default imports

When you first start working with Kotlin it can be a surprise that you can use the `println` function without having to write `System.out.println` every time. This is partly due to the fact that a collection of packages are imported into every Kotlin file by default:

- kotlin.*
- kotlin.annotation.*
- kotlin.collections.*
- kotlin.comparisons.* (since 1.1)
- kotlin.io.*
- kotlin.ranges.*
- kotlin.sequences.*
- kotlin.text.*

The `println` function is declared in [the kotlin.io package](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/index.html), and it’s automatically made available to you.

When working with the Java Virtual Machine (JVM), these packages are also automatically imported:

- java.lang.*
- kotlin.jvm.*

When you’re compiling Kotlin code to JavaScript this package is imported by default:

- kotlin.js.*






