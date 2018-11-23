---
description: This page shows how Kotlin 'data classes' work, including their syntax, benefits, and examples.
---


# Data Classes

Sometimes you just need to create classes to hold data, like structs in the C programming language. Kotlin *data classes* give you a way to create data structures that have automatically-generated functions that make them very useful. If you’re familiar with Scala’s *case classes*, data classes are almost exactly the same.

>Data classes are generally intended for use in a functional programming (FP) environment, but OOP developers can use them as well.



## Key points

- In FP you create classes just to hold data, like structs in C
- Kotlin *data classes* are useful for this purpose
- The compiler automatically generates the following functions for data classes:
    - `equals()` and `hashCode()` methods
    - a useful `toString()` method
    - a `copy()` function that is useful in an [update as you copy](https://alvinalexander.com/scala/fp-book/update-as-you-copy-dont-mutate-case-classes) scenario
    - “componentN” functions are created to let you destructure an instance into its constructor fields
- Data classes are like regular Kotlin classes, but because they’re intended to hold data, the primary constructor must have at least one parameter



## Functional programming

While data classes may be useful for OOP, they’re primarily intended for the FP paradigm:

- FP developers create data classes with all `val` constructor parameters
- All instances of data classes are also `val`

In FP, all variables and all collections are immutable, so the features of data classes are especially useful when everything is immutable, the only way to update variables is to update them as you make a copy of them.

>See my book, [Functional Programming, Simplified](https://alvinalexander.com/scala/functional-programming-simplified-book) for *many* more details on this.



## Example

First, here are some operations on a regular Kotlin class:

````
class Person(
    val name: String,
    val age: Int
)

fun main(args: Array<String>) {

    val p1 = Person("Jane Doe", 30)
    val p2 = Person("Jane Doe", 30)

    println(p1.name)   //Jane Doe
    println(p1.age)    //30

    println(p1 == p2)  //false
    println(p1)        //Person@49476842

}
````

Notice that `p1` does not equal `p2` and `p1` does not print very well.

Next, just put the keyword `data` before the class to create a data class:

````
data class Person(
    val name: String,
    val age: Int
)

fun main(args: Array<String>) {

    val p1 = Person("Jane Doe", 30)
    val p2 = Person("Jane Doe", 30)

    println(p1.name)   //Jane Doe
    println(p1.age)    //30

    println(p1 == p2)  //true
    println(p1)        //Person(name=Jane Doe, age=30)

    val p3 = p2.copy(name = "Jane Deer")
    println(p3)        //Person(name=Jane Deer, age=30)

}
````

Notice:

- `p1` equals `p2` (because `equals` and `hashCode` are generated for you)
- `Person` is readable when you print it out
- Use the `copy` function to create a modified variable



## Getter/setter functions for constructor parameters

For OOP developers, data class constructor parameters can also be a `var`:

````
data class Person (
    var name: String,
    var age: Int
)

fun main(args: Array<String>) {
    val p = Person("Jane Doe", 30)
    p.name = "Jane Deer"  //setter function
    p.age = 31            //setter function
    println(p)            //Person(name=Jane Deer, age=31)
}
````

Key points:

- `var` constructor parameters will have both getter and setter methods
- `val` constructor parameters will have only getter methods
- All constructor parameters are included in the `toString()` output



## Data class properties don’t print

Data classes can also have properties — such as `age` in this next example — but notice that they don’t print out; only constructor fields are included in `toString()` output:

````
data class Person (var name: String) {
    var age: Int = 0
}

fun main(args: Array<String>) {
    val p = Person("Jane Doe")
    p.age = 30
    println(p)   //Person(name=Jane Doe)  <-- no age here
}
````



## `equals()` and `hashCode()`

As shown earlier, data classes have automatically-generated `equals` and `hashCode` methods, so instances can be compared:

````
data class Person(
    val name: String,
    val age: Int
)

val p1 = Person("Jane Doe", 30)
val p2 = Person("Jane Doe", 30)

println(p1 == p2)  //true
````

These methods also let you easily use data class instances in collections like sets and maps.



## `toString()`

As shown, data classes have a good default `toString()` method implementation, which at the very least is helpful when debugging code:

````
val p = Person("Jane Doe", 30)
p   //Person(name=Jane Doe, age=30)
````



## “componentN” functions

Functions are generated for data classes that enable them to be used in destructuring declarations:

````
// create a Person
val p = Person("Jane Doe", 30)

// destructure the person into its fields
val (name, age) = p
println("$name is $age")   //"Jane Doe is 30"

// field names aren’t important
val (a, b) = p
println("$a is $b")        //"Jane Doe is 30"
````

Only constructor fields are destructured this way.



## Copying

As shown earlier, a data class also has an automatically-generated `copy` method that’s extremely helpful when you need to perform the process of a) cloning an object and b) updating one or more of the fields during the cloning process:

````
> data class BaseballTeam(val name: String, val lastWorldSeriesWin: Int)
> val cubs1908 = BaseballTeam("Chicago Cubs", 1908)
> val cubs2016 = cubs1908.copy(lastWorldSeriesWin = 2016)

> cubs1908
BaseballTeam(name=Chicago Cubs, lastWorldSeriesWin=1908)

> cubs2016
BaseballTeam(name=Chicago Cubs, lastWorldSeriesWin=2016)
````

When you use the `copy` method just supply the names of the fields you want to modify during the cloning process.

Because you never mutate data structures in FP, this is how you create a new instance of a class from an existing instance. I refer to this process as “update as you copy,” and I discuss this process in detail in my book, [Functional Programming, Simplified](https://alvinalexander.com/scala/functional-programming-simplified-book).










