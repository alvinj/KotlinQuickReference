---
description: An introduction to Nullable Types in Kotlin.
---

<!-- 
REVIEW: THIS IS JUST AN INTRODUCTION FOR THIS SECTION OF THE BOOK.
-->


# Nullability: Introduction

*Nullability* is a Kotlin feature that’s intended to help you eliminate *NullPointerException*s in your code. We all know that [null pointer exceptions are bad](https://alvinalexander.com/scala/best-practice-eliminate-null-values-from-code-scala-idioms), and the features I introduce in the following lessons are Kotlin’s way of eliminating them.



## Two rules about using null values

Before you move into the following lessons, it’s worth mentioning that I like to think that there are two rules about using null values in Kotlin:

1. Never use null values!
2. When you’re forced to use null values — such as by using an old Java library — use Kotlin’s nullable types and the operators shown in the next few lessons.

With that point made, let’s jump into nullable types.



<!--
## Nullable types

Variables that are instances of standard Kotlin types can’t contain null values:

````
val>>> val s: String = null
error: null can not be a value of a non-null type String
val s: String = null
                ^

>>> val i: Int = null
error: null can not be a value of a non-null type Int
val i : Int = null
              ^
````

Similarly, variables that are instances of custom types can’t be null either:

````
>>> class Person (var name: String)

>>> val p: Person = null
error: null can not be a value of a non-null type Line_3.Person
val p: Person = null
                ^
````

A *nullable type* is a variation of a type that permits null values. You declare a type to be nullable by adding a question mark after it:

````
var s: String? = null
             _
````

Notice that no exceptions are thrown in the REPL when you declare a nullable type:

````
>>> var s: String? = null
>>> var i: Int? = null
>>> var p: Person? = null
````

Also notice that I declare those variables as `var` fields. I do this because nullable types will typically contain multiple values during their lifetime, especially if they’re declared to be null initially.

A brief summary so far:

- Default Kotlin types cannot contain null values.
- A nullable type is a variation of an existing type, and can contain a null value. The `?` operator says, “This instance of this type is allowed to contain a null value.”



## Nullable type operations are restricted

Because nullable types can contain null values, the operations you can perform on them are limited. For instance, you can’t call the `length` method on a `String?` instance:

````
> var s: String? = "fred"

> s.length
error: only safe (?.) or non-null asserted (!!.) calls are allowed on a nullable receiver of type String?
s.length
 ^
````

You also can’t assign a nullable type to its non-nullable equivalent:

````
val x: String? = null

val y: String = x  //error: type mismatch: inferred type is String? but String was expected
````

- TODO: stuff is checked at *compile time*, not runtime



## Discussion

- Java has Optional, Scala has Option; Kotlin takes a different approach


FROM KIA
--------

- *nullable types* - indicates which variables and properties are allowed to be null
    - syntax: String?, Int?, Person?
    - fun foo(s: String) ...  //can’t be null
    - fun foo(s: String?) ... //CAN be null

- variables can’t be null by default:

    var> var s = "yo"
    > s = null
    error: null can not be a value of a non-null type String
    s = null
        ^




## FROM https://www.raywenderlich.com/174395/kotlin-for-android-an-introduction-2

Examples like these are a good summary/explanation, especially the last one:

````
actionBar?.setDisplayHomeAsUpEnabled(true)
shareActionProvider?.setShareIntent(shareIntent)
val len = coverId?.length ?: 0
````

i.e., can you guess what this does:

````
val len = coverId?.length ?: 0
val len = aSquare?.sideLength ?: 0
val numLegs = aDog?.numLegs ?: 0
````


### Caution

Notice the possibility for error:

````
val numLegs = aDog?.numLegs ?: 0
````

Because you don’t really have a dog reference, saying that a dog has zero legs is not technically correct. The real situation here is that you don’t have a reference to a dog, not that the dog you were trying to get a reference to doesn’t have any legs.

-->








