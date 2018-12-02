---
description: This page shows examples of how to create Kotlin classes, including the basic Scala class constructor.
---

<!--
    TODO: discuss `private` constructor (and others)
    TODO: discuss class annotations (more complicated examples of syntax)
-->

<!--
TODO: `internal` keyword on constructor, such as this example:
class TabAdapter internal constructor(fm: FragmentManager) : FragmentStatePagerAdapter(fm) {...
// internal is visible everywhere in the same “module”
// see https://kotlinlang.org/docs/reference/visibility-modifiers.html
-->


# Constructors and Members

In support of object-oriented programming (OOP), Kotlin provides a *class* construct. The syntax is much more concise than languages like Java and C#, but it’s also still easy to use and read.



## Overview

- Classes are created with the `class` keyword
- Primary constructor parameters go in the class header
    - `var` parameters are read-write, and `val` parameters are read-only
- Class instances are created *without* the `new` keyword
    - Think of it like you’re calling a function
- Classes can have initializer blocks
- Classes can have properties and methods (functions)
- Classes can have nested classes and inner classes



## Creating a class

Classes are created with `class` keyword:

````
class Foo
class Person constructor(var firstName: String, var lastName: String)
````

The primary constructor is part of the class header. If the primary constructor does not have any annotations or visibility modifiers, the `constructor` keyword can be omitted:

````
class Person(var firstName: String, var lastName: String)
````

I show annotations and visibility modifiers at the end of this lesson.



## How to create an instance of a class

New instances of classes are created *without* the `new` keyword. You can think of them as being like function calls:

````
val f = Foo()
val p = Person("Bill", "Panner")
````



## Comparison to Java

With the exception of the names of the getter and setter functions, if you’re coming to Kotlin from Java, this Kotlin code:

````
class Person(var firstName: String, var lastName: String)
````

is the equivalent of this Java code:

````
public class Person {

    private String firstName;
    private String lastName;
    
    public Person(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
    
    public String getFirstName() {
        return this.firstName;
    }
    
    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }
    
    public String getLastName() {
        return this.lastName;
    }
    
    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
    
}
````



## Constructor parameter visibility

Class constructor parameters are defined in the class header:

````
class Person(var firstName: String, var lastName: String)
             ---                    ---

class Person(val firstName: String, val lastName: String)
             ---                    ---
````

`var` means fields can be read-from and written-to (they are mutable); they have both a getter and a setter. `val` means the fields are read-only (they are immutable).


### Accessing constructor parameters

Given this definition with `var` fields:

````
class Person(var firstName: String, var lastName: String)
             ---                    ---
````

you can create a new `Person` instance like this:

````
val p = Person("Bill", "Panner")
````

You access the `firstName` and `lastName` fields like this:

````
println("${p.firstName} ${p.lastName}")
Bill Panner
````

The REPL shows that the fields can be updated:

````
> class Person(var firstName: String, var lastName: String)
> val p = Person("Bill", "Panner")

> p.firstName = "William"
> p.lastName = "Bernheim"

> println("${p.firstName} ${p.lastName}")
William Bernheim
````

### `val` fields are read-only

Had the fields been defined as `val`:

````
class Person(val firstName: String, val lastName: String)
             ---                    ---
````

you can still access them (via a getter method), but you can’t change their values (their is no setter method):

````
> class Person(val firstName: String, val lastName: String)
> val p = Person("Bill", "Panner")

// can access the fields
> println(p.firstName)
Bill
> println(p.lastName)
Panner

// can’t mutate the fields
> p.firstName = "William"
error: val cannot be reassigned
p.firstName = "William"
^
> p.lastName = "Bernheim"
error: val cannot be reassigned
p.lastName = "Bernheim"
^
````

Summary:

- `val` fields are read-only
- `var` fields are read-write

>Pro tip: If you use Kotlin to write OOP code, create your fields as `var` fields so you can easily mutate them. If you prefer an FP style of programming you may prefer Kotlin’s *data classes*. (More on this later.)



## A note about annotations and visibility modifiers

Per [the Kotlin documentation](https://kotlinlang.org/docs/reference/classes.html), “If the constructor has annotations or visibility modifiers, the `constructor` keyword is required, and the modifiers go before it”:

````
class Customer public @Inject constructor(name: String) { ... }
                              -----------
````


## Visibility modifiers

Visibility modifiers are:

- private
- protected 
- internal
- public

Per [this kotlinlang.org link](https://kotlinlang.org/docs/reference/visibility-modifiers.html#modules), “classes, objects, interfaces, constructors, functions, properties and their setters can have visibility modifiers.”

Here’s an example of `internal`:

````
// `internal` is visible everywhere in the same “module”
// see https://kotlinlang.org/docs/reference/visibility-modifiers.html
class TabAdapter internal constructor(fm: FragmentManager) : FragmentStatePagerAdapter(fm) {...
                 --------
````









