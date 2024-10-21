---
layout: post
title: "[C++] 유용한 C++ 기능 - brace initialization"
description: "[C++] 유용한 C++ 기능 - brace initialization"
summary: "[C++] 유용한 C++ 기능 - brace initialization"
tags: 
minute: 1
---
[Reference](https://devjino.tistory.com/384)    

기본 초기화의 문제점    
```c++
// #1. 멤버 변수 배열은 초기화할 수 있는 방법이 없다.
struct A
{ 
  int arr[100];  
};
 
// #2. POD 동적 할당을 초기화할 수 있는 방법이 없다.
char* buff = new char[100];
 
// #3. STL 컨테이너를 초기화할 수 없다.
std::vector<int> vec;
 
// #4. 타입에 따라 초기화 구문이 일관적이지 않다.
int i(10); // 10으로 초기화
A a(); // a는 기본 생성자로 초기화?? A 타입을 리턴하는 함수 선언??
```

C++11에서 도입된 중괄호 {}를 사용한 초기화 방식을 "brace initialization" 또는 "uniform initialization"이라고 부릅니다.    
```c++
int myInt = 42;  // 기존의 초기화 방식
int myInt2(42);  // 기존의 초기화 방식
int myInt3 = {42};  // brace initialization
```

__*일관된 초기화 문법*__    
중괄호를 사용한 brace initialization은 여러 타입에 대해 일관된 문법을 제공합니다. 이로 인해 초기화 방식에 일관성이 생겨 코드의 가독성이 향상됩니다.    

__*자동 형 변환 방지*__    
```c++
int myInt = 3.14;  // 자동 형 변환 발생
int myInt2(3.14);  // 자동 형 변환 발생
int myInt3 = {3.14};  // 자동 형 변환 방지, 에러 발생
```

__*brace initialization 으로 초기화 코드*__    
```c++
struct A
{
  int arr[100]{1,2,3,4}; // 나머지는 0으로 초기화
};
 
char* buff = new char[100]{'a','b','c'};  // 나머진 '\0'으로 초기화
 
std::vector<int> vec{1,2,3,4};
 
int a{10};
A a{};
```