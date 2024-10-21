---
layout: post
title: "Kotlin Tip #16: Use the LET Scope Function to Transform Objects and Return the Result — 100 Kotlin Tips in 100 Days"
description: "Kotlin Tip #16: Use the LET Scope Function to Transform Objects and Return the Result — 100 Kotlin Tips in 100 Days"
summary: "Kotlin Tip #16: Use the LET Scope Function to Transform Objects and Return the Result — 100 Kotlin Tips in 100 Days"
tags: 
minute: 1
---
[Reference](https://medium.com/kotlin-with-raphael-de-lio/kotlin-tip-16-use-the-let-scope-function-to-transform-objects-and-return-the-result-100-kotlin-df729a77c6ab)    

The following five tips will be about Kotlin Scope Functions. There are five of them: let, run, with, apply, and also. And they all have one thing in common: they are called on objects and then, within the scope of those functions, you can access the object itself without its name. This might sound a bit abstract now, but don’t worry, we’ll go through each one in detail.    

The first tip is about the let scope function. It is particularly useful when you want to perform transformations on an object and assign the result:    
```kotlin
fun main() {
    val name = "   Kotlin  "
    val cleanName = name.let { 
      val trimmed = it.trim()
      val reversed = trimmed.reversed() 
      reversed
    }
    println(cleanName) // This will print "niltoK"
}
```

The operations within the let block are localized to that block and do not affect the object that invoked it. In the example above, you can see how the operations on name didn’t affect the variable itself. Instead, we stored the result of the transformations in the cleanName variable.    

The let function can also be used to make sure you only execute a block of code if the variable that is invoking it is not null:    
```kotlin
fun main() {
    val name: String? = "Kotlin"
    name?.let {
        println("The name has ${it.length} characters.")
    }
}
```

However, even though this is a common use case, it has been spread that this is the actual purpose of let. When In fact, the term let is derived from mathematical logic and set theory, where it's used to introduce a new variable or constant.    

For example, in mathematics, you might say "let a be such that x²=a" which introduces a as a new variable and defines a condition for it.    

```kotlin
fun main() {
    val x = 3

    // Let a be such that x²=a
    val a = x.let { x ->
        x * x
    }

    println(a)
}
```

Essentially, the let function in Kotlin is saying "let this variable be equal to this value."    

Also, it allows you to define a variable for a certain scope without polluting the outer scope, making your code safer and more predictable.