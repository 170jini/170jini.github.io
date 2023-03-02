---
layout: post
title: 코틀린 중첩과 이너 클래스
description: 코틀린 중첩과 이너 클래스
summary: 코틀린 중첩과 이너 클래스
tags: 
minute: 1
---
1. 중첩 클래스 사용하기 - NestedClassTest.kt
```kotlin
// 1 Thread클래스를 상속받아 구현하기
class Outer {
    val ov = 5
    class Nested {
        val nv = 10
        fun greeting() = "[Nested] Hello ! $nv" // 외부의 ov에는 접근 불가
    }
    fun outside() {
        val msg = Nested().greeting() // Outer 객체 생성 없이 중첩 클래스의 메서드 접근
        println("[Outer]: $msg, ${Nested().nv}") // 중첩 클래스의 프로퍼티 접근
    }
}
fun main() {
    // static 처럼 Outer의 객체 생성 없이 Nested객체를 생성 사용할 수 있음
    val output = Outer.Nested().greeting()
    println(output)
}
```
2. 코틀린 중첩 클래스에서 바깥 클래스 접근    
```kotlin
// 1 Thread클래스를 상속받아 구현하기
class Outer {
    class Nested {
        ...
        fun accessOuter() { // 컴패니언 객체는 접근할 수 있음
            println(country)
            getSomething()
        }
    }
    companion object { // 컴패니언 객체는 static처럼 접근 가능
        const val country = "Korea"
        fun getSomething() = println("Get something...")
    }
}
```
3. 이너 클래스의 바깥 클래스의 멤버 접근    
```kotlin
class Smartphone(val model: String) {
    private val cpu = "Exynos"
    inner class ExternalStorage(val size: Int) {
        fun getInfo() = "${model}: Installed on $cpu with ${size}Gb" // 바깥 클래스의 프로퍼티 접근
    }
}
fun main() {
    val mySdcard = Smartphone("S7").ExternalStorage(32)
    println(mySdcard.getInfo())
}
```