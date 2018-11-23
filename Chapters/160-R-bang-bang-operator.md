---
description: How to use Kotlin’s Force operator, i.e., the !! symbol, to convert nullable types to their non-nullable equivalent.
---

<!-- FIRST DRAFT DONE -->


# The “Force” Operator (`!!`)

Kotlin also includes an operator generally known as the Force Operator. It lets you convert a nullable type to its non-nullable equivalent, such as converting a `String?` to a `String`, and it should only be used when you are 100% certain that a nullable type isn’t null.

>The official name of this operator is the “Non-null assertion operator.”



## Examples

If you’re 100% certain that a nullable type doesn’t contain a null value, you can convert it to its non-nullable equivalent, like this:

````
> val s1: String? = "Christina"

> val s2: String = s1!!

> s2
Christina
````

However, beware that if the nullable type does contain a null value you’ll get a null pointer exception during this process:

````
> val s1: String? = null

> val s2: String = s1!!
kotlin.KotlinNullPointerException
````



## Check for null before using `!!`

Getting a null pointer exception defeats the entire purpose of using nullable types, so the typical way of using the `!!` operator is to test that the nullable variable isn’t null before doing the assignment, like this:

````
var nullableName: String? = null

// nullableName may be reassigned ...

var name = ""

if (nullableName != null) {
    name = nullableName!!
}
````



## Key points

A few key points about the Force operator:

- `!!` gives you a way to convert a nullable type to its non-nullable equivalent
- Be careful, it will throw a `kotlin.KotlinNullPointerException` if the value is null

And one note about when you should use the Force operator:

- Rarely!!

In general, there are better ways to use nullable types rather than converting them all to their non-nullable equivalent.








