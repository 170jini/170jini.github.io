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
3. copy( )의 사용 예    
```kotlin
val cus3 = cus1.copy(name = "Alice") // name만 변경하고자 할 때
println(cus1.toString())
println(cus3.toString())
```
4. 객체가 가지고 있는 프로퍼티를 개별 변수들로 분해    
```kotlin
val (name, email) = cus1
println("name = $name, email = $email")
```
5. 특정 프로퍼티를 가져올 필요 없는 경우    
```kotlin
val (_, email) = cus1 // 첫 번째 프로퍼티 제외
```
6. componentN() 메서드 이용    
```kotlin
val name2 = cus1.component1()
val email2 = cus1.component2()
println("name = $name2, email = $email2")
```
7. 객체 데이터가 많은 경우 for문의 활용    
```kotlin
val cus1 = Customer("Sean", "sean@mail.com")
val cus2 = Customer("Sean", "sean@mail.com")
val bob = Customer("Bob", "bob@mail.com")
val erica = Customer("Erica", "erica@mail.com")
val customers = listOf(cus1, cus2, bob, erica) // 모든 객체를 컬렉션 List 목록으로 구성
...
for((name, email) in customers) { // 반복문을 이용해 모든 객체의 프로퍼티 분해
    println("name = $name, email = $email")
}
```
8. 함수로부터 객체가 반환될 경우    
```kotlin
fun myFunc(): Customer {
    return Customer("Mickey", "mic@abc.com")
}
...
val (myName, myEmail) = myFunc()
```
9. 람다식에서 사용하는 경우    
```kotlin
// 람다식 함수로 Destructuring 된 변수 출력해 보기
val myLamda = {
    (nameLa, emailLa): Customer ->
    println(nameLa)
    println(emailLa)
}
myLamda(cus1)
```