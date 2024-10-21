---
layout: post
title: Dataset Load1
description: Dataset Load1
summary: Dataset Load1
tags: 
minute: 1
---
```python
import matplotlib.pyplot as plt
import tensorflow as tf
import numpy as np
import sys

(train_images, train_labels), (test_images, test_labels) = tf.keras.datasets.mnist.load_data()

print(type(train_images))
print(train_images.shape)
print(train_labels.shape)
print(test_images.shape)
print(test_labels.shape)

print(sys.getsizeof(train_images)/1024/1024)

train_ds = tf.data.Dataset.from_tensor_slices((train_images, train_labels))
train_ds = train_ds.shuffle(60000).batch(9)

test_ds = tf.data.Dataset.from_tensor_slices((test_images, test_labels))
test_ds = test_ds.batch(9)

train_ds_iter = iter(train_ds)
images, labels = next(train_ds_iter)

print(images.shape)
print(labels.shape)

fig, axes = plt.subplots(3, 3, figsize=(5, 5))

for ax_idx, ax in enumerate(axes.flat):
  image = images[ax_idx, ...]
  label = labels[ax_idx]

  ax.imshow(image.numpy(), 'gray')
  ax.set_title(label.numpy(), fontsize=10)

  ax.get_xaxis().set_visible(False)
  ax.get_yaxis().set_visible(False)
```