---
description: This page shows two great features of Kotlin strings, including multiline strings and string interpolation.
---


# Strings

This lesson shows:

- String templates
- Multiline strings
- How to convert a list or array to a `String`



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
> val x = 2
> val y = 3
> println("$x times $y is ${x * y}.")
2 times 3 is 6.
````



## Multiline strings

You can create multiline strings by including the string inside three parentheses:

````
val speech = """Four score and
               seven years ago
               our fathers ..."""
````

One drawback of this basic approach is that lines after the first line are indented, as you can see in the REPL:

````
> speech
Four score and
               seven years ago
               our fathers ...
````

A simple way to fix this problem is to put a `|` symbol in front of all lines after the first line, and call the `trimMargin` function after the string:

````
val speech = """Four score and
               |seven years ago
               |our fathers ...""".trimMargin()
````

The REPL shows that when you do this, all of the lines are left-justified:

````
> speech
Four score and
seven years ago
our fathers ...
````



## How to convert a list to a String

How to convert a list or array to a `String`:

````
val nums = listOf(1,2,3,4,5)

> nums.joinToString()
1, 2, 3, 4, 5

> nums.joinToString(
    separator = ", ",
    prefix = "[",
    postfix = "]",
    limit = 3,
    truncated = "there’s more ..."
)
[1, 2, 3, there’s more ...]
````

Another example:

````
val words = arrayOf("Al", "was", "here")

> words.joinToString()
Al, was, here

> words.joinToString(separator = " ")
Al was here
````







