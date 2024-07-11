---
layout: post
title: "[C++] 유용한 C++ 기능 - attribute specifier"
description: "[C++] 유용한 C++ 기능 - attribute specifier"
summary: "[C++] 유용한 C++ 기능 - attribute specifier"
tags: 
minute: 1
---
[Reference](https://devjino.tistory.com/385)    

C++11부터 도입된 attribute specifier(속성 지정자)는 코드의 컴파일러에 대한 추가 정보를 제공하는 데 사용됩니다. 이를 통해 개발자는 특정 컴파일러에 맞춰진 속성을 지정하거나, 코드에 대한 최적화 및 다른 목적으로 사용자 정의 속성을 추가할 수 있습니다.    

Attribute specifier는 대괄호 [[와 ]]로 묶여진 형태로 사용됩니다. 아래는 attribute specifier의 간단한 예제입니다:    
```c++
[[noreturn]]
void SomeFunc()
{
  ...
  return;	// 함수 내부에 리턴문이 있으면 컴파일 에러가 발생합니다. 
  			// 중간에 리턴문으로 인해 의도하지 않게 함수의 모든 코드를 
            // 실행할 수 없는 상황을 막는데 용이합니다.
  ...
}
 
[[nodiscard]]
bool InsertData(int data) { ... }
InsertData(3); // 리턴값을 무시했기 때문에 컴파일 에러 발생.
 
// 이 함수를 사용할 때 경고 메시지가 뜹니다.
[[deprecated("use Something2 instead")]]
void Something() {}
```

일반적으로 사용되는 몇 가지 속성에 대한 설명은 다음과 같습니다:    

[[deprecated]]: 해당 함수 또는 변수가 더 이상 사용되지 않아야 함을 나타냅니다.    
[[noreturn]]: 함수가 반환하지 않는다는 것을 나타냅니다. 이 속성은 함수의 반환 타입이 void가 아닌 경우에 사용됩니다.    
[[nodiscard]]: 함수의 반환값을 무시하지 말라는 경고를 표시합니다.    
[[fallthrough]]: switch 문에서 fallthrough 주석을 사용하지 않아도 떨어지는 것이 의도된 동작임을 나타냅니다.    
[[maybe_unused]]: 해당 변수가 사용되지 않아도 경고를 발생시키지 않도록 합니다.    
[[optimize("옵션")]]: 컴파일러에게 특정 최적화 옵션을 지정합니다.