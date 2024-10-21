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
```kotlin
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
4. join() 결과 기다리기    
```kotlin
fun main() = runBlocking<Unit> {
    val job = launch { // Job의 객체를 반환
        delay(1000L)
        println("World!")
    }
    println("Hello")
    job.join() // 명시적으로 코루틴이 완료되길 기다림. 취소할 경우 job.cancel()을 사용
}
```
5. 동시성 처리를 위한 async 코루틴    
```kotlin
suspend fun doWork1(): String {
    delay(1000)
    return "Work1"
}
suspend fun doWork2(): String {
    delay(3000)
    return "Work2"
}
private fun worksInParallel() : Job {
    // Deferred<T> 를 통해 결과값을 반환
    val one = GlobalScope.async {
        doWork1()
    }
    val two = GlobalScope.async {
        doWork2()
    }
    val job = GlobalScope.launch {
        val combined = one.await() + "_" + two.await()
        println("Kotlin Combined: $combined")
    }
    return job
}
fun main() = runBlocking<Unit> {
    runBlocking<Unit> {
        val time = measureTimeMillis {
            val job = worksInParallel()
            job.join()
        }
        println("Time: $time")
    }
}
```
6. 부모-자식 및 독립적인 스코프의 코루틴    
```kotlin
fun main() = runBlocking<Unit> {
    val request = launch {
        GlobalScope.launch { // 프로그램 전역으로 독립적인 수행 (부모-자식관계 없음)
            println("job1: before suspend function")
            delay(1000)
            println("job1: after suspend function") // 작업 취소에 영향을 받지 않음
        }
        launch { // 부모의 문맥을 상속 (상위 launch의 자식)
        //launch(Dispatchers.Default) { // 부모의 문맥을 상속 (상위 launch의 자식), 분리된 작업
        //CoroutineScope(Dispatchers.Default).launch { // 새로운 스코프가 구성되 request와 무관
            delay(100)
            println("job2: before suspend function")
            delay(1000)
            println("job2: after suspend function") // request(부모)가 취소되면 수행되지 않음
        }
    }
    delay(500)
    request.cancel() // 부모 코루틴의 취소
    delay(1000)
}
```
7. main()을 블로킹 모드로 동작시키기 - RunBlockingTest.kt    
```kotlin
import kotlinx.coroutines.*
fun main() = runBlocking<Unit> { // 메인 메서드가 코루틴 환경에서 실행
    launch { // 백그라운드로 코루틴 실행
        delay(1000L)
        println("World!")
    }
    println("Hello") // 즉시 이어서 실행됨
}
```
8. runBlocking()을 클래스 내의 멤버 메서드에서 사용할 때    
```kotlin
class MyTest {
    ...
    fun mySuspendMethod() = runBlocking<Unit> {
}
```
9. 특정 디스패처 옵션을 주어줄 때    
```kotlin
runBlocking(Dispatchers.IO) {
    launch {
        repeat(5) {
            println("counting ${it + 1}")
            delay(1000)
        }
    }
}
...
```
10. coroutineScope 빌더의 예    
```kotlin
import kotlinx.coroutines.*
fun main() = runBlocking { // this: CoroutineScope
    launch {
        delay(200L)
        println("Task from runBlocking")
    }
    coroutineScope { // 코루틴 스코프의 생성 -- 부모가 하위 코루틴 완료 기다림
    //CoroutineScope(Dispatchers.Default).launch {//--이때는 부모-자식 관계와 무관(완료를 기다리지 않음)
        launch {
            delay(500L)
            println("Task from nested launch")
        }
        delay(100L)
        println("Task from coroutine scope")
    }
    println("Coroutine scope is over")
}
```