---
description: This page provides a first look at how to write Kotlin functions, including how to test them in the REPL.
---


# A First Look at Kotlin Functions

In Kotlin, *functions* can be defined both inside and outside of classes.


## Key points

- Functions are defined with the `fun` keyword
- The syntax:

````
// single-expression syntax
fun plus1(i: Int) = i + 1
fun plus1(i: Int): Int = i + 1

// multiline syntax
fun plus1(i: Int): Int {
    return i + 1
}

// calling a function
val x = plus1(1)
````

- Functions are called just like you call Java methods
- Function parameters can have default values
- Functions can be called with named parameters
- Local functions can be created (functions defined within functions)
- “Infix” functions can be created (and will be covered in the next lesson)
- *Extension functions* let you extend existing types
- TODO: functions don't have to be inside classes, they can be at a package level



## One-line functions (single-expression)

One-line functions are called “single-expression” functions and they can be written like this:

````
// single-expression syntax
fun plus1(i: Int) = i + 1
fun plus1(i: Int): Int = i + 1
````

Notice that the `return` keyword is not used with the single-expression syntax.



## Multiline functions with return values

A multiline function looks like this:

````
fun addThenDouble(a: Int, b: Int): Int {
    val sum = a + b
    val doubled = sum * 2
    return doubled
}
````

The REPL shows how `addThenDouble` works:

````
> addThenDouble(1,1)
4

> addThenDouble(1,2)
6
````



## Multiline functions without return values

If a multiline function doesn’t have a return value, you can either leave it off the function declaration:

````
fun addAndPrint(a: Int, b: Int) {
    val sum = a + b
    println(sum)
}
````

or declare the return type as `Unit`:

````
fun addAndPrint(a: Int, b: Int): Unit {
    val sum = a + b
    println(sum)
}
````

Kotlin’s `Unit` return type is similar to void/Void in other programming languages.



## Function parameters can have default values

Just like constructors, you can specify default values for function parameters:

````
fun connect(timeout: Int = 5000, protocol: String = "http"): Unit {
    println("timeout = ${timeout}, protocol = ${protocol}")
    // more code here
}
````

Because of the default parameters, that function can be called in these ways:

````
connect()
connect(2500)
connect(10000, "https")
````

Here’s what those examples look like in the REPL:

````
> connect()
timeout = 5000, protocol = http

> connect(2500)
timeout = 2500, protocol = http

> connect(10000, "https")
timeout = 10000, protocol = https
````



## Functions can use named arguments

Just as with constructors, you can use named arguments when calling a function:

````
fun printName(firstName: String, lastName: String) {
    println("Your name is ${firstName} ${lastName}")
}
````

````
printName(firstName="Hala", lastName="Terra")
````

The REPL shows the result:

````
> printName(firstName="Hala", lastName="Terra")
Your name is Hala Terra
````



## Local functions

When functions are only accessed by other functions in the local scope, you can declare those other functions to be `private`, but in Kotlin you can make the other functions local to the outer function. In this example the functions `add` and `double` are defined inside the outer `addThenDouble` function:

````
fun addThenDouble(a: Int, b: Int): Int {
    fun add(a: Int, b: Int) = a + b  //local function
    fun double(a: Int) = a * 2       //local function
    return double(add(a, b))
}
````

The REPL shows that this works as desired:

````
> addThenDouble(1,1)
4

> addThenDouble(1,2)
6
````

Benefits:

- Minimize the scope of functions
- Make it easier to understand the outer function because you don’t need to look around through other code to see the source code for the other functions that it uses







