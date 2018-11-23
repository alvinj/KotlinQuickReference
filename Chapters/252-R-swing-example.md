---
description: In this lesson I show how Kotlin works with Java Swing classes, like JFrame, JTextArea, etc.
---

<!-- 
    TODO create a Github repo
-->


# Kotlin and Swing

Kotlin works with Java Swing classes like `JFrame`, `JTextArea`, etc., very easily. Here’s an example of a Kotlin application that opens a `JFrame`, adds a few components to it, and then displays it:

````
import java.awt.BorderLayout
import java.awt.Dimension
import javax.swing.JFrame
import javax.swing.JScrollPane
import javax.swing.JTextArea

fun main(args: Array<String>) {

    val textArea = JTextArea()
    textArea.setText("Hello, Kotlin/Swing world")
    val scrollPane = JScrollPane(textArea)

    val frame = JFrame("Hello, Kotlin/Swing")
    frame.getContentPane().add(scrollPane, BorderLayout.CENTER)
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)
    frame.setSize(Dimension(600, 400))
    frame.setLocationRelativeTo(null)
    frame.setVisible(true)

}
````

To see how that code works, save it to a file named *KotlinSwing.kt*, then compile it:

````
$ kotlinc KotlinSwing.kt -include-runtime -d KotlinSwing.jar
````

then execute the jar file with this `java` command:

````
$ java -jar KotlinSwing.jar
````






