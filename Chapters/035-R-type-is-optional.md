---
description: In Kotlin you can declare a variable's type, or you leave the type off and let Kotlin infer it for you.
---


# Declaring the Type is Optional

As I showed in the previous lesson, when you create a new variable in Kotlin you can *explicitly* declare its type, like this:

````
val count: Int = 1
val name: String = "Alvin"
````

However, you can generally leave the type off and Kotlin can infer it for you:

````
val count = 1
val name = "Alvin"
````

In most cases your code is easier to read when you leave the type off, so this implicit form is preferred.



## The explicit form feels verbose

One thing you’ll find is that the explicit form feels verbose. For instance, in this example it’s obvious that the data type is `Person`, so there’s no need to declare the type on the left side of the expression:

````
val p = Person("Candy")
````

By contrast, when you put the type next to the variable name, the code feels unnecessarily verbose:

````
val p: Person = Person("Leo")
````

Summary:

````
val p = Person("Candy")           // preferred
val p: Person = Person("Candy")   // unnecessarily verbose
````


## Use the explicit form when you need to be clear

One place where you’ll want to show the data type is when you want to be clear about what you’re creating. That is, if you don’t explicitly declare the data type, the compiler may make a wrong assumption about what you want to create. Some examples of this are when you want to create numbers with specific data types. I show this in the next lesson.










