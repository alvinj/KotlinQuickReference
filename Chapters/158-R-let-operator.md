---
description: TODO
---

<!--
NOTE: this is a rough first draft about using `let`.

NOTE TO SELF: The `null` you see in the Kotlin REPL isn’t printed by the code, it’s the result of the `let` expression. This can be confusing, as I wasted some time trying to figure it out.
-->


# The `let` Operator

The `let` operator is an interesting construct that lets you run an algorithm on a variable inside a closure. When it’s combined with the Safe-Call operator you can think of the approach as, “If the value exists, run this algorithm with the value.” This is best shown by example.



## `let` by itself

To get started, let’s see how `let` works by itself — without the Safe-Call operator. Here’s an example:

````
> val name = "foo"

> name.let { println("`it` is $it") }
`it` is foo
kotlin.Unit
````

TODO: IS "closure" THE CORRECT NAME FOR THIS?

The first line of the REPL output shows that the `println` statement is executed, and the value of `it` is the string `"foo"`. This is how `let` works; it makes the value of the variable it’s applied to available inside the closure. The value in the closure is available through the variable `it`, but you can also use the “named parameter” approach, if you prefer:

````
// named parameter
name.let { s -> println("`s` is $s") }
           -                    --
````

That code works just like the previous `it` example.


### `let` has a return value

Before you move on, notice that the second line of output in the Kotlin REPL is this:

````
kotlin.Unit
````

This line is printed because `let` has a return value. The previous example just printed to STDOUT, so there is no return value, so the REPL shows `kotlin.Unit`. Here’s an example that has a more useful return value:

````
> "foo".let { it.length }
3
````

In this example `it` contains the string `"foo"`, and `"foo".length` is `3`, which is the value returned. In the real world you’ll often assign the result from `let` to a variable, like this:

````
> val len = "foo".let { it.length }

> len
3
````



## Using `let` with the Safe-Call operator

Now that you’ve seen how to use `let` by itself, let’s look at how to use it in combination with the safe-call operator.

Given a `String?` value which may or may not be null:

````
val name: String? = null
//name might be changed later ...
````

You can print the value, if it exists:

````
name?.let { println("The name is $it") }
````

If `name` is null you won’t see any output; `let` is smart enough to know that the value is null, so the closure won’t be executed. But if it happens to contain a value, such as the string `"Al"`, you’ll see output like this:

````
"The name is Al"
````


### The advantage of `let`

Using `let` with the Safe-Call operator is the same as writing this code:

````
if (name != null) {
    // do something with `name`
}
````

The advantage of `let` is that it’s more concise than constantly writing `if` statements like that.


### A space before `let`

Note that if you prefer, you can also write that expression like this, with space before `let`:

````
name?. let { println("The name is $it") }
````

Some people find that approach more readable.



## Lambda syntax and `let`

In a related note, you can write a lambda expression with `let` using a named parameter, like this:

````
// named param
toUpper(name)?.let { s -> println("Hello $s") }
                     -                   --
````

You can also write the lambda expression as I’ve shown previous in this lesson, with the special `it` variable name:

````
// `it`
toUpper(name)?.let { println("Hello $it") }
                                    ---
````



## Key points

- if the value is null, `let` does nothing
- if the value is not null, `let` runs your algorithm
- `let` provides its own function scope and can be called on any value (NerdGuide)



## TODO

- difference(s) between `let`, `run`, and `apply`
    - from my tests, `let` seems to create access to `it`, `run` does not
    - per book, "let returns the value of the closure"
        - per my test, `apply` doesn’t create an `it` reference

- how `let` works:

    > "foo".let { println(it) }
    foo



















