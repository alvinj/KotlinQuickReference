---
description: This page contains a few preliminaries about the Kotlin programming language.
---


# Getting Started With Kotlin

I assume that you’re familiar with another language like Java, so I don’t spend much time on programming basics. That is, I assume that you’ve seen things like for-loops, classes, and methods before, so I generally only write, “This is how you create a class in Kotlin,” that sort of thing.

That being said, there are a few good things to know before you read this book.



## Download Kotlin

To run the examples in this book you’ll need to download the Kotlin compiler and runtime environment. Visit [kotlinlang.org](https://kotlinlang.org/) for information about how to use Kotlin from the command line, or in the IntelliJ IDEA, Android Studio, and Eclipse IDEs.

In this book I assume that you have the Java SDK and Kotlin command line tools installed.



## Comments

Comments in Kotlin are just like comments in Java (and many other languages):


````
// a single line comment

/*
 * a multiline comment
 */

/**
 * also a multiline comment
 */
````



## Naming conventions

Kotlin naming conventions follow the same “camel case” style as Java:

- Class names: `Person`, `StoreEmployee`
- Variable names: `name`, `firstName`
- Method names: `convertToInt`, `toUpper`

Also in regard to names, Kotlin source code files end with the *.kt* filename extension.



## Coding style

- I indent source code lines with four spaces, but that’s not a standard
- In this book I use `val` variables in all places, unless the feature I’m showing specifically requires the use of `var`







