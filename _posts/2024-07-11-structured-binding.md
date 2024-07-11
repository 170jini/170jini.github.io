---
layout: post
title: "[C++] 유용한 C++ 기능 - structured binding"
description: "[C++] 유용한 C++ 기능 - structured binding"
summary: "[C++] 유용한 C++ 기능 - structured binding"
tags: 
minute: 1
---
[Reference](https://devjino.tistory.com/383)    

C++17에서 도입된 structured binding은 복합적인 데이터 구조를 손쉽게 풀어낼 수 있는 기능을 제공합니다. 이를 통해 배열, 튜플, 구조체 등에서 멤버를 간단하게 추출하여 사용할 수 있습니다.    

Structured binding은 다음과 같은 문법을 사용합니다:    
```c++
auto [변수1, 변수2, ...] = 표현식;
```

여기서 표현식은 풀어낼 데이터 구조를 나타내며, 변수1, 변수2 등은 구조체나 튜플의 각 요소에 대응됩니다.    
예를 들어, 튜플을 사용한 structured binding은 다음과 같이 보입니다:    
```c++
#include <iostream>
#include <tuple>

int main() {
    std::tuple<int, double, std::string> myTuple(42, 3.14, "Hello");

    auto [a, b, c] = myTuple;

    std::cout << "a: " << a << ", b: " << b << ", c: " << c << std::endl;

    return 0;
}
```

위의 코드에서 auto [a, b, c] = myTuple; 구문은 튜플 myTuple의 각 요소를 a, b, c 변수에 각각 할당합니다. 이를 통해 각 요소에 간단하게 접근할 수 있습니다.    

Structured binding은 배열, 구조체 등 다양한 데이터 구조에서도 사용할 수 있으며, 코드의 가독성을 높이고 반복적인 코드를 줄이는 데 도움이 됩니다.