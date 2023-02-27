---
layout: post
title: 코틀린 쓰레드
description: 코틀린 쓰레드
summary: 코틀린 쓰레드
tags: 
minute: 1
---
1. 스레드 생성 - Thread 클래스를 상속받거나 Runnable 인터페이스를 구현    
```kotlin
// 1 Thread클래스를 상속받아 구현하기
class SimpleThread: Thread() {
    override fun run() {
        println("Current Threads: ${Thread.currentThread()}")
    }
}
// 2 Runnable 인터페이스로부터 run() 구현하기
class SimpleRunnable: Runnable {
    override fun run() {
        println("Current Threads: ${Thread.currentThread()}")
    }
}
fun main(args: Array<String>) {
    val thread = SimpleThread()
    thread.start()
    val runnable = SimpleRunnable()
    val thread1 = Thread(runnable)
    thread1.start()
}
```
2. 익명 객체를 사용하면 클래스의 객체를 만들지 않고도 다음과 같이 실행    
```kotlin
object : Thread() {
    override fun run() {
        println("Current Threads(object): ${Thread.currentThread()}")
    }
}.start()
```
3. ThreadCustomFunc.kt    
```kotlin
// 람다식 추가 함수를 만들어 실행
public fun thread(start: Boolean = true, isDaemon: Boolean = false,
    contextClassLoader: ClassLoader? = null, name: String? = null,
    priority: Int = -1, block: () -> Unit): Thread {
    val thread = object : Thread() {
        public override fun run() {
            block()
        }
    }
    if (isDaemon) // 백그라운드 실행 여부
        thread.isDaemon = true
    if (priority > 0) // 우선 순위 (1: 낮음 ~ 5: 보통 ~ 10: 높음)
        thread.priority = priority
    if (name != null) // 이름
        thread.name = name
    if (contextClassLoader != null)
        thread.contextClassLoader = contextClassLoader
    if (start)
        thread.start()
    return thread
}
fun main() {
    // 스레드의 옵션 변수를 손쉽게 설정할 수 있다.
    thread(start = true) {
        println("Current Threads(Custom function): ${Thread.currentThread()}")
        println("Priority: ${Thread.currentThread().priority}") // 기본값은 5
        println("Name: ${Thread.currentThread().name}")
        println("Name: ${Thread.currentThread().isDaemon}")
    }
}
```
```
Current Threads(Custom function): Thread[Thread-0,5,main]
Priority: 5
Name: Thread-0
Name: false
```
4. newFixedThreadPool()    
자주 재사용되는 스레드를 이용하기 위해 미리 생성된 스레드풀에서 스레드 이용    
예) 8개의 스레드로 특정 백그라운드 서비스를 하도록 만든다고 했을 때    
```kotlin
val myService:ExecutorService = Executors.newFixedThreadPool(8)
var i = 0
while (i < items.size) { // 아주 큰 데이터를 처리할 때
    val item = items[i]
    myService.submit {
        processItem(item) // 여기서 아주 긴 시간 동안 처리 하는 경우
    }
}
```