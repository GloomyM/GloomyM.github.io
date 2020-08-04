---
title: Python函数和代码复用
date: 2019-05-15 19:12:30
tags: Python
categories:
  - 学习历程
  - Python基础
---

## 函数的定义和使用：
**-函数是一段具有特定功能的可重用的语句组**
**使用方式：**

```python
def <函数名>(<参数(0个或多个)>):
    <函数体>
    return <返回值>
```
<!-- more -->

**例如：**

```python
#求n的阶乘
def cal(N):
    ans = 1
    for i in range(1,N+1):
        ans *= i
    return ans
n = eval(input("请输入一个整数:"))
print("{}的阶乘为{}".format(n,cal(n)))
```
### 函数中的可选参数：
**使用方式：**
```python
def <函数名> (<非可选参数> , <可选参数>): #非可选参数一定要放在可选参数之前
    <函数体>
    return <返回值>
```
**在上述代码中进行更改，例如：**
```python
#计算N的阶乘整除m，如果函数中不传入参数m，那么m默认为1，所以将m称为可选参数
def cal(N,m = 1):
    ans = 1
    for i in range(1,N+1):
        ans *= i
    return ans // m
n,m = eval(input("请分别输入两个整数:(用逗号隔开)"))
print("结果为{}".format(cal(n,m)))
```
### 函数中的可变参数：
**使用方式：**
```python
# 这与C/C++中的数组传地址有些类似,*参数可以类比于传入一个首地址
def <函数名> (<参数> , *参数): 
    <函数体>
    return <返回值>
```
**例如：**
```python
#计算n的阶乘然后再分成与1，2，3，4相乘
#方法1：
def cal(N,*m):
    ans = 1
    for i in range(1,N+1):
        ans *= i
    for i in range(len(m)):
        ans *= m[i]
    return ans
n= eval(input("请输入一个整数:"))
print("结果为{}".format(cal(n,1,2,3,4)))
```
```python
#方法2：
def cal(N,*m):
    ans = 1
    for i in range(1,N+1):
        ans *= i
    for i in m:
        ans *= i
    return ans
n= eval(input("请输入一个整数:"))
print("结果为{}".format(cal(n,1,2,3,4)))
```
### 函数的返回值：
**-return保留字用来传递返回值，函数可以有返回值也可以没有返回值，return 可以传递0个返回值，也可以传递多个返回值**
**例如：**
```python
#计算n!，n! * m , n! / m
def cal(N , M = 1):
    ans = 1
    for i in range(1,N+1):
        ans *= i
    return ans , ans * M , ans // M
n , m = eval(input("请分别输入两个整数:（用逗号隔开）"))
a,b,c = cal(n,m)
print("{}! = {},{}! * {} = {},{}! / {} = {}".format(n,a,n,m,b,n,m,c))
#输入5,2对应输出结果为：5! = 120,5! * 2 = 240,5!/2 = 60
```
### 局部变量和全局变量：
**-函数内部使用变量叫做局部变量，函数外部使用变量酒窖全局变量**
**-全局变量和局部变量即使名字是相同的也是不同的变量**
**例如：**
```python
#可以看到有两个ans变量，但输出结果为3628800 50，所以全局变量和局部变量即使名字一样但也是不同的变量
n,ans = 10,50
def cal(n):
    ans = 1
    for i in range(1,n+1):
        ans *= i
    return ans
print(cal(n),ans)
```
**如果想要在函数中使用全局变量，我们可以使用global保留字声明，例如：**
```python
n,ans = 10,10
def cal(n):
    global ans      #这里的ans就是10
    for i in range(1,n+1):
        ans *= i
    return ans
print(cal(n),ans)
```
**-局部变量为组合数据类型且未创建，等同于全局变量**
**例如：**
```python
ls = ["F","f"]
def func(a):
    ls.append(a)
func("c")
print(ls)
#输出结果为：["F","f","c"]
```
### lambda函数
**使用方式：**
**<函数名> = lambda <参数>: <表达式>**
**例如：**
```python
f = lambda x,y : x + y
print(f(10,20))
#输出结果为30
```
**实例：**

```python
#七段数码管
import turtle as t
import time as ti
def drawline(draw):
    t.pendown() if draw else t.penup()
    t.fd(40)
    t.right(90)
def init(n):
    t.penup()
    t.fd(n)
def drawdigit(digit):
    drawline(True) if digit in [2,3,4,5,6,8,9] else drawline(False)
    drawline(True) if digit in [0,1,3,4,5,6,7,8,9] else drawline(False)
    drawline(True) if digit in [0,2,3,5,6,8,9] else drawline(False)
    drawline(True) if digit in [0,2,6,8] else drawline(False)
    t.left(90)
    drawline(True) if digit in [0,4,5,6,8,9] else drawline(False)
    drawline(True) if digit in [0,2,3,5,6,7,8,9] else drawline(False)
    drawline(True) if digit in [0,1,2,3,4,7,8,9] else drawline(False)
    t.left(180)
    init(15)
def drawdata(s):
    t.pencolor("red")
    for c in s:
        if c == '-':
            t.write("年",font = ("Arial" , 25 , "normal"))
            t.pencolor("green")
            t.fd(60)
        elif c == '=':
            t.write("月",font = ("Arial" , 25 , "normal"))
            t.pencolor("blue")
            t.fd(60)
        elif c == '+':
            t.write("日",font = ("Arial" , 25 , "normal"))
        else:
            drawdigit(eval(c))
            
def main():
    t.setup(1000,350,200,200)
    t.hideturtle()
    t.speed(0)
    s = ti.strftime('%Y-%m=%d+',ti.gmtime())
    init(-300)
    t.pensize(5)
    drawdata(s)
    t.done()
    
main()
```
## 代码复用与函数递归：

### 函数的递归：
```python
#计算n的阶乘
def cal(n):
    return cal(n-1)*n if n != 1 else 1
print(cal(5))
#输出结果为120
```
```python
#递归翻转字符串
def rev(s):
    return s if s == "" else rev(s[1:]) + s[0]
print(rev("123456"))
```
**实例:**
```python
#Python科赫雪花
import turtle as t
def coh(size,n):
    if n == 0:
        t.fd(size)
    else:
        for angle in [0,60,-120,60]:
            t.left(angle)
            coh(size/2,n-1)
def init():
    t.setup(600,600)
    t.pensize(4)
    t.penup()
    t.goto(0,0)
    t.pendown()
    t.hideturtle()
def main():
    init()
    coh(100,2)
    t.right(120)
    coh(100,2)
    t.right(120)
    coh(100,2)
    t.done()
main()

```