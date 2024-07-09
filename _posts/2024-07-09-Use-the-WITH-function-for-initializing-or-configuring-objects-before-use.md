---
layout: post
title: "Kotlin Tip #17: Use the WITH function for initializing or configuring objects before use — 100 Kotlin Tips in 100 Days"
description: "Kotlin Tip #17: Use the WITH function for initializing or configuring objects before use — 100 Kotlin Tips in 100 Days"
summary: "Kotlin Tip #17: Use the WITH function for initializing or configuring objects before use — 100 Kotlin Tips in 100 Days"
tags: 
minute: 1
---
[Reference](https://medium.com/kotlin-with-raphael-de-lio/kotlin-tip-17-use-the-with-function-for-initializing-objects-or-configuring-objects-before-use-abb3f2a5cb83)    

In our previous tip, we introduced Kotlin's five scope functions. Today, we will talk about the second one: the with function.    

Consider the scenario where you’re setting up a new object with multiple properties. Traditionally, you might find yourself repeatedly referencing the object to configure its fields:    
```kotlin
fun main() {
    val stringBuilder = StringBuilder()
    stringBuilder.append("Hello, ")
    stringBuilder.append("world!")
    stringBuilder.append(" How ")
    stringBuilder.append("are ")
    stringBuilder.append("you?")

    println(stringBuilder.toString())
}
```

By utilizing with, you transform what could have been verbose and repetitive code into a clear and succinct block:    
```kotlin
fun main() {
    val stringBuilder = StringBuilder()

    with(stringBuilder) {
        append("Hello, ")
        append("world!")
        append(" How ")
        append("are ")
        append("you?")
    }

    println(stringBuilder.toString())
}
```

The with function takes two parameters: the object you're working with and a lambda containing the actions to be performed on that object. Inside this lambda, you can access the object's members directly, without needing to prefix them with the object's name or a reference. This not only cuts down on verbosity but also on the potential for errors in referencing the object.