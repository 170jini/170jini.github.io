---
layout: post
title: 코틀린 데이터 클래스
description: 코틀린 데이터 클래스
summary: 코틀린 데이터 클래스
tags: 
minute: 1
---
1. 간단한 로직을 포함 하려면
부 생성자나 init 블록을 넣어 데이터를 위한 간단한 로직을 포함할 수 있다.    
```kotlin
// 1 Thread클래스를 상속받아 구현하기
data class Customer(var name: String, var email: String) {
    var job: String = "Unknown"
    constructor(name: String, email: String, _job: String): this(name, email) {
        job = _job
    }
    init {
        // 간단한 로직은 여기에
    }
}
```
2. equals( )와 hashCode( ) 예    
```kotlin
// 1 Thread클래스를 상속받아 구현하기
val cus1 = Customer("Sean", "sean@mail.com")
val cus2 = Customer("Sean", "sean@mail.com")
...
println(cus1 == cus2) // 동등성 비교 true
println(cus1.equals(cus2)) // 위와 동일 true
println("${cus1.hashCode()}, ${cus2.hashCode()}") // 고유값도 동일
```