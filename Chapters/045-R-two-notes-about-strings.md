---
description: This page shows two great features of Kotlin strings, including multiline strings and string interpolation.
---



# Two Notes About Strings

Kotlin has a few nice `String` features:

- String templates
- Multiline strings


## String templates

Kotlin has a nice, Ruby- and Scala-like way to merge multiple strings known as String Templates. Given these three variables:

````
val firstName = "John"
val mi = 'C'
val lastName = "Doe"
````

you can append them together like this:

````
val name = "$firstName $mi $lastName"
````

This creates a very readable way to print multiple strings:

````
println("Name: $firstName $mi $lastName")
````

You can also include complete expressions inside strings:

````
>>> val x = 2
>>> val y = 3
>>> println("$x times $y is ${x * y}.")
2 times 3 is 6.
````



## Multiline strings

You can create multiline strings by including the string inside three parentheses:

````
val speech = """Four score and
               seven years ago
               our fathers ..."""
````

This is helpful for a variety of occasions, such as when you want to write SQL queries by hand, provide sample data during tests, and many more occasions.

One drawback of this basic approach is that lines after the first line are indented, as you can see in the REPL:

````
>>> speech
Four score and
               seven years ago
               our fathers ...
````

A simple way to fix this problem is to put a `|` symbol in front of all lines after the first line, and call the `trimMargin` method after the string:

````
val speech = """Four score and
               |seven years ago
               |our fathers ...""".trimMargin()
````

The REPL shows that when you do this, all of the lines are left-justified:

````
>>> speech
Four score and
seven years ago
our fathers ...
````

Because this is what you generally want, this is a common way to create multiline strings.








