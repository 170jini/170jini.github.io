---
layout: post
title: "[C++] std::function"
description: "[C++] std::function"
summary: "[C++] std::function"
tags: 
minute: 1
---
[Reference](https://devjino.tistory.com/152)    

C++11표준 라이브러리의 한 템플릿으로, 함수 포인터 개념을 일반화한 것입니다. 함수 포인터는 함수만 가리킬 수 있지만 std::function은 호출 가능한 객체이면 그 어느 것도 가리킬 수 있습니다. 즉, 함수 처럼 호출 할 수 있는 것이면 그 무엇이라도 std::function으로 가리킬 수 있습니다.    

예를 들면 함수, operator(), 람다 함수들이 있으며 다음은 그 예시입니다.    

```c++
int sum(int a, int b) {
	return a + b;
}

struct Sum {
	int operator()(int a, int b) { return a + b; }
};

int main() {
	std::function<int(int, int)> s1 = sum;
	std::function<int(int, int)> s2 = Sum();
	std::function<int(int, int)> s3 = [](int a, int b) -> int { return a + b; };

	std::cout << s1(1, 2) << std::endl;
	std::cout << s2(1, 2) << std::endl;
	std::cout << s3(1, 2) << std::endl;
}
```

멤버 변수를 참조하는 경우는 사용방법이 조금 다릅니다.    

```c++
class TwoNum {
	int a = 1;
	int b = 2;

public:
	int sum() { return a + b; }
};

int main() {
	TwoNum a;

	std::function<int()> s1 = a.sum;

	s1();
}
```

위 코드는 다음과 같은 컴파일 오류가 발생합니다.    
error C3867:  'TwoNum::sum': 비표준 구문입니다. '&'를 사용하여 멤버 포인터를 만드세요.    
이유는 s1을 호출 했을때 a + b에서 어떤 객체 인스턴스의 a와 b인지 모르기 때문입니다.    
이럴땐, 멤버 변수를 참조하는 경우에는 다음과 같이 std::function을 사용하면 됩니다.    

```c++
class TwoNum {
	int a = 1;
	int b = 2;

public:
	int sum() { return a + b; }
};

int main() {
	TwoNum a;

	std::function<int(TwoNum&)> s2 = &TwoNum::sum;

	s2(a);
}
```