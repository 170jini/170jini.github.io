---
layout: post
title: 코틀린의 apply, with, let, also, run
description: 코틀린의 apply, with, let, also, run
summary: 코틀린의 apply, with, let, also, run
tags: 
minute: 1
---
[코틀린 의 apply, with, let, also, run 은 언제 사용하는가?](https://medium.com/@limgyumin/%EC%BD%94%ED%8B%80%EB%A6%B0-%EC%9D%98-apply-with-let-also-run-%EC%9D%80-%EC%96%B8%EC%A0%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%EA%B0%80-4a517292df29)    
1. apply 사용 규칙
수신 객체 람다 내부에서 수신 객체의 함수를 사용하지 않고 수신 객체 자신을 다시 반환 하려는 경우에 apply 를 사용합니다.    
수신 객체 의 프로퍼티 만을 사용하는 대표적인 경우가 객체의 초기화 이며, 이곳에 apply 를 사용합니다.    
```kotlin
val peter = Person().apply {
    // apply 의 블록 에서는 오직 프로퍼티 만 사용합니다!
    name = "Peter"
    age = 18
}
```
2. also 사용 규칙
수신 객체 람다가 전달된 수신 객체를 전혀 사용 하지 않거나 수신 객체의 속성을 변경하지 않고 사용하는 경우 also 를 사용합니다.    
also 는 apply 와 마찬가지로 수신 객체를 반환 하므로 블록 함수가 다른 값을 반환 해야하는 경우에는 also 를 사용할수 없습니다.    
예를 들자면, 객체의 사이드 이팩트를 확인하거나 수신 객체의 프로퍼티에 데이터를 할당하기 전에 해당 데이터의 유효성을 검사 할 때 매우 유용합니다.    
```kotlin
class Book(author: Person) {
    val author = author.also {
      requireNotNull(it.age)
      print(it.name)
    }
}
```
3. let 사용 규칙
다음과 같은 경우에 let 을 사용합니다.
* 지정된 값이 null 이 아닌 경우에 코드를 실행해야 하는 경우.
* Nullable 객체를 다른 Nullable 객체로 변환하는 경우.
* 단일 지역 변수의 범위를 제한 하는 경우.
```kotlin
getNullablePerson()?.let {
    // null 이 아닐때만 실행됩니다.
    promote(it)
}
val driversLicence: Licence? = getNullablePerson()?.let {
    // nullable personal객체를 nullable driversLicence 객체로 변경합니다.
    licenceService.getDriversLicence(it) 
}
val person: Person = getPerson()
getPersonDao().let { dao -> 
    // 변수 dao 의 범위는 이 블록 안 으로 제한 됩니다.
    dao.insert(person)
}
```
4. with 사용 규칙
Non-nullable (Null 이 될수 없는) 수신 객체 이고 결과가 필요하지 않은 경우에만 with 를 사용합니다.
```kotlin
val person: Person = getPerson()
with(person) {
    print(name)
    print(age)
}
```
5. run 사용 규칙
어떤 값을 계산할 필요가 있거나 여러개의 지역 변수의 범위를 제한하려면 run 을 사용합니다.
매개 변수로 전달된 명시적 수신객체 를 암시적 수신 객체로 변환 할때 run ()을 사용할수 있습니다.
```kotlin
val inserted: Boolean = run {
    // person 과 personDao 의 범위를 제한 합니다.
    val person: Person = getPerson()
    val personDao: PersonDao = getPersonDao()
    // 수행 결과를 반환 합니다.
    personDao.insert(person)
}
fun printAge(person: Person) = person.run {
    // person 을 수신객체로 변환하여 age 값을 사용합니다.
    print(age)
}
```