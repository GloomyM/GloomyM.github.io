---
title: Matplotlib库数据处理
date: 2020-04-08 11:26:46
tags: Python
categories: 
  - 学习历程
  - 大数据分析
---

### 简介：
**Matplotlib 是 Python 的绘图库。 它可与 NumPy 一起使用，提供了一种有效的 MatLab 开源替代方案。在数据分析中尤为重要**

<!-- more -->

### 安装方式：
**这里我使用清华大学的镜像进行安装（当然你也可以选择其他镜像）：**
`pip install matplotlib --index https://pypi.mirrors.ustc.edu.cn/simple/`

### 基础函数及用法：

| 函数          | 描述                              |
| ------------- | --------------------------------- |
| plt.title()   | 为产生的图像设置主标题            |
| plt.xlabel()  | 为x轴设置标题                     |
| plt.ylabel()  | 为y轴设置标题                     |
| plt.plot()    | 根据参数生成图像                  |
| plt.show()    | 显示所生成的图像                  |
| plt.xlim(l,r) | 设置x轴的左右区间，None表示无限制 |
| plt.ylim(l,r) | 设置y轴的左右区间，None表示无限制 |

### 折线图的绘制：

**plt.plot(x,y)用来生成折线图：x表示x轴的坐标，y表示对应y轴的坐标**

**描述：画出y = 3x+2的图像**

```python
from matplotlib import pyplot as plt
import numpy as np
x = np.arange(1,10)
y = 3*x + 2             #函数y = 3x+2
plt.title("Demo")       #设置主标题
plt.xlabel("This is x") #设置x轴标题
plt.ylabel("This is y") #设置y轴标题
plt.plot(x,y)       #按照上述函数生成
plt.show()
```

**生成图像：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_01.PNG" style="zoom:50%;" />

### 散点图的绘制：

**plt.scatter(x,y,s,c,marker)：x，y表示数据，要求长度相等且必须为向量，s表示散点大小，c表示散点颜色，marker表示散点形式**

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.random.normal(0,1,150) #随机生成两组数据
y = np.random.normal(0,1,150)
plt.scatter(x,y)	#生成散点图
plt.show()
```

**生成图像：**

**高级散点绘制：**

```python
import matplotlib.pyplot as plt
import numpy as np

fig,ax = plt.subplots()#后文有详细讲解

for color in ['purple','green','yellow']:
    x = np.random.normal(0,1,150)
    y = np.random.normal(0,1,150)
    ax.scatter(x,y,c = color,label = color)	#c表示散点颜色，label表示图例颜色

plt.legend() #生成图例
plt.show()
```

**图像生成：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_10.PNG" style="zoom:50%;" />

#### 相关样式：

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_03.PNG"  />

![](https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_04.PNG)



### 条形图的绘制：

**Pyplot子模块提供bar()函数来生成条形图。以下实例生成两组 x 和 y 数组的条形图。**

```python
from matplotlib import pyplot as plt 
x =  [5,8,10] 
y =  [12,16,6] 
x2 =  [6,9,11] 
y2 =  [6,15,7] 
plt.bar(x, y, align =  'center') 
plt.bar(x2, y2, color =  'g', align =  'center') #条形图颜色为绿色并居中
plt.title('Bar graph') 
plt.ylabel('Y axis') 
plt.xlabel('X axis') 
plt.show()
```

**生成图像：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_05.PNG" style="zoom:50%;" />

### 直方图的绘制：

**plt.hist() 函数是数据的频率分布的图形表示。 水平尺寸相等的矩形对应于类间隔，称为 bin，变量 height 对应于频率。plt.histogram()函数将输入数组和 bin 作为两个参数。 bin 数组中的连续元素用作每个 bin 的边界。**

```python
from matplotlib import pyplot as plt 
import numpy as np  
 
a = np.array([22,87,5,43,56,73,55,54,11,20,51,5,79,31,27]) 
plt.hist(a, bins =  [0,20,40,60,80,100]) 
plt.title("Histogram") 
plt.show()
```

**生成图像：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_06.PNG" style="zoom:50%;" />

**直方图高级用法：**

**histtype参数说明:**
**bar是传统的条形直方图。如果给定多个数据，则条并排排列。**
**barstacked是一种条形直方图，其中多个数据相互叠加。**
**step生成默认为未填充的线条图。**
**stepfilled生成默认填充的线条图。**

```python
import matplotlib.pyplot as plt
import numpy as np

fig,ax = plt.subplots(2,2)
x = np.random.randn(1000, 3)

colors = ['red','blue','yellow']

ax[0][0].hist(x,10,density = True,histtype = 'bar',color = colors,label = colors)
ax[0][0].set_title("Bars with legend")
plt.legend(prop={'size': 8})

ax[0][1].hist(x,10,density = True,histtype = 'bar',stacked = True)
ax[0][1].set_title('Stacked Bar')

ax[1][0].hist(x, 10, histtype='step', stacked=True)
ax[1][0].set_title('Stack Step (unfilled)')

x_multi = [np.random.randn(n) for n in [10000, 5000, 2000]]
ax[1][1].hist(x_multi, 10, histtype='bar')
ax[1][1].set_title('Different Sample Sizes')

plt.tight_layout() #会自动调整子图参数，使它填充整个图像区域，避免文字重合
plt.show()
#代码参考:https://blog.csdn.net/qq_38251616/article/details/103802310
```

**图像生成：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_11.PNG" style="zoom:50%;" />



### subplot()和subplots()：

#### subplots():

**将多组数据放到一张图显示的操作**

```python
fig, ax = plt.subplots()
```

**subplots返回两个参数，fig：matplotlib.figure.Figure 对象，ax：子图对象（ matplotlib.axes.Axes）**

**subplots(2,3)表示生成2*3的网格，可以调用ax[i,j]进行调用，在网格的不同位置生成图像**

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(0,10)
fig,ax = plt.subplots()
for i in range(10):
    ax.plot(x+i)
plt.show()
```

**生成图像：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_07.PNG" style="zoom:50%;" />

#### subplot:

**subplot(n,m,k)在生成的n*m个网格的第k（从第一行第一列开始依次计数）个位置绘图**

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.arange(0,10)
for i in range(1,7):
    plt.subplot(2,3,i) #2*3的网格，第i个位置
    plt.plot(x+i)
plt.show()
```

**生成图像：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_08.PNG" style="zoom:50%;" />

#### 实例1：

**描述：在一张图中画出正弦余弦函数**

```python
from matplotlib import pyplot as plt
import numpy as np
x = np.arange(1,10)
siny = np.sin(x)
cosy = np.cos(x)
plt.subplot(2,1,1)#生成一个2*1的网络，激活第一张图
plt.title("Sin x")
plt.xlabel("x")
plt.ylabel("y")
plt.plot(x,siny)
plt.subplot(2,1,2)#激活第二张图
plt.title("Cos x")
plt.xlabel("x")
plt.ylabel("y")
plt.plot(x,cosy)
plt.show()
```
**生成图像：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python-Matplotlib%E5%BA%93/Image_02.PNG" style="zoom:50%;" />



**英文参考文档：**

**https://matplotlib.org/api/_as_gen/matplotlib.pyplot.hist.html?highlight=hist#matplotlib.pyplot.hist**