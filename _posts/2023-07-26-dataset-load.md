---
layout: post
title: Dataset Load2
description: Dataset Load2
summary: Dataset Load2
tags: 
minute: 1
---
```python
import tensorflow_datasets as tfds
import matplotlib.pyplot as plt
import numpy as np

(train_ds, validation_ds, test_ds), ds_info = tfds.load(name='beans',
                                         shuffle_files=True,
                                         as_supervised=True,
                                         split=['train', 'validation', 'test'],
                                         with_info=True,
                                         batch_size=16)

train_ds_iter = iter(train_ds)
images, labels = next(train_ds_iter)
images = images.numpy()
labels = labels.numpy()
print(images.shape)

fig, axes = plt.subplots(4, 4, figsize=(5, 5))

for ax_idx, ax in enumerate(axes.flat):
  image = images[ax_idx, ...]
  label = labels[ax_idx]

  ax.imshow(image, 'gray')
  ax.set_title(label, fontsize=10)

  ax.get_xaxis().set_visible(False)
  ax.get_yaxis().set_visible(False)
```