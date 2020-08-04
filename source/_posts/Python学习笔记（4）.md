---
title: Python程序的控制结构
date: 2019-05-14 09:10:32
tags: Python
categories:
  - 学习历程
  - Python基础
---

## 程序的分支结构：
### 单分支结构：
**根据判断条件结果而选择不同的向前路径**
**使用方式：**
```python
if <条件>:
  <语句块>
```
<!-- more -->

### 二分支结构：

**根据判断条件结果而选择不同向前路径的运行方式**
**使用方式：**
```python
if <条件>:
    <语句块1>
else:
    <语句块2>
```
**紧凑形式：适用于简单表达式的二分之结构
使用方式：**
```python
<表达式1> if <条件> else <表达式2>
```
**例如：**

```python
#判断奇偶，偶数输出YES奇数输出NO
ans = eval(input())
print("Yes") if ans % 2 == 0 else print("NO")
```
### 多分支结构：
**使用方式：**
```python
if <条件1>:
    <语句1>
elif <条件2>:
    <语句2>
else ：
    <语句3>
```
### 条件组合的三个保留字：
**① x and y：逻辑与（相当于C/C++中的 &&），x与y，同1为1，否则为0
② x or y：逻辑或（相当于C/C++中的 ||），x或y，有1为1，全0为0
③ not x：逻辑非（相当于C/C++中的 !），not 1 为 0 ，not 0 为1**
### 程序异常处理：
**使用方式：**
```python
try :
    <语句块1>
except <异常类型> :
    <语句块2>
```
**例如：**
```python
#判断奇偶
try:
    num = eval(input("请输入一个整数："))
    print("{}是{}数".format(num,"偶" if num % 2 == 0 else "奇"))
except:
    print("输入的不是整数")
```
### 异常处理的高级使用：
**使用方式：**
```python
# 当语句1执行时，语句3也执行，如果发生异常，语句2执行，无论是否异常，语句4都执行
try:
    <语句1>
except：
    <语句2>
else:
    <语句3>
finally:
    <语句4>
```
**实例：**
```python
#BIM身体质量指标判断
who,nat = "",""
def judge(bmi):
    if bmi < 18.5:
        who,nat = "偏瘦","偏瘦"
    elif 18.5 <= bmi < 24:
        who,nat = "正常","正常"
    elif 24 <= bmi < 25:
        who,nat = "正常","偏胖"
    elif 25 <= bmi < 28:
        who,nat = "偏胖","偏胖"
    elif 28 <= bmi < 30:
        who,nat - "偏胖","肥胖"
    else:
        who,nat = "肥胖","肥胖"
    print("BIM指标为:国际:{},国内{}".format(who,nat))
height , weight = eval(input("请输入身高（米）和体重（公斤）[用逗号隔开]:"))
bmi = weight / pow(height,2)
print("BIM 的数值为:{:.2f}".format(bmi))
judge(bmi)
```
## 程序的循环结构：
### 遍历循环：
**使用方式：**
```python
for <循环变量> in <遍历结构>:
    <语句块>
```
**计数循环（N次）：**
```python
#for i in range(N):
#    <语句块>
for i in range(5):
    print(i)        #输出从0到4之间的所有数字
```
```python
#for i in range(M,N,K):       从M开始到N-1结束，步长为K
#    <语句块>   
for i in range(5,10,2):
    print(i)       #输出结果为5，7，9（各占一行）
```
**字符串遍历的两种方式：**
```python
s = "12345"
for c in s:                     #第一种
    print(c,end = ",")
print("\n")
for i in range(len(s)):     #第二种
    print(s[i],end = ",")
```
**列表遍历：**
```python
for i in ['A','B','C']:
    print(i)            #输出结果为A,B,C（各占一行）
```
**文件遍历：**
```python
 #后面会具体介绍，这里只给出使用方式
#fi是文件标识符
for line in fi:            
    print(line)
```
### 无限循环:
**由条件控制的循环运行方式**
**使用方式：**
```python
while <循环条件>:
    <语句块>
```
### 循环控制保留字：
**break：跳出循环
continue：结束当此循环，继续后面的循环**
### 循环的高级用法：
**for循环使用方式：**
```python
#当循环正常结束时（不是因break退出）执行else语句
for <循环变量> in <遍历结构>:
    <语句块1>
else:
    <语句块2>
```
**while循环使用方式：**
```python
#当循环正常结束时（不是因break退出）执行else语句
while <循环条件>:
    <语句块1>
else:
    <语句块2>
```
**例1：**
```python
for c in "123456":
    if c == "3":
        continue
    print(c)
else:
    print("正常退出") #由于循环中不含break，所以最后会输出正常退出
```
**例2：**
```python
for c in "123456":
    if c == "3":
        break
    print(c)
else:
    print("正常退出")   #由于for循环是因break退出，所以最后不会输出正常退出
```