---
layout: post
title: 코틀린 코루틴
description: 코틀린 코루틴
summary: 코틀린 코루틴
tags: 
minute: 1
---
1. 기본적인 launch 빌더의 사용 - BasicCoroutines.kt    
```kotlin
fun main() { // 메인스레드의 문맥
    GlobalScope.launch { // 새로운 코루틴을 백그라운드에 실행
        delay(1000L) // 1초의 넌블로킹 지연 (시간의 기본 단위는 ms)
        println("World!") // 지연 후 출력
    }
    println("Hello,") // main 스레드가 코루틴이 지연되는 동안 계속 실행
    Thread.sleep(2000L) // main 스레드가 JVM에서 바로 종료되지 않게 2초 기다림
}
```
2. 코루틴의 순차적 실행 - LaunchSuspend.kt    
```kotlin
suspend fun doWork1(): String {
    delay(1000)
    return "Work1"
}
suspend fun doWork2(): String {
    delay(3000)
    return "Work2"
}
private fun worksInSerial() {
    // 순차적 실행
    GlobalScope.launch {
        val one = doWork1()
        val two = doWork2()
        println("Kotlin One : $one")
        println("Kotlin Two : $two")
    }
}
fun main() {
    worksInSerial()
    readLine() // main()이 먼저 종료되는 것을 방지하기 위해 콘솔에서 엔터키 입력 대기
}
```
3. Job 객체의 반환 - CoroutinesReturn.kt    
``kotlin
import kotlinx.coroutines.*
fun main() {
    val job = GlobalScope.launch { // Job 객체의 반환
        delay(1000L)
        println("World!")
    }
    println("Hello,")
    println("job.isActive: ${job.isActive}, completed: ${job.isCompleted}")
    Thread.sleep(2000L)
    println("job.isActive: ${job.isActive}, completed: ${job.isCompleted}")
}
```