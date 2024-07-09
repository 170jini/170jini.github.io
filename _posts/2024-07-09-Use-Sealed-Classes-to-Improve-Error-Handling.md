---
layout: post
title: "Kotlin Tip #21: Use Sealed Classes to Improve Error Handling — 100 Kotlin Tips in 100 Days"
description: "Kotlin Tip #21: Use Sealed Classes to Improve Error Handling — 100 Kotlin Tips in 100 Days"
summary: "Kotlin Tip #21: Use Sealed Classes to Improve Error Handling — 100 Kotlin Tips in 100 Days"
tags: 
minute: 1
---
[Reference](https://medium.com/kotlin-with-raphael-de-lio/kotlin-tip-21-use-sealed-classes-to-improve-error-handling-100-kotlin-tips-in-100-days-a755cefaebb4)    

Sealed classes in Kotlin stand out as an elegant solution for representing operation results, especially when dealing with external APIs or complex logic that can lead to multiple outcomes.    

Sealed classes allow developers to encapsulate different operation results in a type-safe manner. Unlike using exceptions for control flow, which can obscure the intent and make error handling cumbersome, sealed classes make the possible outcomes of an operation explicit and part of the type system. This not only improves readability but also enhances the robustness of your code by making error handling a deliberate part of your design.    

Consider the scenario where an operation can fail for several reasons, each with its own context and information. Using exceptions to signal these failures would force callers of your API to rely on try/catch blocks, which can easily lead to error-prone and hard-to-read code.    

In contrast, by using sealed classes, you can define a clear and concise hierarchy of outcomes. This hierarchy can include successful results, various kinds of failures, and even intermediate states, all as part of the same type family. This approach leverages Kotlin’s type system and when expressions, allowing you to handle all possible outcomes exhaustively and safely.    

To further illustrate the concept, let’s consider a network request operation, which is a common scenario in modern applications. Network operations can fail for a variety of reasons, such as network errors, server errors, invalid responses, or even timeouts. A sealed class hierarchy can elegantly encapsulate these outcomes:    
```kotlin
sealed class NetworkResult<out T> {
    data class Success<out T>(val data: T) : NetworkResult<T>()
    object NetworkError : NetworkResult<Nothing>()
    object ServerError : NetworkResult<Nothing>()
    data class InvalidData(val error: String) : NetworkResult<Nothing>()
    object Timeout : NetworkResult<Nothing>()
}

fun performRequest(): NetworkResult<String> {
    // Placeholder for network request logic
    return NetworkResult.NetworkError // Example outcome
}
```

This structure allows the caller to handle each specific outcome with a clear understanding of what happened, using a when expression:    
```kotlin
val result = performRequest()
when (result) {
    is NetworkResult.Success -> println("Success with data: ${result.data}")
    is NetworkResult.NetworkError -> println("Network error occurred")
    is NetworkResult.ServerError -> println("Server error occurred")
    is NetworkResult.InvalidData -> println("Invalid data: ${result.error}")
    is NetworkResult.Timeout -> println("Request timed out")
}
```

Sealed classes allow us to design APIs that are both easy to use and maintain. They promote a pattern where errors and various outcomes are first-class citizens of your API design, leading to safer, clearer, and more idiomatic Kotlin code.