---
description: This lesson provides an introduction to Nullable Types in Kotlin.
---

<!--
TODO: ADD THIS: Checks are performed at compile time, not runtime, so there is no performance overhead. (not my words. verify/attribute it.)

TODO: Note that nullable types are typically `var` fields.
-->


# Nullable Types

Nullable types are an approach in Kotlin to help you eliminate null values and null pointer exceptions (the dreaded `NullPointerException`). Here are the main concepts.



## Key points

These are the key points of this lesson:

- A variable of type `String` can never be null
- A variable of the nullable type `String?` can be null
- The operations that can be performed on nullable types are very limited

I use `String` in those statements, but the same things can be said about every other type, including `Int`, `Float`, `Person`, etc.



## Standard types can’t be null

Variables that are instances of standard Kotlin types can’t contain null values:

````
val> val s: String = null
error: null can not be a value of a non-null type String
val s: String = null
                ^

> val i: Int = null
error: null can not be a value of a non-null type Int
val i : Int = null
              ^
````

Similarly, variables that are instances of custom types can’t be null either:

````
> class Person (var name: String)

> val p: Person = null
error: null can not be a value of a non-null type Line_3.Person
val p: Person = null
                ^
````



## Nullable types

A *nullable type* is a variation of a type that permits null values. You declare a type to be nullable by adding a question mark after it:

````
var s: String? = null
             _
````

This simple addition to your type allows your variable to contain null values. Notice that no exceptions are thrown in the REPL when you declare a nullable type:

````
> var s: String? = null
> var i: Int? = null
> var p: Person? = null
````

Also notice that I intentionally declare those variables as `var` fields. I do this because they’re declared with null values, but at some point later in their lifetime they’ll presumably contain more useful values.



## Summary

A brief summary so far:

- Default Kotlin types cannot contain null values.
- A nullable type is a variation of an existing type, and can contain a null value. The `?` operator says, “This instance of this type is allowed to contain a null value.”

As mentioned in the previous chapter, you should write your code to never use null values. Allowing null values in your code is considered a “bad smell.” (When I look at code that permits null values I think, “How quaint, this is like code from 1996.”)



## Places where you’ll use nullable types

You’ll use and encounter nullable types in several areas:

- Variable assignment
- Function parameters
- Function return values
- Converting a nullable type to its non-nullable equivalent

Here’s what those situations look like. You’ve already seen variable assignment:

````
var s: String? = null
````

This is a function parameter:

````
fun foo(s: String?) ...
````

This is a nullable type used as a function return value:

````
fun foo(): String? = ...
````

You may also need to handle the process of converting a nullable type to its non-nullable equivalent:

````
val x: String? = null
val y: String = x    // error: this won’t compile
````

If you attempt to write the code as shown, you’ll see this error message on the second line:

````
//error: type mismatch: inferred type is String? but String was expected
````

I’ll show how to handle this situation in the following lessons.



## Nullable types are limited

Because a nullable type can be `null`, in order for them to be safe to work with, the methods you can call on them are intentionally very restricted. As you can imagine, if you try to call a function like `length()` on a null string, it will throw a null pointer exception. Therefore, a `String?` instance doesn’t have a `length` property:

````
> var s: String? = "fred"

> s.length
error: only safe (?.) or non-null asserted (!!.) calls are allowed
on a nullable receiver of type String?
s.length
 ^
````

A `String?` instance also doesn’t have a `toUpperCase()` function:

````
> s.toUpperCase()
error: only safe (?.) or non-null asserted (!!.) calls are allowed
on a nullable receiver of type String?
s.toUpperCase()
 ^
````

That error message is Kotlin’s way of saying, “`String?` doesn’t have this functionality.”

This is an important point: a `String?` isn’t the same as a `String`. For example, with Kotlin 1.5.2, a `String` instance has well over 100 functions that can be called on it, while a `String?` has only 13. You can think of `String?` as being a limited subset of a `String`.

>Note 1: Nullability concepts are enforced by the compiler at compile-time.

>Note 2: I’ll discuss the `?.` and `!!.` operators you see referenced in those error messages in the lessons that follow.



## Coming soon: Operators to help you

While you can work with nullable types manually by checking for null values in if/then expressions:

````
val len = if (s != null) s.length else 0
````

that code is verbose, and it only gets worse when you have several nullable types. Therefore, this style of code is considered a bad practice, and Kotlin has operators to help you work with nullable types. Those operators will be demonstrated in the lessons that follow.








