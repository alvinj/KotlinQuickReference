---
description: TODO
---

<!--
NOTE: this is a rough first draft about using `?.`
-->


# The Safe-Call Operator

A main operator you’ll use with nullable types is called the *safe-call operator*, and as you’ll see in this lesson, it’s represented by the symbol `?.` (a question mark followed by a period).



## Background

If Kotlin had nullable types but didn’t have any other operators to work with them, you’d always have to use if/then checks to work with them, like this:

````
fun toUpper(s: String?): String? = if (s != null) s.toUpperCase() else null
````
That function isn’t too helpful, but it does help keep you from throwing null pointer exceptions. The REPL shows how it works:

````
>>> toUpper("al")
AL

>>> toUpper(null)
null
````



## The safe-call operator

Fortunately Kotlin has a safe-call operator that does the same thing:

````
fun toUpper(s: String?): String? = s?.toUpperCase()
````

The REPL shows that this function works just like the previous one:

````
>>> toUpper("al")
AL

>>> toUpper(null)
null
````

In summary, these two pieces of code are equivalent:

| Safe-Call Operator | Manual check |
| ------------------ | ------------ |
| `s?.toUpperCase()` | `if (s != null) s.toUpperCase() else null` |



## Chaining safe calls together

In the real world, a field of one class may be a nullable type, and that class may have another nullable type, and so on. For example, in the following code `Order` has the nullable field `customer`; the `Customer` type has a nullable field `address`; and `Address` has a nullable field `street2`:

````
class Order (
    var customer: Customer?,
    var pizzas: List<Pizza>
)

class Customer (
    var name: String,
    var address: Address?
)

class Address (
    var street1: String,
    var street2: String?,
    var city: String,
    var state: String,
    var zip: String
)

class Pizza(
        //...
)
````

A great thing about the safe-call operator is that it can be chained together so you can access the `street2` field like this:

````
val street2Address = order.customer?.address?.street2
````

That syntax can be read as, “Reach inside the `order` instance and if the `customer` field is not null, and its `address` field is not null, give me the `street2` value (which may be null). However, if `customer` or `address` are null, give me a `null` value.”

It’s important to know that `street2Address` may still be null, but the key here is that this code won’t throw a `NullPointerException` if `customer`, `address`, or `street2` is null.



## Complete code example

Here’s a larger example of using the safe-call operator:

````
class Order (
    var customer: Customer?,
    var pizzas: List<Pizza>
)

class Customer (
    var name: String,
    var address: Address?
)

class Address (
    var street1: String,
    var street2: String?,
    var city: String,
    var state: String,
    var zip: String
)

class Pizza(
    //...
)

fun main(args: Array<String>) {
    val address = Address(
        "123 Main",
        null,
        "Talkeetna",
        "Alaska",
        "99676"
    )

    // customer has no address
    var customer = Customer("Al", null)
    val order = Order(customer, emptyList<Pizza>())
    println("test1: ${order.customer?.address?.street2}")   //null

    // customer has address but no 'street2'
    customer.address = address
    println("test2: ${order.customer?.address?.street2}")   //null

}
````



## Null object pattern

Depending on your needs, don’t forget about the *Null Object Pattern*. Here’s a link to a [Scala null object pattern example](https://alvinalexander.com/scala/best-practice-eliminate-null-values-from-code-scala-idioms#the-null-object-pattern) I put together.










