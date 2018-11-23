---
description: This page shows examples of the Kotlin 'when' expression, which is like a more powerful 'switch' statement.
---


# `when` Expressions

Kotlin `when` expressions are like Java `switch` statements, but you’ll see in this lesson, they’re much more powerful. If you’re experienced with Scala, `when` is similar to Scala’s `match` expression.



## Replacement for `switch`

In its most basic use, `when` can be used as a replacement for a Java `switch` statement:

````
val dayAsInt = 1

when (dayAsInt) {
    1 -> println("Sunday")
    2 -> println("Monday")
    3 -> println("Tuesday")
    4 -> println("Wednesday")
    5 -> println("Thursday")
    6 -> println("Friday")
    7 -> println("Saturday")
    else -> {
        // notice you can use a block
        println("invalid day")
    }
}
````



## `when` is an expression

`when` can also be used as an expression, meaning that it returns a value:

````
val dayAsInt = 1

val dayAsString = when (dayAsInt) {
    1 -> "Sunday"
    2 -> "Monday"
    3 -> "Tuesday"
    4 -> "Wednesday"
    5 -> "Thursday"
    6 -> "Friday"
    7 -> "Saturday"
    else -> "invalid day"
}

println(dayAsString)
````

### Matches must be exhaustive

When `when` is used as an expression you generally must include an `else` clause. If you don’t, you risk the chance of getting an error, as in this example:

````
val i = 0

val result = when (i) {
    1 -> "a little odd"
    2 -> "a little even"
}
````

That code produces this error message:

````
error: 'when' expression must be exhaustive, add necessary 'else' branch
val result = when (i) {
             ^
````



## Multiple branch conditions

When you have multiple branch conditions with constants that should be handled the same way, they can be combined in one statement with a comma:

````
when (i) {
    1,2,3 -> println("got a 1, 2, or 3")
    4,5,6 -> println("got a 4, 5, or 6")
    else  -> println("something else")
}
````



## Testing against ranges

You can also check a value for being in a range (`in`) or not in a range (`!in`):

````
val i = 1

when (i) {
    in 1..3  -> println("1, 2, or 3")
    !in 4..5 -> println("not a 4 or 5")
    else     -> println("something else")
}

// result: 1, 2, or 3
````

The order of the expressions is important. In this example I reverse the first two possible matches, and get a different result:

````
val i = 1

when (i) {
    !in 4..5 -> println("not a 4 or 5")
    in 1..3  -> println("1, 2, or 3")
    else     -> println("something else")
}

// result: not a 4 or 5
````

These examples also show that the `when` expression stops on the first statement that matches the given value.


### `in` with `listOf`

Similar to ranges, you can also use `in` with `listOf` as the predicate condition:

````
val i = 1
when (i) {
    in listOf(1,3,5) -> println("a little odd")
    in listOf(2,4,6) -> println("a little even")
    else             -> println("something else")
}
````



## Expressions as branch conditions

`when` expressions aren’t limited to using only constants, you can also use any sort of predicate as a branch condition. Here are some tests with Kotlin’s `is` operator:

````
val x: Any = 11.0

when (x) {
    is Boolean -> println("$x is a Boolean")
    is Double  -> println("$x is a Double")
    is String  -> println("$x is a String")
    !is String -> println("$x is not a String")
    else       -> println("$x is something else")
}
````

When you run that code as shown the result is:

````
11.0 is a Double
````

Here’s an example that demonstrates how to use a function (`toUpperCase()`) in a branch condition:

````
fun isUpperCase(s: String): Boolean {
    return when (s) {
        s.toUpperCase() -> true
        else -> false
    }
}
````

The REPL shows how this works:

````
>>> isUpperCase("FOO")
true

>>> isUpperCase("foo")
false

>>> isUpperCase("Foo")
false
````



## `when` without arguments

If you don’t give `when` an argument, it can be used as a replacement for an if/else expression:

````
val i = 1

when {
    i < 0  -> println("less than zero")
    i == 0 -> println("zero")
    else   -> println("greater than zero")
}
````

>Key point: Notice that this example uses `when`, and not `when(i)`.

This syntax is useful for using `when` as the body of a function:

````
fun intToString(i: Int): String = when {
    i < 0  -> "a negative number!"
    i == 0 -> "0"
    else   -> "a positive number!"
}
````

Notice in this example that `when` is used as the body of the `intToString` function, and returns a `String`. If you haven’t seen that approach before, it can help to see it broken down into steps:

````
fun intToString(i: Int): String {
    // convert the Int to a String
    val string = when {
        i < 0  -> "a negative number!"
        i == 0 -> "0"
        else   -> "a positive number!"
    }
    // return the String
    return string
}
````



## Smart casts with `when`

When you use an `is` expression as a branch condition you can check the type of the variable passed into `when`, and call methods on it on the right-hand side of the expression. Here’s an example:

````
fun getInfo (x: Any): String {
    return when (x) {
        is Int    -> "The Int plus one is ${x + 1}"
        is String -> "Got a String, length is " + x.length
        else -> "Got something else"
    }
}
````

Here’s what the function looks like if you call it several times with different types:

````
println(getInfo(1))      //The Int plus one is 2
println(getInfo("foo"))  //Got a String, length is 3
println(getInfo(1L))     //Got something else
````



## Even more!

While that covers most of `when`’s functionality, there are even more things you can do with it.










