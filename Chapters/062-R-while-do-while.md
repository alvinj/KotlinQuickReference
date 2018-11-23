---
description: This page shows how to use Kotlin's while and do..while constructs, including several complete examples.
---


# while and do..while

Kotlin’s `while` and `do..while` constructs are just like Java. 


## while

Here’s `while`:

````
var i = 1

while (i < 5) {
    println(i++)
}
````

Here’s its output in the REPL:

````
>>> while (i < 5) {
...     println(i++)
... }
1
2
3
4
````

## do..while

Here’s do..while:

````
var i = 1

do {
    println(i++)
} while (i < 0)
````

and its REPL output:

````
>>> do {
...     println(i++)
... } while (i < 0)
1
````

Notice that do..while always runs at least once because it executes its body before running the first test.




