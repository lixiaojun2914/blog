---
title: "Numpy笔记"
date: 2022-01-28T21:12:59+08:00
description: Numpy笔记
slug: numpy
categories:
    - Python
    - Data Processing
    - Machine Learning
    - Deep Learning
tags:
    - 数值计算
    - 矩阵计算
---

# Numpy笔记

## ndarray
### ndarray的属性
```python
import numpy as np

a = np.arange(6).reshape(2, 3)
print(a)
# 维度
print(f'shape: {a.shape}')
# 轴
print(f'ndim: {a.ndim}')
# 元素大小
print(f'itemsize: {a.itemsize}')
# 元素个数
print(f'size: {a.size}')
# 元素类型
print(f'dtype: {a.dtype}')
# 元数据
print(f'data: {a.data}')
```
## 数组创建
```python
# 定义数组形状
>>> s = (3, 3)
# 创建全为零的数组
>>> np.zeros(s)
array([[0., 0., 0.],
       [0., 0., 0.],
       [0., 0., 0.]])
# 创建全为一的数组
>>> np.ones(s)
array([[1., 1., 1.],
       [1., 1., 1.],
       [1., 1., 1.]])
# 创建空数组，元素用随机数填充
>>> np.empty(s)
array([[1., 1., 1.],
       [1., 1., 1.],
       [1., 1., 1.]])
# 创建一个元素全为123的数组
>>> np.full(s, 123)
array([[123, 123, 123],
       [123, 123, 123],
       [123, 123, 123]])
# 创建一个九个元素，形状为s的数组
>>> a = np.arange(9).reshape(s)
# 创建维度和a相同且元素全为零的数组
>>> np.zeros_like(a)
array([[0, 0, 0],
       [0, 0, 0],
       [0, 0, 0]])
# 创建维度和a相同且元素全为一的数组
>>> np.ones_like(a)
array([[1, 1, 1],
       [1, 1, 1],
       [1, 1, 1]])
# 创建维度和a相同的空数组
>>> np.empty_like(a)
array([[0, 0, 0],
       [0, 0, 0],
       [0, 0, 0]])
# 创建一个维度和a相同且元素全为123的数组
>>> np.full_like(a, 123)
array([[123, 123, 123],
       [123, 123, 123],
       [123, 123, 123]])
# 创建一个从10到30，且步距为5的数组
>>> np.arange(10, 30, 5)
array([10, 15, 20, 25])
# 在10到30之间均匀的创建5个元素的数组
>>> np.linspace(10, 30, 5)
array([10., 15., 20., 25., 30.])
```
## 通函数
```python
# 如果全不为0，则为true，否则为false
>>> a = [-1, 0, 1, 2, 3]
>>> np.all(a)
False
# 如果全为0，则为false，否则为true
>>> np.any(a)
True
# 返回最大值的索引
>>> a = [1, 2, 6, 4, 5]
>>> np.argmax(a)
2
# 返回最小值的索引
>>> np.argmin(a)
0
# 计算最大值
>>> np.max(a)
6
# 计算最小值
>>> np.min(a)
1
# 计算平均值
>>> np.mean(a)
3.6
# 计算方差
>>> np.std(a)
1.8547236990991407
# 计算方差
>>> np.var(a)
3.44
# 计算协方差
>>> np.cov(a, a)
array([[4.3, 4.3],
       [4.3, 4.3]])
# 计算元素总和
>>> np.sum(a)
# 计算排序后的下标
>>> np.argsort(a)
array([0, 1, 3, 4, 2], dtype=int64)
# 返回排序后的数组
>>> np.sort(a)
array([1, 2, 4, 5, 6])
# 将元素的值限定在所给的范围内
>>> a = np.arange(10)
>>> np.clip(a, 1, 8)
array([1, 1, 2, 3, 4, 5, 6, 7, 8, 8])
# 如果a和b都是一维向量，则计算两个向量的内积
# 如果a和b都是n维向量，则计算两个向量的外积
# 计算外积建议使用matmul
>>> a = [[1], [2], [3]]
>>> b = [[4, 5, 6]]
>>> np.dot(a, b)
array([[ 4,  5,  6],
       [ 8, 10, 12],
       [12, 15, 18]])
# 计算两个矩阵的成绩
>>> np.matmul(a, b)
array([[ 4,  5,  6],
       [ 8, 10, 12],
       [12, 15, 18]])
# 返回非零元素的下标
>>> a = [0, 1, 2]
>>> np.nonzero(a)
(array([1, 2], dtype=int64),)
# 轴对换函数
>>> a = np.arange(12).reshape(2, 2, 3)
>>> np.transpose(a, (0, 2, 1)).shape
(2, 3, 2)
# 条件成立，输出a，否则输出-1
>>> np.where(a<5, a, -1)
array([[[ 0,  1,  2],
        [ 3,  4, -1]],

       [[-1, -1, -1],
        [-1, -1, -1]]])
```
## 线性代数
```python
# 计算矩阵的逆
a = np.arange(4, dtype=float).reshape(2, 2)
>>> np.linalg.inv(a)
array([[-1.5,  0.5],
       [ 1. ,  0. ]])
# 计算矩阵的迹
>>> np.trace(a)
3.0
# 计算矩阵的特征值和特征向量
>>> np.linalg.eig(a)
(array([-0.56155281,  3.56155281]), array([[-0.87192821, -0.27032301],
       [ 0.48963374, -0.96276969]]))
```
