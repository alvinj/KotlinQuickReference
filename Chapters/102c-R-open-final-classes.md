---
description: This lesson provides an introduction to making classes and functions 'open' (because they are 'final' by default).
---

# Open and Final Classes


## Key points

- Because of a concern about the “fragile base class” problem, Kotlin classes and their functions are `final` by default
- To allow a class to be extended it must be marked `open`, meaning that it’s “open to be extended”
- To allow class functions and fields to be overridden, they must also be marked `open`



## Classes and functions are final by default

I’ll demonstrate how this works through a series of examples. 


### (1) Class and function are not open

In this first example, `Child` won’t compile because `Parent` and its function `name` are `final` (by default):

````
class Parent {            //class is final by default
    fun name() = "base"   //function is final by default
}

// this won’t compile
class Child : Parent() {
    override fun name() = "Child"
}

// error messages:
error: this type is final, so it cannot be inherited from
class Child : Parent() {
              ^
error: 'name' in 'Parent' is final and cannot be overridden
    override fun name() = "Child"
    ^
````


### (2) Class is open, function is not

In this example, `Parent` is now open, but because `name` isn’t open the code still won’t compile:

````
open class Parent {
    fun name() = "base"
}

class Child : Parent() {
    override fun name() = "Child"   //intentional error
}

// error message:
error: 'name' in 'Parent' is final and cannot be overridden
    override fun name() = "Child"   //intentional error
    ^
````

### (3) Success: Class and function are open

Finally, with `Parent` and `name` both being marked `open`, this code will compile:

````
open class Parent {
    open fun name() = "base"
}

class Child : Parent() {
    override fun name() = "Child"
}
````

Also, note the need for the `override` modifier on `Child::name`.



## Closing an open method

To begin looking at an interesting problem, notice that `foo` is defined to be `open` in class `A`, and then it is overridden in both class `B` and then class `C`:

````
open class A {
    open fun foo() = "foo in A"
}

open class B : A() {
    override fun foo() = "foo in B"
}

open class C : B() {
    override fun foo() = "foo in C"
}
````

This code is perfectly legal; so far, so good.

Now, if you’re writing class `B` and don’t want your subclasses to override `foo`, you can mark `foo` as `final` in your class:

````
open class A {
    open fun foo() = "foo in A"
}

open class B : A() {
    // added `final` here
    final override fun foo() = "foo in B"
}

open class C : B() {
    // this won’t compile because `foo` is marked
    // `final` in B
    override fun foo() = "foo in C"
}

// error:
error: 'foo' in 'B' is final and cannot be overridden
````

Similarly, if you take the `open` off of class `B`, class `C` will no longer compile:

````
open class A {
    open fun foo() = "foo in A"
}

// removed `open` here
class B : A() {
    override fun foo() = "foo in B"
}

// this code won’t compile because B is closed
open class C : B() {
    override fun foo() = "foo in C"
}

// error message:
error: this type is final, so it cannot be inherited from
open class C : B() {
               ^
````



## More information: Fragile base classes

To understand Kotlin’s approach with classes and functions, you first have to understand the “fragile base class” problem. [Wikipedia describes it](https://en.wikipedia.org/wiki/Fragile_base_class) like this:


“The fragile base class problem is a fundamental architectural problem of object-oriented programming systems where base classes (superclasses) are considered ‘fragile’ because seemingly safe modifications to a base class, when inherited by the derived classes, may cause the derived classes to malfunction. The programmer cannot determine whether a base class change is safe simply by examining the methods of the base class in isolation.”

This is a problem in Java, where classes and methods are open by default. To fix the problem, as Joshua Block writes in his classic book, [Effective Java](TODO:https://amzn.to/2Ks3iqY), to protect against this problem, developers should “Design and document for inheritance or else prohibit it.”

Because of this experience in Java, the Kotlin designers decided to make all classes and methods `final` by default. That way, you can “design for inheritance” by marking classes and functions as `open` only when you really want them to be open to extension.
















