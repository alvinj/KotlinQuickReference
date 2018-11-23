---
description: This page provides a first look at how to write infix functions in Kotlin, including how to test them in the REPL.
---


# Infix Functions

An *infix function* is a function that appears in between two variables. Kotlin makes it easy to create functions like this.



## Key points

- Infix functions are declared similarly to extension functions
- They are declared by writing `infix fun` at the start of the function definition
- When applied like `1 plus 2`, the function belongs to the variable on the left (`1`) and the variable on the right (`2`) is the function parameter
- Can be used to create DSLs



## Examples

Imagine that the `+` operator doesn’t exist and you want a function to add two integers, like this:

````
val x = 1 plus 1
````

Just write an infix function like this:

````
infix fun Int.plus(that: Int) = this + that
````

Here’s how it looks in the Kotlin REPL:

````
> 1 plus 1
2
````


### Notes

Note the `infix` keyword:

````
infix fun Int.plus(that: Int) = this + that
-----
````

Notice that it’s an extension function for the `Int` type:

````
infix fun Int.plus(that: Int) = this + that
          ---
````


## Understanding the “target” object

By changing the function:

````
infix fun Int.plus(that: Int): Int {
    println("this: ${this}, that: ${that}")
    return this + that
}

> 1 plus 2
this: 1, that: 2
3
````

You can see:

- The variable on the left (`1`) is considered the *target* object
- The variable on the right (`2`) is the function parameter







