---
title: Random库
date: 2019-05-17 22:11:23
tags: Python
categories: 学习历程
---

## 简介：
**random库是生成随机数的Python标准库**
**基本随机函数：seed(),random()
扩展随机函数：randint(),getrandbits(),uniform(),randrange(),choice(),shuffle()**

<!-- more -->

## 使用方式：

**① seed(a)：初始化给定的随机数种子，默认为当前系统时间
② random()：生成一个[0.0,1.0]之间的随机小数**
**例如：**

```python
import random as r
r.seed(20)
print(r.random())
```
**③ randomint(a,b)：生成一个数值在a-b之间的随机整数
④ randrange(m,n,k)：生成一个m-n之间k为步长的整数
⑤ getrandbits(k)：生成一个k比特长的随机整数
⑥ uniform(a,b)：生成一个[a,b]之间的随机小数
⑦ choice(seq)：从序列seq中随机选出一个元素
⑧ shuffle(seq)：将序列seq中的元素随机排列，返回打乱后的序列**
**例如：**

```python
import random as r
s = [1,2,3,4,5,6,7]
r.shuffle(s)
print(s)           #输出打印乱后的结果
```
**公式法计算圆周率PI：**
```python
pi = 0
N = 100
for k in range(N+1):
    pi += 1/pow(16,k)*(4/(8*k+1) - 2/(8*k+4) - 1/(8*k+5) - 1/(8*k+6))
print("圆周率的值为：{}".format(pi))
#输出结果为：3.141592653589793
```
**蒙特卡罗法计算圆周率：**
```python
import random as r
import time as t
d = 1000*1000
hits = 0
st = t.perf_counter()
for i in range(d+1):
    x,y = r.random(),r.random()
    if pow(x ** 2 + y ** 2 , 0.5) <= 1.0:
        hits += 1
pi = 4 * hits / d
print("圆周率为:{}".format(pi))
print("程序运行时间为:{:.2f}s".format(t.perf_counter() - st))
```