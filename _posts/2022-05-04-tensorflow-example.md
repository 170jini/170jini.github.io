---
layout: post
title: Tensorflow Example
description: Tensorflow Example
summary: Tensorflow Example
tags: 
minute: 1
---
```python
import tensorflow as tf
import numpy as np
import matplotlib
import matplotlib.pyplot as plt

matplotlib.use('WebAgg')

x_data = tf.random.normal(shape=[10,], dtype=tf.float32)
y_data = 3 * x_data + 1

w = tf.Variable(-1.)
b = tf.Variable(-1.)

learning_rate = 0.01

w_trace, b_trace = [], []
for x, y in zip(x_data, y_data):
    with tf.GradientTape() as tape:
        prediction = w * x + b
        loss = (prediction - y) ** 2
    
    gradients = tape.gradient(loss, [w, b])
    
    w_trace.append(w.numpy())
    b_trace.append(b.numpy())
    w = tf.Variable(w - learning_rate * gradients[0])
    b = tf.Variable(b - learning_rate * gradients[1])
    
plt.plot(w_trace, label='weight')
plt.plot(b_trace, label='bias')
plt.show()
```