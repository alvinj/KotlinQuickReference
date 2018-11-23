---
description: This page shows how to work with I/O in Kotlin, including reading and writing to files and reading/writing with the command line.
---

<!--
    TODO show I/O with binary files (bytes)
-->

# I/O With Kotlin

To get ready to show `for` loops, `if` expressions, and other Kotlin constructs, let’s take a look at how to handle I/O with Kotlin.



## Writing to STDOUT and STDERR

Write to standard out (STDOUT) using `println`:

````
println("Hello, world")          // includes newline
print("Hello without newline")   // no newline character
````

Because `println` is so commonly used, there’s no need to import it.

Writing to STDERR:

````
System.err.println("yikes, an error happened")
````



## Reading command-line input

A simple way to read command-line (console) input is with the `readLine()` function:

````
print("Enter your name: ")
val name = readLine()
````

`readLine()` provides a simple way to read input. For more complicated needs you can also use the *java.util.Scanner* class, as shown in this example:

````
import java.util.Scanner
val scanner = Scanner(System.`in`)
print("Enter an int: ")
val i: Int = scanner.nextInt()
println("i = $i")
````

Just be careful with the `Scanner` class. If you’re looking for an `Int` and the user enters something else, you’ll end up with a `InputMismatchException`:

````
>>> val i: Int = scanner.nextInt()
1.1
java.util.InputMismatchException
	at java.util.Scanner.throwFor(Scanner.java:864)
	at java.util.Scanner.next(Scanner.java:1485)
	at java.util.Scanner.nextInt(Scanner.java:2117)
	at java.util.Scanner.nextInt(Scanner.java:2076)
````

>I write more about the `Scanner` class in my article, [How to prompt users for input in Scala shell scripts](https://alvinalexander.com/scala/scala-shell-scripts-how-prompt-users-input-read).



## Reading text files

There are a number of ways to read text files in Kotlin. While this approach isn’t recommended for large text files, it’s a simple way to read small-ish text files into a `List<String>`:

````
import java.io.File
fun readFile(filename: String): List<String> = File(filename).readLines()
````

Here’s how you use that function to read the */etc/passwd* file:

````
val lines = readFile("/etc/passwd")
````

And here are two ways to print all of those lines to STDOUT:

````
lines.forEach{ println(it) }
lines.forEach{ line -> println(line) }
````

### Other ways to read text files

Here are a few other ways to read text files in Kotlin:

````
fun readFile(filename: String): List<String> = File(filename).readLines()

fun readFile(filename: String): List<String> = File(filename).bufferedReader().readLines()

fun readFile(filename: String): List<String> = File(filename).useLines { it.toList() }

fun readFile(filename: String): String = File(filename).inputStream().readBytes().toString(Charsets.UTF_8)

val text = File("/etc/passwd").bufferedReader().use { it.readText() }
````

The file-reading function signatures look like this:

````
// Do not use this function for huge files.
fun File.readLines(
    charset: Charset = Charsets.UTF_8
): List<String>

fun File.bufferedReader(
    charset: Charset = Charsets.UTF_8,
    bufferSize: Int = DEFAULT_BUFFER_SIZE
): BufferedReader

fun File.reader(
    charset: Charset = Charsets.UTF_8
): InputStreamReader

fun <T> File.useLines(
    charset: Charset = Charsets.UTF_8,
    block: (Sequence<String>) -> T
): T

// This method is not recommended on huge files. It has an internal limitation of 2 GB byte array size.
fun File.readBytes(): ByteArray

// This method is not recommended on huge files. It has an internal limitation of 2 GB file size.
fun File.readText(charset: Charset = Charsets.UTF_8): String
````

See the Kotlin [java.io.File documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/java.io.-file/index.html) for more information and caveats about the methods shown (`readLines`, `useLines`, etc.).



## Writing text files

There are several ways to write text files in Kotlin. Here’s a simple approach:

````
File(filename).writeText(string)
````

That approach default to the UTF-8 character set. You can also specify the `Charset` when using `writeText`:

````
File(filename).writeText(string, Charset.forName("UTF-16"))
````

### Other ways to write files

There are other ways to write to files in Kotlin. Here are some examples:

````
File(filename).writeBytes(byteArray)
File(filename).printWriter().use { out -> out.println(string) }
File(filename).bufferedWriter().use { out -> out.write(string) }
````

The file-writing function signatures look like this:

````
fun File.writeText(
    text: String,
    charset: Charset = Charsets.UTF_8
)

fun File.writeBytes(array: ByteArray)

fun File.printWriter(
    charset: Charset = Charsets.UTF_8
): PrintWriter

fun File.bufferedWriter(
    charset: Charset = Charsets.UTF_8,
    bufferSize: Int = DEFAULT_BUFFER_SIZE
): BufferedWriter
````

See the Kotlin [java.io.File documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/java.io.-file/index.html) for more information about the methods shown.








