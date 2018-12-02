---
description: This lesson provides an introduction to 'companion objects' in Kotlin, including writing 'apply' and 'unapply' methods.
---


# Companion Objects (TODO)

- Similar to Scala
- Create a companion object inside a class
- A way of adding static methods to a class
- Factory pattern: private constructor in class + factory method in companion object
- TODO: Document rules about relationship between a class and its companion object



## Syntax

From Kotlin Language Reference (TODO: write my own example):

(1) Give the companion object a name:

````
class MyClass {
    companion object Factory {
        fun create(): MyClass = MyClass() 
    }
}

val instance = MyClass.create()
````

(2) No name on companion object:

````
class MyClass {
    companion object { } // will be called "Companion"
}
fun MyClass.Companion.foo() { ... }
````



## Notes

- Style/Idiom: Use package-level functions instead of static methods in companion objects? (Noted in Kotlin Language Reference)



## TODO

- `@JvmStatic` annotation
- From Kotlin Language Reference, p. 83: “Note that, even though the members of companion objects look like static members in other languages, at runtime those are still instance members of real objects, and can, for example, implement interfaces:”






