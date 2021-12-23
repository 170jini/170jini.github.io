---
layout: post
title: 코틀린 의 apply, with, let, also, run
description: 코틀린 의 apply, with, let, also, run
summary: 코틀린 의 apply, with, let, also, run
tags: 
minute: 1
---
1. apply 사용 규칙
수신 객체 람다 내부에서 수신 객체의 함수를 사용하지 않고 수신 객체 자신을 다시 반환 하려는 경우에 apply 를 사용합니다.    
수신 객체 의 프로퍼티 만을 사용하는 대표적인 경우가 객체의 초기화 이며, 이곳에 apply 를 사용합니다.    
```c++
val peter = Person().apply {
    // apply 의 블록 에서는 오직 프로퍼티 만 사용합니다!
    name = "Peter"
    age = 18
}
```