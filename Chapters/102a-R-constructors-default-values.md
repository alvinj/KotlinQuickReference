---
description: This page shows how to provide default values for Kotlin constructor parameters, with several examples.
---


# Constructor Default Values and Named Arguments

Kotlin has two nice features that you’ll also find in Scala:

- You can supply default values for constructor parameters
- You can use named arguments when calling a constructor



## Default values for constructor parameters

A convenient Kotlin feature is that you can supply default values for constructor parameters. For example, you *could* define a `Socket` class like this:

````
class Socket(var timeout: Int, var linger: Int) {
    override def toString = s"timeout: $timeout, linger: $linger"
}
````

That’s nice, but you can make this class even better by supplying default values for the `timeout` and `linger` parameters:

````
class Socket(var timeout: Int = 2000, var linger: Int = 3000) {
    override fun toString(): String = "timeout: ${timeout}, linger: ${linger}"
}
````

By supplying default values for the parameters, you can now create a new `Socket` in a variety of different ways:

````
Socket()
Socket(1000)
Socket(4000, 6000)
````

This is what those examples look like in the REPL:

````
>>> Socket()
timeout: 2000, linger: 3000

>>> Socket(1000)
timeout: 1000, linger: 3000

>>> Socket(4000, 6000)
timeout: 4000, linger: 6000
````

As those examples shows:

- When all parameters have default values, you don’t have to provide any values when creating a new instance
- If you supply one value, it’s used for the first named parameter
- You can override the default values with your own values

An important implication of this is that default values have the effect of letting consumers consumers create instances of your class in a variety of ways — in a sense they work just as though you had created multiple, different constructors for your class.


### When you don’t provide defaults for all parameters

As a word of caution, it generally doesn’t make any sense to provide a default value for an early parameter without providing a default for subsequent parameters. 

````
// don't do this
class Socket(var timeout: Int = 5000, var linger: Int) {
    override fun toString(): String = "timeout: ${timeout}, linger: ${linger}"
}
````

If you do that, you’ll get errors when trying to construct an instance with zero or one parameters:

````
>>> val s = Socket()
error: no value passed for parameter 'linger'
val s = Socket()
               ^

>>> val s = Socket(2)
error: no value passed for parameter 'linger'
val s = Socket(2)
                ^
````

If you’re not going to provide default values for all parameters, you should only provide default values for the last parameters in the constructor:

````
// this is a little better
class Socket(var timeout: Int, var linger: Int = 5000) {
    override fun toString(): String = "timeout: ${timeout}, linger: ${linger}"
}
````

With this approach the zero-argument constructor still fails, but you can use the one-argument constructor:

````
>>> val s = Socket()
error: no value passed for parameter 'timeout'
val s = Socket()
               ^

>>> val s = Socket(10)
>>> s
timeout: 10, linger: 5000
````



## Named arguments

You can use named arguments when creating new class instances. For example, given this class:

````
class Socket(var timeout: Int, var linger: Int) {
    override fun toString(): String = "timeout: ${timeout}, linger: ${linger}"
}
````

you can create a new `Socket` like this:

````
val s = Socket(timeout=2000, linger=3000)
````

I don’t use this feature too often, but it comes in handy in certain situations, such as when all of the class constructor parameters have the same type (such as `Int` in this example). For example, some people find that this code:

````
val s = new Socket(timeout=2000, linger=3000)
````

is more readable than this code:

````
val s = new Socket(2000, 3000)
````








