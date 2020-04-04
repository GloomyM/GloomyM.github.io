---
title: Python基本图形绘制
date: 2019-05-12 14:02:31
tags: Python
---

### turtle的绘图窗体：
**turtle.setup(width,height,startx,starty)前两个参数是分别是窗体的长和宽，后两个参数分别是窗体左上角的横纵坐标。例如turtle.setup(800,800,0,0)这表示我们生成了一个长宽分别为800，800的窗体，左上角的坐标为(0,0)也就是位于屏幕的左上角，如果我们不给后面两个变量赋值，也就是turtle.setup(800,800)，那么窗体位置就默认位于屏幕中间。**

<!-- more -->

### turtle库函数：
##### 运动控制函数：
**turtle.goto(x,y)：从某点到达坐标为(x,y)的点
turtle.bk(d)：向反方向行进
turtle.fd(d)：向正前方行进
turtle.circle(r,angle)：如果r为正则以海龟左侧的点为圆心向左旋转angle°，如果r为负则表示圆心位于海龟右侧的点，并向右侧旋转angel°**
##### 方向控制函数：
**turtle.seth(angle)：改变行进角度但并不行进
turtle.left(angle)：将画笔方向向左旋转
turtle.right(angle)：将画笔方向向右旋转**
##### 画笔控制函数：
**turtle.penup() / turtle.pu()：表示将画笔抬起，不留下痕迹，一般和turtle.pd()成对出现
turtle.pendown() / turtle.pd()：表示将画笔放下，一般和turtle.pu()成对出现
turtle.pensize(width) / turtle.width(width)：设置画笔的宽度
turtle.pencolor(color)：设置画笔的颜色
turtle.write(s,font=("font-name",fontsize,"fonttype"))：写文本，s为文本内容，font是字体的参数，里面分别为字体名称，大小和类型；font为可选项, font的参数也是可选项**

**利用以上内容在画布上画一个Z字形：**
```python
import turtle
turtle.setup(500, 500, 80, 80) #设置一个长宽分别为500的正方形窗口，左上角坐标（80，80）
turtle.left(45)        #画笔向左旋转45°
turtle.fd(50)        #画笔前进50个像素
turtle.right(135) #画笔向右旋转135°
turtle.fd(100)    #画笔前进100个像素
turtle.left(135) #画笔向左旋转135°
turtle.fd(50)    #画笔前进50个像素
turtle.done()   #绘图结束
```

### import的更多用法：
**①import <库名>
调用该库中的函数：<库名>.<函数名>（<函数参数>）
Tip：不会出现函数重名
②from <库名> import *
调用该库中的函数：<函数名>（<函数参数>）
Tip：会出现函数重名
③：import <库名> as <库别名>
调用该库中的函数：<库别名>.<函数名>（<函数参数>）**

**根据以上内容制作一个Python蟒蛇的实例：**
```python
import turtle
turtle.setup(650,350,200,200)
turtle.pu()
turtle.fd(-250)
turtle.pd()
turtle.pensize(25)
turtle.pencolor("purple")
turtle.seth(-40)
for i in range(4):
    turtle.circle(40,80)
    turtle.circle(-40,80)
turtle.circle(40,80/2)
turtle.fd(40)
turtle.circle(16,180)
turtle.fd(40*2/3)
turtle.done()


```