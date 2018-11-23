# Kotlin Cheat Sheet

<!--
    - didn't cover file i/o
    - didn't cover i++
 -->

## Overview

Kotlin:

- is a high-level language
- is statically typed
- is concise
- supports the object-oriented programming paradigm
- supports the functional programming paradigm
- supports a sophisticated type inference system
- has traits, which are a combination of interfaces and abstract classes, and can be used as mixins, and support a modular programming style
- has an Actors API, which is based on the Actors concurrency model built into Erlang



## Kotlin idioms

- prefer `val` over `var`
- use `Option` or `Try` instead of `null` or exceptions
- every line of code should be an expression (Expression Oriented Programming (EOP))



## Two types of variables

- `val` is an immutable variable, and should be preferred
- `var` creates a mutable variable, and should only be used when there is a specific reason to use it
- examples:

````
val x = 1   //immutable
var y = 0   //mutable
````


## Implicit and explicit variable creation

Create variables without declaring their type (an implicit style):

````
val x = 1
val s = "a string"
val p = new Person("Regina")
````

Much less often you can also explicitly declare their type:

````
val x: Int = 1
val s: String = "a string"
val p: Person = new Person("Regina")
````


## The if/else control structure

if/else:

````
if (a == b) doSomething()

if (a == b) doSomething() else doSomethingElse()

if (a == b) {
    doSomething()
} else {
    doSomethingElse()
}
````

`else if`:

````
if (test1) {
    doX()
} else if (test2) {
    doY()
} else if (test3) {
    doY()
} else {
    doZ()
}
````



## The `when` control structure

Using `when` like a `switch` statement, and assigning the result to a variable:

````
val dayOfWeek = when (i) {
    1 -> "Sunday"
    2 -> "Monday"
    3 -> "Tuesday"
    4 -> "Wednesday"
    5 -> "Thursday"
    6 -> "Friday"
    7 -> "Saturday"
    else -> "invalid day"
}

println(dayOfWeek)
````

Multiple branch conditions:

````
when (i) {
    1,2,3 -> println("got a 1, 2, or 3")
    4,5,6 -> println("got a 4, 5, or 6")
    else -> println("something else")
}
````


Using `match` as the body of a method, and matching multiple different types:

````
def getClassAsString(x: Any):String = x match {
  case s: String => s + " is a String"
  case i: Int => "Int"
  case f: Float => "Float"
  case l: List[_] => "List"
  case p: Person => "Person"
  case _ => "Unknown"
}
````



## The try/catch control structure

How to catch multiple exceptions:

````
try {
    doSomething()
} catch {
    case fnfe: FileNotFoundException => println(fnfe)
    case ioe: IOException => println(ioe)
}
````

TODO: SHOW `FINALLY`



## Loops (for, foreach, while)

`for` loops:

````
for (arg <- args) println(arg)

// "x to y" syntax
for (i <- 0 to 5) println(i)

// "x to y by" syntax
for (i <- 0 to 10 by 2) println(i)

// yield
for (i <- 1 to 5) yield i * 2

// yield (multiple lines)
val lengths = for (e <- names) yield {
    // imagine that this required multiple lines of code
    e.length
}
````

A `foreach` method is available on most collections classes:

````
// function literal - body is "println(arg)"
args.foreach(arg => println(arg))

// shorter
args.foreach(println(_))

// even shorter - if function literal consists of one
// statement that takes a single argument, you can do this:
args.foreach(println)
````

`while` loops:

````
var i = 0
while (i < 3) {
    println(i)
    i += 1
}
````

See:

- https://alvinalexander.com/scala/scala-for-loop-examples-syntax-yield-foreach



## Classes

How to create a class with multiple constructor parameters:

````
class Person(var firstName: String, var lastName: String) {
    def printFullName() {
        println(s"$firstName $lastName")
    }
}
````

Create and use an instance of the `Person` class:

````
val al = new Person("Alvin", "Alexander")
al.printFullName()
````

When constructor parameters are defined as `var`, they can be mutated:

````
val p = new Person("John", "Doe")
p.firstName = "Jane"
````

Defining auxiliary constructors:

````
// primary constructor
class Pizza (var crustSize: Int, var crustType: String) {

    // one-arg auxiliary constructor
    def this(crustSize: Int) {
        this(crustSize, Pizza.DEFAULT_CRUST_TYPE)
    }

    // one-arg auxiliary constructor
    def this(crustType: String) { 
        this(Pizza.DEFAULT_CRUST_SIZE, crustType)
    }

    // zero-arg auxiliary constructor
    def this() {
        this(Pizza.DEFAULT_CRUST_SIZE, Pizza.DEFAULT_CRUST_TYPE)
    }

    override def toString = s"A $crustSize inch pizza with a $crustType crust" 
}

// companion object
object Pizza {
    val DEFAULT_CRUST_SIZE = 12
    val DEFAULT_CRUST_TYPE = "THIN"
}
````

That code lets you create new `Pizza` instances like this:

````
val p1 = new Pizza(Pizza.DEFAULT_CRUST_SIZE, Pizza.DEFAULT_CRUST_TYPE)
val p2 = new Pizza(Pizza.DEFAULT_CRUST_SIZE)
val p3 = new Pizza(Pizza.DEFAULT_CRUST_TYPE)
val p4 = new Pizza
````

How to provide default values for constructor parameters:

````
class Socket (val timeout: Int = 10000)
````



## Kotlin methods

Basic syntax:

````
def sum(a: Int, b: Int) = a + b
def sum(a: Int, b: Int): Int = a + b

def concatenate(s1: String, s2: String) = s1 + s2
def concatenate(s1: String, s2: String): String = s1 + s2
````

Default values for method parameters:

````
class Connection {
    def makeConnection(timeout: Int = 5000, protocol: = "http") {
        println("timeout = %d, protocol = %s".format(timeout, protocol))
        // more code here
    }
}

val c = new Connection
c.makeConnection()
c.makeConnection(2000)
c.makeConnection(3000, "https")
````

Using parameter names when calling a method:

````
// a regular class
class Pizza {
    var crustSize = 12
    var crustType = "Thin"
    def update(crustSize: Int, crustType: String) {
        this.crustSize = crustSize
        this.crustType = crustType
    }
    override def toString = {
        "A %d inch %s crust pizza.".format(crustSize, crustType)
    }
}

// create an instance
val p = new Pizza

p.update(crustSize = 16, crustType = "Thick")
p.update(crustType = "Pan", crustSize = 14)
````



## Collections classes

Rule: Forget what you know about Java collections classes, and use the Kotlin collections classes.

To start with, use only these classes:

TODO: UPDATE Seq/Vector

- `Vector`
    - indexed, immutable
    - use `Seq`, or its underlying data type (`Vector`)
- `ArrayBuffer`
    - indexed, mutable
- `List`
    - linear, immutable
- `ListBuffer`
    - linear, mutable
- `Map`
    - like a Java `HashMap`
- `Set`
    - a sequence of unique elements
- `Queue`
    - a first-in, first-out data structure
- `Stack`
    - a last-in, first-out data structure

Choosing a sequential collection class:

   Foo  | Immutable | Mutable
------- | --------- | -------
Indexed | `Seq`     | `ArrayBuffer`
Linear  | `List`    | `ListBuffer`



## Collections methods (sequences)

There are many collections methods, which you’ll eventually see is a great benefit to you. These are the most commonly used methods:

- use `for` and `foreach` to traverse
- `map`
- `filter`
- `fold`, `reduce`

In the following examples I use this sequence:

````
val nums = Seq(1,2,3,4,5)
````

### foreach

````
nums.foreach((i: Int) => println(i))   // long form
nums.foreach(i => println(i))
nums.foreach(println(_))
nums.foreach(println)                  // short form
````

### Traversing a sequence with `for`

````
for (n <- nums) println(n)
````

````
for {
    n <- nums
    if n > 2
} println(n)
````

### for/yield

````
for (n <- nums) yield n * 2
````

````
val fruits = Seq("apple", "banana", "lime", "orange")
val upper = for (f <- fruits) yield (f.toUpperCase)
val x = for (i <- 0 until fruits.length) yield (i, fruits(i))
val x = for (f <- fruits) yield (f, f.length)
val x = for {
    f <- fruits
    if f.length > 4
} yield (f, f.length)
````


### map

````
val numsDoubled = nums.map(i => i * 2)
val numsDoubled = nums.map(_ * 2)

val helpers = Vector("adam", "kim", "melissa")
val caps = helpers.map(e => e.capitalize)
val caps = helpers.map(_.capitalize)
val names = Array("Fred", "Joe", "Jonathan")
val lengths = names.map(_.length)
val nieces = List("Aleka", "Christina", "Molly")
val elems = nieces.map(niece => <li>{niece}</li>)
````


### filter

````
val lowNums = nums.filter(i => i < 4)
val lowNums = nums.filter(_ < 4)

val x = List.range(1, 10)
val evens = x.filter(_ % 2 == 0)
````

fold/reduce:

````
val a = Array(12, 6, 15, 2, 20, 9)
a.reduceLeft(_ + _)
a.reduceLeft(_ * _)
a.reduceLeft(_ min _)
a.reduceLeft(_ max _)
````

TODO: do any more?

- drop, dropWhile
- take, takeWhile
- head
- tail


### Populating lists with `Range`

````
List.range(0, 10)
Vector.range(0, 10, 2)
val list = 1 to 10 by 2 toList
val list = (1 to 10).by(2).toList
val letters = ('a' to 'f').toList
val letters = ('a' to 'f').by(2).toList
val doubles = (1 to 5).map(_ * 2.0)
val map = (1 to 5).map(e => (e,e)).toMap
````



## Collections methods (maps)

````
// immutable map
val states = Map("AL" -> "Alabama", "AK" -> "Alaska")
````

````
// mutable map
val states = collection.mutable.Map("AL" -> "Alabama", "AK" -> "Alaska")
states += ("CO" -> "Colorado")
````

Traversing and printing maps:

````
for((k,v) <- m) println(s"key: $k, value: $v")
````

````
val ratings = Map(
    "Lady in the Water"-> 3.0, 
    "Snakes on a Plane"-> 4.0, 
    "You, Me and Dupree"-> 3.5
)
for ((k,v) <- ratings) println(s"key: $k, value: $v")

ratings.foreach {
    case(movie, rating) => println(s"key: $movie, value: $rating")
}

ratings.foreach(x => println(s"key: ${x._1}, value: ${x._2}"))
````

See:

- https://alvinalexander.com/scala/how-to-traverse-map-for-loop-foreach-scala-cookbook


SortedMap:

````
import scala.collection.SortedMap

//TODO show in REPL
val grades = SortedMap(
    "Kim" -> 90,
    "Al" -> 85,
    "Melissa" -> 95,
    "Emily" -> 91,
    "Hannah" -> 92
)
````



## Traits

TODO: PUT THIS CLOSER TO CLASSES

Using a trait as an interface:

````
trait Animal {
    def speak(whatToSay: String)
}
````

Class that extends one trait:

````
class Dog extends Animal
````

Class that extends multiple traits:

````
class Dog extends Animal with WaggingTail with FourLeggedAnimal { ...
````



## When to use abstract classes

Always prefer traits over abstract classes, except when:

- You want to create a base class that requires constructor arguments
- The code will be called from Java code

Regarding the first point, this won’t compile:

````
trait Animal(name: String)   //traits can’t have parameters
````

Use this instead:

````
abstract class Animal(name: String)
````

````
coming soon ...
````



## Inheritance

````
class Bird extends Animal with Wings {
    // body here
}
````

Handling constructor parameters when extending a class:

````
class Person (var name: String, var address: Address) {
    override def toString = if (address == null) name else s"$name @ $address"
}
````

````
class Employee (name: String, address: Address, var age: Int) 
extends Person (name, address) {
    // rest of the class ...
}
````



## Packaging

Most people use the “Java” packaging style, with the `package` declaration at the top of source code files:

````
package com.alvinalexander.pizzastore.model

class Pizza ...
````

You can also use this style:

````
package com.alvinalexander.pizzastore.model {
    class Pizza ...
}
````

You can also nest packages:

````
package foo {
    package bar {
        class Bar ...
    }
    package baz {
        class Baz ...
    }
}
````



## Imports

How to import one class:

````
// import one class
import java.io.File
````

How to import multiple classes:

````
// import every class in a package
import java.io._

// import multiple classes from a package (version 1)
import java.io.{File, IOException, FileNotFoundException}

// import multiple classes from a package (version 2)
import java.io.File
import java.io.FileNotFoundException
import java.io.IOException
````

You can also put `import` statements anywhere you want them:

````
// before a method
import java.util.Date
def myMethod(d: Date): String = {
    // inside a method
    import java.text.SimpleDateFormat
    ...
}
````



## Using Java collections

Import all conversions:

TODO: use JavaConverters instead of JavaConversions

````
import scala.collection.JavaConverters._
````

Use the Java `ArrayList`:

````
import scala.collection.JavaConverters._
var list = new java.util.ArrayList[Int]()
list.add(1)
list.add(2)
val listInKotlin = list.asScala
listInKotlin.foreach(println)
````

````
coming soon ...
````

See:

- [JavaConverters docs](https://docs.scala-lang.org/overviews/collections/conversions-between-java-and-scala-collections.html)
- [JavaConverters](http://www.scala-lang.org/api/2.12.3/scala/collection/JavaConverters$.html)




## Using Java libraries

````
coming soon ...
````



## Simple Build Tool (SBT)

TODO: show the directory structure:

`````
.
|-- build.sbt
|-- lib
|-- project
|-- src
|-- |-- main
|-- |-- -- 
| |-- java
| |
| |
| |
| |-- test
| |-- java
|       |-- resources
| |-- scala
|-- java
|-- resources
|-- scala
|-- target
`````

Show a basic *build.sbt* file:

````
name := "MyKotlinSbtProject"

version := "1.0"

scalaVersion := "2.12.4"

libraryDependencies ++= Seq(
    "org.typelevel" %% "cats-core" % "1.0.0-MF"
)

scalacOptions += "-deprecation"
````

See:

- https://alvinalexander.com/scala/sbt-how-to-compile-run-package-scala-project
- https://alvinalexander.com/scala/sbt-how-pass-command-line-arguments-sbt-run
- https://alvinalexander.com/scala/sbt-how-specify-main-method-class-to-run-in-project
- https://alvinalexander.com/scala/sbt-how-to-generate-project-api-documentation
- 



## KotlinTest

- https://alvinalexander.com/scala/scalatest-tutorials-from-scala-cookbook



## Concurrency (futures)


````
import scala.concurrent.{Future}
import scala.concurrent.ExecutionContext.Implicits.global
import scala.util.{Failure, Success}
import scala.util.Random

object Example1 extends App {

    println("starting calculation ...")

    val f = Future {
        sleep(Random.nextInt(500))
        42
    }

    println("before onComplete")
    f.onComplete {
        case Success(value) => println(s"Got the callback, meaning = $value")
        case Failure(e) => e.printStackTrace
    }

    // do the rest of your work
    println("A ..."); sleep(100)
    println("B ..."); sleep(100)
    println("C ..."); sleep(100)
    println("D ..."); sleep(100)
    println("E ..."); sleep(100)
    println("F ..."); sleep(100)
    sleep(2000)
}
````

Proper way to create and use multiple Kotlin futures:

````
package futures

import scala.concurrent.Future
import scala.concurrent.ExecutionContext.Implicits.global
import scala.util.{Failure, Success}

/**
 * @author: alvin alexander, http://alvinalexander.com
 */
object MultipleFutures1 extends App {

    // (a) create the futures
    val f1 = Future { sleep(800); 1 }
    val f2 = Future { sleep(200); 2 }
    val f3 = Future { sleep(400); 3 }

    // (b) run them simultaneously in a for-comprehension
    val result = for {
        r1 <- f1
        r2 <- f2
        r3 <- f3
    } yield (r1 + r2 + r3)

    // (c) do whatever you need to do with the result
    result.onComplete {
       case Success(x) => println(s"\nresult = $x")
       case Failure(e) => e.printStackTrace
    }

    // important for a little parallel demo: keep the jvm alive
    sleep(3000)
    
    def sleep(time: Long): Unit = Thread.sleep(time)

}
````

````
coming soon ...
````

See:

- [How to use multiple Futures in a Kotlin for-comprehension](https://alvinalexander.com/scala/how-use-multiple-scala-futures-in-for-comprehension-loop)



## Command line I/O

````
// print with a newline
println("Hello, world")

// print without newline
print("Hello without newline")

// print to STDERR
System.err.println("yikes, an error happened")
````

How to use `readLine` to read input:

````
import scala.io.StdIn.readLine

object HelloYou extends App {

    print("Enter your first name: ")
    val firstName = readLine()

    print("Enter your last name: ")
    val lastName = readLine()

    println(s"Your name is $firstName $lastName")

}
````



## File I/O

### Writing to STDOUT and STDERR

````
println("Hello, world")
print("Hello without newline")
System.err.println("yikes, an error happened")
````


### Reading command-line input

`readLine` is simple:

````
print("Enter your name: ")
val name = readLine()
````

Can also use the *java.util.Scanner* class:

````
import java.util.Scanner
val scanner = Scanner(System.`in`)
print("Enter an int: ")
val i: Int = scanner.nextInt()
println("i = $i")
````


### Reading text files

Simple:

````
import java.io.File
fun readFile(filename: String): List<String> = File(filename).readLines()

val lines = readFile("/etc/passwd")

lines.forEach{ println(it) }
lines.forEach{ line -> println(line) }
````

#### Other ways to read text files

Other ways to read text files in Kotlin:

````
fun readFile(filename: String): List<String> = File(filename).readLines()
fun readFile(filename: String): List<String> = File(filename).bufferedReader().readLines()
fun readFile(filename: String): List<String> = File(filename).useLines { it.toList() }
fun readFile(filename: String): String = File(filename).inputStream().readBytes().toString(Charsets.UTF_8)
val text = File("/etc/passwd").bufferedReader().use { it.readText() }
````


### Writing text files

A simple approach:

````
File(filename).writeText(string)
File(filename).writeText(string, Charset.forName("UTF-16"))
````

#### Other ways to write files

There are other ways to write to files in Kotlin:

````
File(filename).writeBytes(byteArray)
File(filename).printWriter().use { out -> out.println(string) }
File(filename).bufferedWriter().use { out -> out.write(string) }
````




## The ubiquitous underscore character

````
coming soon ...
````



## Tuples

Tuples let you put a heterogenous collection of elements in a little container:

````
val things = (100, "Foo")
println(things._1)
println(things._2)

val d = ("Debi", 95)

case class Person(name: String)
val t = (3, "Three", new Person("Al"))
t._1
t._2
t._3

val(x, y, z) = (3, "Three", new Person("Al"))
````



## Strings (multiline, string interpolation)

````
val name = "Joe"
val age = 42
val weight = 180.5

// prints "Hello, Joe"
println(s"Hello, $name")

// prints "Joe is 42 years old, and weighs 180.5 pounds."
println(f"$name is $age years old, and weighs $weight%.1f pounds.")

// 'raw' interpolator
println(raw"foo\nbar")
````


scala> println(s"Age next year: ${age + 1}")
Age next year: 34

println(s"You are 33 years old: ${age == 33}")

scala> case class Student(name: String, score: Int)
defined class Student

scala> val hannah = Student("Hannah", 95)
hannah: Student = Student(Hannah,95)

scala> println(s"${hannah.name} has a score of ${hannah.score}")
Hannah has a score of 95

s"foo\nbar"
raw"foo\nbar"



## Shell scripts

````
#!/bin/sh
exec scala -savecompiled "$0" "$@"
!#

args.foreach(println)

// more here ...

case class Person(name: String)
````



````
#!/bin/sh
exec scala "$0" "$@"
!#

case class Person(name: String)




object HelloWorld {
  def main(args: Array[String]) {
    val al = Person("Al")
    println(al)
  }
}

HelloWorld.main(args)
````



## TODO

- TODO: add string interpolation











