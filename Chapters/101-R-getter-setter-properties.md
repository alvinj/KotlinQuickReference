---
description: This page shows examples of how to define custom getter and setter methods on Kotlin classes, including how to work with the 'field' reference.
---

# Custom Class Field Getters and Setters


## Key points

- Kotlin classes can have *properties* (what we call *fields* in Java)
- Properties can be defined as `val` or `var`
- `val` fields are read-only, `var` fields are read-write
- Fields are accessed directly by their name, just like constructor parameters
- TODO: Properties are public by default, but can also be private
- You can write custom getter and setter (accessor and mutator) methods for your properties with a special syntax
- The getter/setter methods can use a “backing field” named `field` (TODO: `field` is kind of a reserved word in Kotlin but not really)



## A field without custom getters or setters

If you just want a simple property in a class that you can read and modify, declare the field as a `var`:

````
class Person() {
    var name = ""
}

// create an instance
>>> val p = Person()

// no initial value
>>> p.name

// set the value
>>> p.name = "Al"

// get (access) the value
>>> p.name
Al
````

That shows how to get and set values of a simple property.



## Custom get/set methods

Conversely, if you want to create custom get/set methods, define custom `get()` and `set()` methods just below the property. For example, imagine that you want to make a log entry every time someone accesses or updates the `name` of a `Person`:

````
class Person {
    var name: String = "<no name>"
        get() {
            println("OMG, someone accessed 'name'")
            return field
        }
        set(s) {
            println("OMG, someone updated 'name' to be '$s'")
            field = s
        }
}
````

The REPL shows how this works:

````
>>> val p = Person()

>>> p.name
OMG, someone accessed 'name'
<no name>

>>> p.name = "Al"
OMG, someone updated 'name' to be 'Al'

>>> p.name
OMG, someone accessed 'name'
Al
````

Key points:

- The getter/setter methods can use a “backing field” named `field`
- `field` is a way of referencing the value you’re referencing, in this case the `name` field
- `field` is made available to you, but you don’t have to use it
- Per [the official Kotlin documentation](https://kotlinlang.org/docs/reference/properties.html), “A backing field will be generated for a property if it uses the default implementation of at least one of the accessors, or if a custom accessor references it through the field identifier.”



## More examples

Here are a few more examples of Kotlin’s getter/setter approach.

First, a one-line getter with a multiline setter, both using the special backing field:

````
class Foo {
    var prop: String = "initial value"
        get() = field  //no real need for this, just showing syntax
        set(s) {
            // do whatever you want with `s` ...
            // then:
            field = s
        }
}
````

Second, multiline getters and setters:

````
class Bar {
    var name = ""
        get() {
            val s = if (field == "") "hello" else "hello, ${field}"
            return s
        }
        set(s) {
            // do whatever you want with `s`
            field = s
        }
}
````

This is how you can use your own “backing field” instead of `field`:

````
class Baz {
    private var _name = ""
    var name = ""
        fun get() = _name
        fun set(s: String) {
            _name = s
        }
}
````

Finally, here’s an example that shows get/set methods alongside other functions in a class:

````
class BlogPost {
    var content = ""
        get() {
            logAccess(Date())
            return field
        }
        set(s) {
            logUpdate(Date(), s)
            field = s
        }
    fun logAccess(d: Date) {
        println("logAccess called ...")
        //...
    }
    fun logUpdate(d: Date, s: String) {
        println("logUpdate called ...")
        //...
    }
}
````










