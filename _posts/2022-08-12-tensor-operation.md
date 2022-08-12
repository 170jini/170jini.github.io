---
layout: post
title: 텐서와 연산
description: 텐서와 연산
summary: 텐서와 연산
tags: 
minute: 1
---
#### TensorFlow 가져오기    
시작하기 위해서 텐서플로 모듈을 임포트합니다. 텐서플로 2.0에서는 즉시 실행(eager execution)이 기본적으로 실행됩니다. 이는 텐서플로를 조금 더 대화형 프론트엔드(frontend)에 가깝게 만들어 줍니다. 세부사항은 나중에 이야기할 것입니다.    
```python
import tensorflow as tf
```
#### 텐서
텐서는 다차원 배열입니다. NumPy ndarray 객체와 유사하게 tf.Tensor 객체에는 데이터 유형과 형상이 있습니다. 또한 tf.Tensor는 가속기 메모리(예: GPU)에 상주할 수 있습니다. TensorFlow는 tf.Tensor를 소비하고 생성하는 풍부한 연산 라이브러리를 제공합니다(tf.add, tf.matmul, tf.linalg.inv 등). 이러한 연산은 기본 Python 유형을 자동으로 변환합니다. 예를 들면 다음과 같습니다.    