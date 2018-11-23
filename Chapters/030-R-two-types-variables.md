---
description: The Kotlin language has two types of variables, known as 'val' and 'var' variables.
---


# Two Types of Variables

Kotlin has two types of variable declarations:

- `val` creates an *immutable* variable (like `final` in Java)
- `var` creates a *mutable* variable

Examples:

````
val s = "hello"   // immutable
var i = 42        // mutable

val p = Person("Hala")
````

Notes:

- Kotlin can usually infer the variable’s data type from the code on the right side of the `=` sign.
- This is considered an *implicit* form.
- You can also *explicitly* declare the variable type if you prefer:

````
val s: String = "hello"
var i: Int = 42
````

- The implicit form is generally preferred
- I use the explicit form when I don’t think the type is obvious; code is easier to maintain that way



## The difference between `val` and `var`

The REPL shows what happens when you try to reassign a `val` field:

````
> val a = 'a'

> a = 'b'
error: val cannot be reassigned
a = 'b'
^
````

That fails with a “val cannot be reassigned” error, as expected. Conversely, you can reassign a `var`:

````
> var a = 'a'

> a = 'b'

> a
b
````

The general rule is that you should always use a `val` field unless there’s a good reason not to. This simple rule has several benefits:

- It makes your intention obvious: you don’t want this field to be reassigned
- It makes your code more like algebra 
- If you ever want to go there, it helps get you started down the path to *functional programming*, where *all* fields are immutable



## “Hello, world” with a `val` field

Here’s a “Hello, world” app with a `val` field:

````
fun main(args: Array<String>) {
    val s = "Hello, world"
    println(s)
}
````

As before:

- Save that code in a file named *HelloVal.kt*
- Compile it with `kotlinc HelloVal.kt -include-runtime -d HelloVal.jar`
- Run it with `java -jar HelloVal.jar`



## Deferred initialization of `val`

Per [Kotlin in Action](https://amzn.to/2DJtTAW), “a `val` variable must be initialized exactly once during the execution of the block where it’s defined ... but you can initialize it with different values depending on some condition.” Examples:

````
val name: String
val num: Int

val r = (1..10).shuffled().first()

// assign `name` and `num`
name = if (r % 2 == 0) "Alvin" else "Alexander"
num = r

println("name = $name, num = $num")
````



## A note about `val` fields in the REPL

You can’t reassign a `val` field in the REPL:

````
> val age = 18

> age = 19
error: val cannot be reassigned
age = 19
^
````

However, you can do this in the REPL:

````
> val age = 18

> val age = 19
````

I thought I’d mention that because I didn’t want you to see it one day and think, “Hey, Al said `val` fields couldn’t be reassigned.” They can be reassigned like that, but only in the REPL.










