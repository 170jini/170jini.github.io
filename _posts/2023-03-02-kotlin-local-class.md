---
layout: post
title: 코틀린 로컬과 익명 클래스
description: 코틀린 로컬과 익명 클래스
summary: 코틀린 로컬과 익명 클래스
tags: 
minute: 1
---
1. 메서드에 지역 클래스 추가해보기 - InnerClassTest.kt    
```kotlin
class Smartphone(val model: String) {
    private val cpu = "Exynos"
    fun powerOn(): String {
        class Led(val color: String) { // 지역 클래스 선언
            fun blink(): String = "Blinking $color on $model" // 외부의 프로퍼티는 접근 가능
        }
        val powerStatus = Led("Red") // 여기에서 지역 클래스가 사용됨
        return powerStatus.blink()
    } // powerOn() 블록 끝
}
fun main() {
    ...
    val myphone = Smartphone("Note9")
    println(myphone.powerOn())
}
```
2. 익명 객체를 위한 인터페이스 추가 - InnerClassTest.kt    
```kotlin
interface Switcher { // 1 인터페이스의 선언
    fun on(): String
}
class Smartphone(val model: String) {
    private val cpu = "Exynos"
    fun powerOn(): String {
        class Led(val color: String) { // 지역 클래스 선언
            fun blink(): String = "Blinking $color on $model" // 외부의 프로퍼티는 접근 가능
        }
        val powerStatus = Led("Red") // 여기에서 지역 클래스가 사용됨
        val powerSwitch = object : Switcher { // 2 익명 객체를 사용해 Switcher의 on()을 구현
            override fun on(): String {
                return powerStatus.blink()
            }
        } // 익명(object) 객체 블록의 끝
        return powerSwitch.on()
    } // powerOn() 블록 끝
}
fun main() {
    ...
    val myphone = Smartphone("Note9")
    println(myphone.powerOn())
}
```