Kotlin Quick Reference
======================

This file is intended for anyone interested in contributing to the [Kotlin Quick Reference](http://kotlin-quick-reference.com/) book.

The purpose of this book is to provide a very brief (ultra-brief!) introduction to [the Kotlin programming language](https://kotlinlang.org/). The idea is to show Kotlin syntax and examples with as few words as possible so that experienced developers who are new to Kotlin can find what they need quickly.

If it helps to have a model in mind, this book is something like a large cheat sheet, and it’s similar in purpose to the book, [Scala for the Impatient](https://amzn.to/2RXkRmV).



## Target audience

The target audience for this book is someone who already knows languages like Java and Scala and just needs a very quick reference of Kotlin’s syntax and some examples so they can be productive. For instance, I assume the reader already knows what classes are and what they’re good for; I make no attempt to discuss OOP theory. It’s more like, “Here’s Kotlin’s syntax to create classes, constructors, secondary constructors, and methods, and here are a few examples.” In regards to Android development, I assume the reader has already developed Android applications with Java, and just needs to see what’s different with Android/Kotlin.

Because of that target audience, this book is *not* intended for someone who needs a lot of explanation. If someone needs an “Introduction to Kotlin” book, [Kotlin in Action](https://amzn.to/2DJtTAW) is a good book for that audience.

On a personal note, I’m creating this for myself. What happens to me is that I often work with a technology like Kotlin for a while, then have to get away from it for a while, and a resource like this is helpful for when I start working with it again. Common needs for me are/were:

- I need to see nullability examples
- I need to see collections examples (List, Array, Map, etc.)
- What can I do with Kotlin interfaces?
- How do I pass a function to a function?
- How do secondary constructors work?
- How does object equality work?
- Generic types
- More ...



## Contributing

If you’re interested in contributing to this book, please read the notes that follow about writing styles, coding standards, examples, and building the book and website.

To find areas where you can contribute:

- Search the *Chapters* directory for `TODO` tags (i.e., `grep TODO *.md`)
- Look at the [open issues](https://github.com/alvinj/KotlinQuickReference/issues) for this project on Github



## Writing

The writing style for this book should be very terse, “minimalist” if you prefer. I usually start by writing a few source code examples, and then put as few words around it as necessary. Again, the target audience is an experienced developer who just needs to see the syntax and examples.

In regards to the Markdown files:

- Most lessons should begin with a `##` section titled, “Key points”
- I put three blank lines before each `##` header

In regards to writing:

- Remember that this content will be published as a website and ebooks; don’t write things like “Earlier on this page” or anything else that implies a web format
- Don’t copy source code or verbiage from other sources; see the next section for coding examples that I typically use

Some of the current lessons are a little too verbose, especially the early ones. For examples of my preferred minimalist writing style for this book, see these lessons:

- Data classes
- Open and final classes
- Getter/setter properties
- `when` expressions 



# Good examples to use in a book

If you need ideas for source code examples, I find that these are examples that all programmers can relate to and understand:

- Anything related to:
    - Pizza and a pizza store
        - Pizza, toppings, order, employees
    - Star Trek
    - Beer, brewery
    - Books, bookstore
    - Stocks, stock market
    - Social networking (people, friends, post/tweet, comments, likes)
- `Person`, `Employee`
- Math things (Pi, Fibonacci, Checksum)
- Networking, REST, and JSON processing, for example, Twitter/Facebook/Github clients
- Concepts like a To-Do List or a Blog (writing your own blogging app)



## Code standards

My coding standards in this book are:

- Indent lines with four spaces
- Curly braces look like this:

````
interface TailWagger {
    // concrete implementations
    fun startTail() { println("tail is wagging") }
    fun stopTail() { println("tail is stopped") }
}

if (test1) {
    doX()
} else if (test2) {
    doY()
} else {
    doZ()
}
````

- Functions declared like this:

````
// single-expression syntax
fun plus1(i: Int) = i + 1
fun plus1(i: Int): Int = i + 1

// multiline syntax
fun plus1(i: Int): Int {
    return i + 1
}
````

- Class declared on one line or multiple lines:

````
class Person (var firstName: String, var lastName: String)

class Person (
    var firstName: String, 
    var lastName: String
)
````



## Build notes

I use the [Gitbook command line tool](https://toolchain.gitbook.com/) to build the book.

A few notes about building different versions of the book:

- I use the script *_StartServer.sh* to run the Gitbook server on my system so I can see the book in its HTML/web format while I’m working
- The PDF is built with this command: `gitbook pdf ./ Kotlin-Quick-Reference.pdf` (there’s a script named *_CreatePdf.sh* for that)
- The PDF uses the file named cover.jpg as the book cover
    - Preferred size: 1800x2360
    - 200x262 for cover_small.jpg
    - see: https://toolchain.gitbook.com/ebook.html
- `ebook-convert` is required to generate all ebooks (pdf, mobi, epub)
- You need to run `gitbook install` in the MD files directory to install the “localized-footer” plugin (or remove or comment-out the *book.json* file on your system); I use that plugin to put a footer on the [kotlin-quick-reference.com](http://kotlin-quick-reference.com) website

Per [the Gitbook website](https://toolchain.gitbook.com/ebook.html), here are the commands for building different ebook versions:

````
// Generate a PDF file
$ gitbook pdf ./ ./KotlinQuickReference.pdf

// Generate an ePub file
$ gitbook epub ./ ./KotlinQuickReference.epub

// Generate a Mobi file
$ gitbook mobi ./ ./KotlinQuickReference.mobi
````

See that web page for more details.



## Why the lessons are numbered

My writing tools are pretty primitive, I just use TextMate or SublimeText when writing. Therefore, I started numbering the lessons so I could keep them in order in the “list of files” view in those editors. If there’s a better way to keep files in order while writing I’m open to suggestions. (I used to use a Mac app named Scrivener that keeps chapters/lessons in order, but I didn’t care for its text editor, and it’s also a paid tool.)

>Note: Free tools like the [Gitbook Editor](https://legacy.gitbook.com/editor) may be better for this purpose, but it fails to install on my Mac.



## To-Do items

The To-Do List for this project is currently in a file named TODO.txt. I’ll eventually move it into a list off Github “issues.”








