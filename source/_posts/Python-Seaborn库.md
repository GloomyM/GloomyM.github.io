---
title: Seaborn库数据处理
date: 2020-04-08 16:20:20
tags: Python
categories: 
  - 学习历程
  - 大数据分析
---

### 简介：

**Seaborn是Matplotlib的强大的一个扩展。可以通过Seaborn实现简单的需求，且代码量较少**

<!-- more -->

### Seaborn与Matplotib的比较

**描述：导入鸢尾花数据集，画出花萼和花瓣的长度散点图，利用不同颜色区分花的种类并实现图例**

**使用Matplotib**

```python
import pandas as pd
import matplotlib.pyplot as plt

iris = pd.read_csv('iris.csv')#导入鸢尾花数据集

color = dict(zip(iris.Species.unique(),['red','blue','purple']))
#按照花名生成对应的颜色字典,unique函数用来去重

for name,group in iris.groupby('Species'):	#groupby函数按照花名进行分类
    plt.scatter(group['Petal.Length'],group['Sepal.Length'],color = color[name],alpha=0.5,label = name) #x轴花瓣，y轴花萼，图例(label)为花名，透明度(alpha)0.5

plt.legend(title = 'Name') #图例名称设置为Name
plt.xlabel('Petal.Length') #x轴名称
plt.ylabel('Sepal.Length')  #y轴名称
plt.show()
plt.tight_layout()
```

**图像生成：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python--Seaborn%E5%BA%93/Image_01.PNG" style="zoom:50%;" />

**使用Seaborn**

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

iris = pd.read_csv('iris.csv')#导入鸢尾花数据集
color = dict(zip(iris.Species.unique(),['red','blue','purple']))
#根据花名生成颜色字典
sns.lmplot('Petal.Length','Sepal.Length',iris,hue='Species',fit_reg=False)
#hue用来设置分类类似于groupby
plt.show()
```

**图像生成：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python--Seaborn%E5%BA%93/Image_02.PNG" style="zoom:50%;" />

**由此可见利用Seaborn绘制图像代码量要少很多**

### Seaborn绘制直方图

**Seaborn中的方法distplot用来生成直方图，它支持一些参数：**

**bins：直方图的分块**
**hist：True表示绘制直方图，默认为True**
**kde：True表示绘制密度图，默认为True**
**rug：显示分布情况，默认为False不显示**

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np

x = np.random.randn(1000)
sns.distplot(x,hist=True,color = 'purple')
plt.show()
```

**生成图像（密度图为图中的曲线）:**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python--Seaborn%E5%BA%93/Image_03.PNG" style="zoom:50%;" />

### Seaborn绘制密度图：

**kdeplot方法用来生成密度图**

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np

x = np.random.randn(1000)
sns.kdeplot(x,shade = True ,color = 'purple') #shade表示是否生成填充（默认为False）
plt.show()
```

**图像生成：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python--Seaborn%E5%BA%93/Image_04.PNG" style="zoom:50%;" />

### Seaborn绘制热力图：

**heatmap()方法用来生成热力图**

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np

data = sns.load_dataset('flights') #下载数据集
data = data.pivot(index = 'month',columns = 'year',values = 'passengers')
#将数据集转换为month\columns的表
sns.heatmap(data)#生成热力图
plt.show()
```

**图像生成：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python--Seaborn%E5%BA%93/Image_05.PNG" style="zoom:50%;" />

### Seaborn绘制柱状图：

**barplot方法用来绘制柱状图**

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np

data = sns.load_dataset('flights')
data = data.pivot(index = 'month',columns = 'year',values = 'passengers')
data = data.sum()#求出每年乘客的总数
sns.barplot(data.index,data.values)#分别设置x，y坐标
plt.show()
```

**图像生成：**

<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python--Seaborn%E5%BA%93/Image_06.PNG" style="zoom:50%;" />

### DataFrame.pivot:

**上文使用了privot方法，改方法用于对数据集进行格式化**

**例如：data = data.pivot(index = 'month',columns = 'year',values = 'passengers')，实际上就生成了一个这样的表格：**

**<img src="https://personalblog-1301685299.cos.ap-nanjing.myqcloud.com/MyBlog-Images/Python--Seaborn%E5%BA%93/Image_07.PNG" style="zoom:50%;" />**

**月份代表索引，年份定义为列，这样看就一目了然了**

**Tip：在使用数据透视时要保证index和colunms可以有唯一的对应**

### DataFrame里的数据提取：

**当读取一个数据集时，一般会先输出部分内容以观察数据，这里就用到了DataFrame.head()，输出前五组数据，如果想查看某个具体属性的数据，可以使用DataFrame.属性名的方式进行查看**

```python
import seaborn as sns
import matplotlib.pyplot as plt


data = sns.load_dataset("car_crashes")#导入数据集
print(data.head())#查看前五条数据
for item in data.speeding: #查看属性名为speeding的所有数据
    print(item)
```

