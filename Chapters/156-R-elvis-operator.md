---
description: The Kotlin 'Elvis' operator is like a ternary operator, and this lesson shows examples of the Elvis operator.
---

<!--
- WORKING, EARLY
- Elvis operator is like a ternary operator

    val name: String = nullableName ?: "default_name"
    val postcode: String = nullableAddress?.postcode ?:  "default_postcode"
-->

# The Elvis Operator `?:`

The Safe-Call operator shown in the previous lesson is nice in many situations where a variable may contain a null value, and you’re okay with ending up with another null value when you use it in an expression. But what about those times where you want to handle that null value and return something besides `null`? That’s where the so-called “Elvis” Operator comes in.

>I don’t see it myself, but I’ve read that if you turn your head sideways the `?:` characters look a little like Elvis. The official name for this operator is the “Null Coalescing Operator,” and I think “Elvis Operator” is just easier to remember.



## Key points

- `?:` comes after a nullable type instance and can be read as “or else” or “if that’s null do this”
- `?.` returns null, but `?:` lets you return some other value besides `null`



## Examples

In the previous lesson I returned `String?` from my `toUpper` function. I do that because the function accepts a nullable string, and may therefore return a null value:

````
fun toUpper(s: String?): String? = s?.toUpperCase()
                       ---------
````

The Elvis operator — `?:` — is nice because it lets you easily return something besides `null`:

````
fun toUpper(s: String?): String = s?.toUpperCase() ?: "DUDE!"
                       --------                    --
````

Here’s how that function works:

````
>>> toUpper("foo")
FOO

>>> toUpper(null)
DUDE!
````

The use of the Safe-Call and Elvis operators in this example is equivalent to this code:

````
fun toUpper(s: String?): String {
    if (s != null) {
        return s.toUpperCase()
    } else {
        return "DUDE!"
    }
}
````



## Discussion

The `Option` class in the Scala programming language has a method called `getOrElse`, and the `Optional` class in Java has an `orElse` method. I find that the Elvis operator reminds me of these methods. It’s basically a way of saying “or else,” which you can see in this example:

````
fun toUpper(s: String?): String = s?.toUpperCase() ?: "DUDE!"
                                  ----------------    ----------------
                                  if s is not null    "or else" return
                                     return this            this
````

You can also think of the Elvis operator as being an operator named `ifThatsNullReturnThis`:

````
fun toUpper(s: String?): String = s?.toUpperCase() ifThatsNullReturnThis: "DUDE!"
````



## Another example

Here’s another example you can use for testing:

````
class Person (
    var firstName: String,
    var mi: String?,
    var lastName: String
)

fun main(args: Array<String>) {
    var p: Person? = null
    p = Person("Alvin", null, "Alexander")
    val mi = p?.mi ?: "<blank>"
    println("mi = $mi")  //prints "mi = <blank>"
}
````

<!--
    TODO create a better example, such as Pizza/Order/Customer/CreditCard
-->








