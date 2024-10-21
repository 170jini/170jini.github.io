---
layout: post
title: Dataset Split
description: Dataset Split
summary: Dataset Split
tags: 
minute: 1
---
```python
import tensorflow_datasets as tfds
import matplotlib.pyplot as plt
import tensorflow as tf
import numpy as np

(train_validation_ds, test_ds), ds_info = tfds.load(name='mnist',
                                                    shuffle_files=True,
                                                    as_supervised=True,
                                                    split=['train', 'test'],
                                                    with_info=True)

n_train_validation = ds_info.splits['train'].num_examples
train_ratio = 0.8
n_train = int(n_train_validation * train_ratio)
n_validation = n_train_validation - n_train

train_ds = train_validation_ds.take(n_train)
remaining_ds = train_validation_ds.skip(n_train)
validation_ds = remaining_ds.take(n_validation)

train_ds = train_ds.shuffle(100).batch(32)
validation_ds = validation_ds.batch(32)
test_ds = test_ds.batch(32)

train_ds_iter = iter(train_ds)
images, labels = next(train_ds_iter)

print(images.shape)
print(labels.shape)
```