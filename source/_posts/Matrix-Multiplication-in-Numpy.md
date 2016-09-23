---
title: Matrix Multiplication in Numpy
date: 2016-09-22 21:35:00
categories: Paper
tags:
---

Recently I have tried to use python as the machine learning language instead of Matlab (no offence to Matlab fans). There are some differences between python and Matlab.

<!-- more -->

* In Matlab, `*` means matrix multiplication while `.*` means  dot multipication. 
* In numpy (a popular package for array processing), element-wise multipication is preferred. For A (m*n) and B (n*k), 

A * B doesn't means matrix multipication. Instead, numpy will find a way to broad one or both the matrix.

```python
import numpy as np
a = np.array([1,2,3])
b = 2
a * b

>>  array([2, 4, 6])
```

`*` only works on the following conditions:

1. they are equal, or
2. one of them is 1

Otherwise it will throw `ValueError: frames are not aligned`

* We can use numpy.dot(A,B) to perform matrix multiplication.

As demonstrated in the numpy official guide:

`For 2-D arrays it is equivalent to matrix multiplication, and for 1-D arrays to inner product of vectors (without complex conjugation). For N dimensions it is a sum product over the last axis of a and the second-to-last of b`