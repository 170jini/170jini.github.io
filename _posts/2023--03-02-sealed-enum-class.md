---
layout: post
title: 코틀린 실드와 열거형 클래스
description: 코틀린 실드와 열거형 클래스
summary: 코틀린 실드와 열거형 클래스
tags: 
minute: 1
---
1. 실드 클래스 작성하기 - SealedClassTest.kt    
```kotlin
// 실드 클래스 선언 방법 첫번째 스타일
sealed class Result {
    open class Success(val message: String): Result()
    class Error(val code: Int, val message: String): Result()
}
class Status: Result() // 실드 클래스 상속은 같은 파일에서만 가능
class Inside: Result.Success("Status") // 내부 클래스 상속
```
```kotlin
// 실드 클래스 선언 방법 두 번째 스타일
sealed class Result
open class Success(val message: String): Result()
class Error(val code: Int, val message: String): Result()
class Status: Result()
class Inside: Success("Status")
```
```kotlin
fun main() {
    // Success에 대한 객체 생성
    val result = Result.Success("Good!")
    val msg = eval(result)
    println(msg)
}
// 상태를 검사하기 위한 함수
fun eval(result: Result): String = when(result) {
    is Status -> "in progress"
    is Result.Success -> result.message
    is Result.Error -> result.message
    // 모든 조건을 가지므로 else가 필요 없음
}
```
2. 열거형 클래스의 예    
```kotlin
enum class Direction {
    NORTH, SOUTH, WEST, EAST
}
enum class DayOfWeek(val num: Int) {
    MONDAY(1), TUESDAY(2), WEDNESDAY(3), THURSDAY(4),
    FRIDAY(5), SATURDAY(6), SUNDAY(7)
}
val day = DayOfWeek.SATURDAY // SATURDAY의 값을 읽기
when(day.num) {
    1, 2, 3, 4, 5 -> println("Weekday")
    6, 7 -> println("Weekend!")
}
```
```kotlin
enum class Color(val r: Int, val g: Int, val b: Int) {
    RED(255, 0, 0), ORANGE(255, 165, 0),
    YELLOW(255, 255, 0), GREEN(0, 255, 0), BLUE(0, 0, 255),
    INDIGO(75, 0, 130), VIOLET(238, 130, 238); // 여기에 세미콜론으로 끝을 알리고
    fun rgb() = (r * 256 + g) * 256 + b // 메서드를 포함할 수 있음
}
fun main(args: Array) {
    println(Color.BLUE.rgb())
}
```
3. 인터페이스를 통한 enum 클래스의 구현    
```kotlin
interface Score {
    fun getScore(): Int
}
enum class MemberType(var prio: String) : Score {
    NORMAL("Thrid") {
        override fun getScore(): Int = 100 // 구현된 메소드
    },
    SILVER("Second") {
        override fun getScore(): Int = 500
    },
    GOLD("First") {
        override fun getScore(): Int = 1500
    }
}
fun main() {
    println(MemberType.NORMAL.getScore())
    println(MemberType.GOLD)
    println(MemberType.valueOf("SILVER"))
    println(MemberType.SILVER.prio)
    for (grade in MemberType.values()) { // 모든 값을 가져오기 위한 반복문
        println("grade.name = ${grade.name}, prio = ${grade.prio}")
    }
}
```
