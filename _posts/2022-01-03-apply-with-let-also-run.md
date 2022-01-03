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
블록에 객체 자신이 리시버 객체로 전달되고 이 객체가 반환    
```kotlin
// fun <T> T.apply(block: T.() -> Unit): T
val result = car?.apply {
    car.setColor(Color.RED)
    car.setPrice(1000)
}
```
2. also() 함수    
블록에 자기 자신을 인수로 전달되고 이 객체가 반환
```kotlin
// fun <T> T.also(block: (T) -> Unit): T
val numbers = mutableListOf("one", "two", "three")
numbers
    .also { println("The list elements before adding new one: $it") }
    .add("four")
```
3. let() 함수    
블록에 자기 자신을 인수로 전달하고 수행된 결과를 반환    
```kotlin
// fun <T, R> T.let(block: (T) -> R): R
val result = str?.let { // Int
    Integer.parseInt(it)
}
```
4. with() 함수    
인수로 객체를 받고 블록에 리시버 객체로 전달하고 수행된 결과를 반환    
```kotlin
// fun <T, R> with(receiver: T, block T.() -> R): R
with(str) {
    println(toUpperCase())
}
```
5. run() 함수    
익명 함수처럼 사용할 때는 블록의 결과를 반환    
```kotlin
// fun <R> run(block: () -> R): R
val avg = run {
    val korean = 100
    val english = 80
    val math = 50

    (korean + english + math) / 3.0
}
```    
객체를 블록의 리시버 객체로 전달하고 블록의 결과를 반환    
```kotlin
// fun <T, R> T.run(block: T.() -> R): R
str?.run {
    println(toUpperCase())
}
```