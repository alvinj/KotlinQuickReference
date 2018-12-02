---
description: This page shows examples of how to use Kotlin with Android.
---


# Android

This section of the book will contain Kotlin syntax examples that can help in building Android applications.



## FloatingActionButton lambda

This code:

````
fab.setOnClickListener(object : View.OnClickListener {
    override fun onClick(view: View) {
        save("Note1.txt")
    }
})
````

can be written like this:

````
fab.setOnClickListener { save("Note1.txt") }
````


