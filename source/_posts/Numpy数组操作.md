---
title: Numpy数组数据处理
date: 2020-04-06 19:54:4
tags: Python
categories: 
  - 学习历程
  - 大数据分析
---

### Numpy库为什么如此高效
**Numpy是由C语言编写，整体执行效率高，Numpy数组内的数据必须是完全统一的，比如全部是浮点型，而Python列表中支持任意类型数据的随意组合，Numpy数组内的数据连续存储在内存中，而Python列表数据分散在内存中，这种存储结构，与一些更加高效的底层处理方法更加的契合，除此之外，Python语言执行有线程锁，无法真正实现多线程，而C语言可以，因此Numpy库的效率更高**

<!-- more -->

### 什么时候用Numpy
**在数据处理的过程中，遇到for循环实现的一些向量化，矩阵化操作的时候，优先考虑Numpy
1、两个向量的点乘
2、矩阵乘法**

### Numpy数组的创建
#### 1、通过列表创建
```python
import numpy
x = numpy.array([1,2,3],dtype="int") #dtype表示数据类型
print(x)
```
#### 2、从头创建数组
**（1）创建一维数组初值为0**

```python
x = numpy.zeros(5,dtype = int)
#表示创建一个5个元素都为0的一维数组
```
**（2）创建二维数组初值为1**
```python
x = numpy.ones((2,4),type = int)
#表示创建一个2 * 4的int型二维数组，并且初值都为1
```
**（3）创建自定义二维数组**

```python
x = numpy.full((2,4),8)
#表示创建一个2 * 4的二维数组，并且初值为8
```
**（4）创建单位矩阵**

```python
x = numpy.eye(3)
#表示创建一个3*3的单位矩阵
```
**（5）创建线性序列**

```python
numpy.arange(1,10,2)
#从1到10步长为2创建序列
```
**（6）创建等差数列**

```python
x = numpy.linspace(1,10,4)
#a1 = 1,a4 = 10
```
**（7）创建等比数列**

```python
x = numpy.logspace(1,9,2)
#a1 = 2的0次方，a9 = 2的9次方
```
**（8）创建0-1之间随机分布的数组**

```python
x = numpy.random.random(3*3)
#生成一个3 * 3的元素都为0-1之间随机分布的数组
```
**（9）创建整数类型的随机数组**

```python
x = numpy.random.randint(0,10,(3,3))
#创建一个0-10之间随机元素组成的3*3的二维矩阵
```
**（10）数组的合并**

```python
a = [1,2,3]
b = [4,5,6]
x = numpy.concatenate((a,b)) #将数组a，b合并为数组x
print(x)
```

**Tip：Numpy数组中的切片与Python列表基本一致**

### Numpy数组的属性
#### 1、shape返回数组的形状
```python
x = numpy.full((2,4),8)
print(x.shape[0]) # 返回数组的行
print(x.shape[1) # 返回数组的列
```
#### 2、nidm返回数组的维度
```python
x = numpy.full((2,4),8)
print(x.nidm)#这里输出的结果就为2，因为是2维数组
```
#### 3、size返回数组的大小（即元素个数）
```python
x = numpy.full((2,4),8)
print(x.size)#这里输出的结果就为8，因为是2*4的二维数组
```
#### 4、mean()返回数组的算术平均值

```python
x = numpy.arange(24).reshape((2,3,4))
print(x.mean())
```

### Numpy数组的变形

#### 1、reshape(n,m): 

将数组转换为n行m列的数组（不改变原数组）

```python
import numpy as np
x1 = np.arange(1,7).reshape(2,3)
print(x1)
```
#### 2、resize(n,m):

用法和reshape一样但直接改变原数组

#### 3、flatten()：

**将数组转换为一维向量（返回的是副本）**

#### 4、ravel():

**将数组转换为一维向量（返回的是视图）**

### Numpy数组的拼接
#### 1、np.hstack()/np.c_[]：

**水平拼接，要保证两个数组的行数一致**

#### 2、np.vstack()/np.r_[]:

**垂直拼接，要保证两个数组列数一致**

### Numpy数组的分割：
#### 1、np.hsplit(x,[2,4]):

**水平分割，将数组x从第2行，第四行分割成三部分**

#### 2、np.vsplit(x,[2,4]):

**垂直分割，将数组x从第2列，第四列分割成三部分**

### Numpy数组的运算：
#### 向量运算：
**Numpy数组在执行运算时，是对数组内的每一个元素进行运算，下面介绍除基本运算以外的其他运算**

| 函数                                                         | 描述                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| np.abs(x)                                                    | 对x中的所有元素进行绝对值运算                        |
| np.sin(x) / np.cos(x) / np.tan(x) / np.arcsin(x) / np.arccos(x) / np.arctan(x) | 对x中的元素进行三角函数及反三角函数的相关运算        |
| np.exp(x)                                                    | 对x中的元素进行指数运算（e）                         |
| np.ln(x) / np.log2(x) / np.log10(x)                          | 对x中的元素进行对数运算（以e/2/10为底）              |
| np.rint(x)                                                   | 对数组各元素的值四舍五入                             |
| np.modf(x)                                                   | 将数组各元素的小数和整数部分以两个独立的数组形式返回 |





```python
import numpy as np
x1 = np.arange(1,7).reshape(2,3)
print(x1)
print(x1 + 4)
```
#### 矩阵运算：
**（1）x.T：返回x的转置矩阵**
**（2）x.dot(y) / np.dot(x,y)：返回矩阵x与矩阵y相乘的结果，这里与x * y不同，x * y是向量相乘也就是对应项相乘，而矩阵的乘法要严格遵守数学中的矩阵乘法规则**

#### 比较运算和掩码
```python
import numpy as np
x1 = np.arange(-3,3).reshape(2,3) #生成一个2行3列，数据由-3~3构成的数组
x2 = x1 > 0 #返回x1 > 0 的布尔数组
print(x2)
```
**np.sum()**
```python
import numpy as np
x1 = np.arange(-3,3).reshape(2,3) #生成一个2行3列，数据由-3~3构成的数组
print(x1)
print(np.sum(x1 > 0)) #这里返回的不是大于0的数字的和，而是大于0的数字个数
```
**np.all()**
```python
import numpy as np
x1 = np.arange(-3,3).reshape(2,3) #生成一个2行3列，数据由-3~3构成的数组
print(x1)
print(np.all(x1 > 0)) #如果数组x1中所有的元素都满足大于0的条件输出True，否则输出False
```
**np.any()**
```python
import numpy as np
x1 = np.arange(-3,3).reshape(2,3) #生成一个2行3列，数据由-3~3构成的数组
print(x1)
print(np.any(x1 > 0)) #如果数组x1中至少有一个元素都满足大于0的条件输出True，否则输出False
```
#### 将布尔数组作为掩码
```python
import numpy as np
x1 = np.arange(-3,3).reshape(2,3) #生成一个2行3列，数据由-3~3构成的数组
print(x1[x1 > 0]) #将布尔数组中所有返回为True的元素输出
```
#### 花哨索引
**一维向量的花哨索引：**
```python
import numpy as np
x = np.arange(1,7).reshape(-1) #建立一个一维数组
index = [0,2,4]
print(x[index])             #输出下标为0,2,4的元素
```
**二维向量的花哨索引：**
```python
import numpy as np
x = np.arange(1,7).reshape(2,3) #建立一个一维数组
print(x)
index = [[0,1],[1,2]]
print(x[index])             #输出下标为[0,1],[1,2]的元素
```

### Numpy中的广播

NumPy中，形状不同的数组之间也可以进行运算。之前的例子中，在 2×2的矩阵A和标量10之间进行了乘法运算。在这个过程中，如图所示， 标量10被扩展成了2×2的形状，然后再与矩阵A进行乘法运算。这个巧妙 的功能称为广播（broadcast）。

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Numpy%E6%95%B0%E7%BB%84/Img01.png)

```python
import numpy as np

x1 = np.arange(1,7).reshape(2,3) #2行3列的二维数组
x2 = np.arange(1,4).reshape(-1)  #一维数组
print(x1)
print(x2)
print(x1*x2)	#相乘时一维数组自动扩展，变为二维数组，再进行相乘
```

### CSV文件

#### np.savetxt

np.savetxt(frame,array,fmt = '',delimiter = None)

frame:文件、字符串或产生器，可以是.gz或.bz2的压缩文件

array:存储文件的数组

fmt:写入文件的格式。例如'%d'

delimiter: 分割字符串，默认是任何空格

#### np.loadtxt

np.loadtxt(frame,dtype = , delimiter = None,unpack = False)

frame:文件、字符串或产生器，可以是.gz或.bz2的压缩文件

delimiter: 分割字符串，默认是任何空格

dtype:数据类型，可选

Tip：Numpy数组在数据处理中尤为重要🙃