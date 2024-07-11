---
layout: post
title: "[C++] 유용한 C++ 기능 - if / switch init statement"
description: "[C++] 유용한 C++ 기능 - if / switch init statement"
summary: "[C++] 유용한 C++ 기능 - if / switch init statement"
tags: 
minute: 1
---
[Reference](https://devjino.tistory.com/382)    

로컬 변수의 생명주기가 블럭과 같도록 합니다.    
if 문 이후에 x 변수가 잘못 사용되는 위험을 방지하고 코드의 의도를 명확히 합니다.    

```c++
if (int x = getX(); x > 0) {
    // x가 0보다 큰 경우에 실행되는 코드
    // x를 여기서 사용할 수 있음
} else {
    // x가 0 이하인 경우에 실행되는 코드
}
```

위의 예제에서 getX() 함수는 변수 x를 초기화하는데 사용됩니다. 이렇게 하면 if 블록 내에서만 x가 유효하게 됩니다.    
다음은 switch에서 사용하는 예시입니다.    

```c++
switch (int value = getValue(); value) {
    case 1:
        // value가 1인 경우에 실행되는 코드
        break;
    case 2:
        // value가 2인 경우에 실행되는 코드
        break;
    default:
        // 위의 case에 해당하지 않는 경우에 실행되는 코드
        break;
}
```

switch 문에서도 비슷한 방식으로 초기화 구문을 사용할 수 있습니다. getValue() 함수가 반환한 값으로 value 변수를 초기화하며, 각 case에서 value 값을 비교합니다.    
이렇게 초기화 구문을 사용하면 변수의 범위(scope)를 더욱 지역화할 수 있고, 코드의 가독성을 향상시킬 수 있습니다. 다만, 이 기능을 사용할 때에는 해당 변수가 if 블록이나 switch 문의 바깥에서 사용되지 않도록 주의해야 합니다.