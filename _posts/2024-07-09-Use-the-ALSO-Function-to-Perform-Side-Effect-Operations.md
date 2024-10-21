---
layout: post
title: "Kotlin Tip #20: Use the ALSO Function to Perform Side Effect Operations— 100 Kotlin Tips in 100 Days"
description: "Kotlin Tip #20: Use the ALSO Function to Perform Side Effect Operations— 100 Kotlin Tips in 100 Days"
summary: "Kotlin Tip #20: Use the ALSO Function to Perform Side Effect Operations— 100 Kotlin Tips in 100 Days"
tags: 
minute: 1
---
[Reference](https://medium.com/kotlin-with-raphael-de-lio/kotlin-tip-20-use-the-also-function-to-perform-side-effects-100-kotlin-tips-in-100-days-a2a2eaf1256a)    

Today, we will talk about the last of the five Kotlin scope functions, the ALSO function.    

The ALSO is particularly useful for executing operations that should not interfere with the main object’s state or for adding logging and other side effects.    

```kotlin
class File {
    var name: String = ""
    var extension: String = ""
    var content: String = ""

    fun save() {
        println("Saving file $name.$extension with content: $content")
    }
}

fun main() {
    val report = File().apply {
        name = "Report"
        extension = "txt"
        content = "This is the content of the report."
    }.also {
        println("Preparing to save file: ${it.name}.${it.extension}")
        it.save()
    }
}
```

In this example, also is used to log the details of the File object and then save it right after its initialization with apply. The use of it within the also block refers to the File object, allowing direct access to its properties. The beauty of also lies in its simplicity and power to maintain code readability while offering the flexibility to add meaningful side operations.    

Furthermore, also’s ability to return the original object makes it a perfect tool for chaining multiple operations, where each operation is separate, and keeping the core business logic clean and independent.    

Regardless of the side-operation you're performing, the also function exemplifies Kotlin’s commitment to concise, readable, and expressive code.