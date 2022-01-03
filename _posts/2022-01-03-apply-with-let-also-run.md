---
layout: post
title: 코틀린의 apply, with, let, also, run
description: 코틀린의 apply, with, let, also, run
summary: 코틀린의 apply, with, let, also, run
tags: 
minute: 1
---
[Scope functions](https://kotlinlang.org/docs/scope-functions.html)    
1. apply() 함수    
The context object is available as a receiver (this). The return value is the object itself.    
```kotlin
// fun <T> T.apply(block: T.() -> Unit): T
val result = car?.apply {
    car.setColor(Color.RED)
    car.setPrice(1000)
}
```
2. also() 함수    
The context object is available as an argument (it). The return value is the object itself.    
```kotlin
// fun <T> T.also(block: (T) -> Unit): T
val numbers = mutableListOf("one", "two", "three")
numbers
    .also { println("The list elements before adding new one: $it") }
    .add("four")
```
3. let() 함수    
The context object is available as an argument (it). The return value is the lambda result.    
```kotlin
// fun <T, R> T.let(block: (T) -> R): R
val result = str?.let { // Int
    Integer.parseInt(it)
}
```
4. with() 함수    
A non-extension function: the context object is passed as an argument, but inside the lambda, it's available as a receiver (this). The return value is the lambda result.    
```kotlin
val numbers = mutableListOf("one", "two", "three")
val firstAndLast = with(numbers) {
    "The first element is ${first()}," +
    " the last element is ${last()}"
}
println(firstAndLast)
```
5. run() 함수    
The context object is available as a receiver (this). The return value is the lambda result.    
```kotlin
val service = MultiportService("https://example.kotlinlang.org", 80)

val result = service.run {
    port = 8080
    query(prepareRequest() + " to port $port")
}
```