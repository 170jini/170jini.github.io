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
val result = car?.apply {
    car.setColor(Color.RED)
    car.setPrice(1000)
}
```
2. also() 함수    
The context object is available as an argument (it). The return value is the object itself.    
```kotlin
val numbers = mutableListOf("one", "two", "three")
numbers
    .also { println("The list elements before adding new one: $it") }
    .add("four")
```
3. let() 함수    
The context object is available as an argument (it). The return value is the lambda result.    
```kotlin
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
class Employee {
    var firstName: String? = null
    var age: Int = 0
}
val employee: Employee? = Employee()
employee?.firstName = "Suneet"
employee?.age = 27
employee?.run {
    println(age)
}
```