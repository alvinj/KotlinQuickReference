---
description: This page shows how object equality works in Kotlin, including the 'equals', '==', and '===' functions
---


# Object Equality

Comparing objects — class instances — in Kotlin is a little different than Java, and very similar to Scala.



## Key points

- `==` calls `equals` under the hood (structural equality)
- `===` is used to test reference equality
- Classes don’t have `equals` or `hashCode` methods by default, you need to implement them
- *Data classes* have automatically generated `equals` and `hashCode` methods



## `==` and `===`

This code shows how object equality works when a class *does not* have an `equals` method (`Person`) and when a class *does* have an `equals` method (`PersonWithEquals`):

````
class Person(var name: String)

class PersonWithEquals(var name: String) {
    override fun equals(that: Any?): Boolean {
        if (that == null) return false
        if (that !is PersonWithEquals) return false
        if (this.name == that.name) {
            return true
        } else {
            return false
        }
    }
}

fun main(args: Array<String>) {

    // Person (without `equals`)
    val p1 = Person("Joe")
    val p2 = Person("Joe")
    println(p1 == p2)   //false
    println(p1 === p2)  //false
    println(p1 === p1)  //true

    // PersonWithEquals
    val p1a = PersonWithEquals("Joe")
    val p2a = PersonWithEquals("Joe")
    println(p1a == p2a)   //true
    println(p1a === p2a)  //false
    println(p1a === p1a)  //true

}
````

Notes:

- You can write the `equals` function differently; I’m just trying to be obvious about the tests
- In the real world you should implement `hashCode`
- As you’ll see in the Data Classes lesson, a *data class* implements `equals` and `hashCode` for you
- See the “nullability” lessons for the meaning of `Any?`











