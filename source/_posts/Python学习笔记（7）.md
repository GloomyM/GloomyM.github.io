---
title: Python文件和数据格式化
date: 2019-05-17 22:11:23
tags: Python
---

## 文件的使用：
**数据的抽象和集合**
**-文件时存储在辅助存储器上当数据序列
-文件时数据存储的一种形式
-两种形态文本文件和二级制文件**
**文本文件：由单一特定编码组成的文件，如UTF-8编码，简单来说，文本文件就是一个字符串**
**二进制文件：直接由比特0和1组成，没用统一字符编码**

<!-- more -->

### 文件的打开和关闭：

**文件处理的步骤：打开--操作--关闭**
**文件的打开：<变量名> = open(<文件名>（指文件的路径和名称）,<打开模式>)**
**打开模式：①二进制文件：rt  ②文本文件：rb**
### 文件的路径：
**①绝对路径：例如文件在"D:\Python\f.txt"，由于Python中"\"是转义字符，所以在输入路径是要把"\"改成"/"，也就是"D:/Python/f.txt"
②相对路径：指从文件所属的根目录起，如果文件是在D盘，那么可以直接输入"./Python/f.txt"，也就是从上级目录开始**
### 打开模式：

| 文件打开模式 | 描述                                                    |
| ------------ | ------------------------------------------------------- |
| "r"          | 只读模式，默认值，如果文件不存在，返回FileNotFoundError |
| "w"          | 覆盖写模式，文件不存就则创建，存在则完全覆盖            |
| "x"          | 创建写模式，文件不存在则创建，存在则返回FileExistsError |
| "a"          | 追加写模式，文件不存在则创建，存在则在文件最后追加内容  |
| "b"          | 二进制文件的模式                                        |
| "t"          | 文本文件的模式                                          |


```python
f = open("f.txt")
文本形式、只读模式、默认值
```
## 文件读取：

|           操作方法           |                             描述                             |
| :--------------------------: | :----------------------------------------------------------: |
|   <f>.read(size = <长度>)    |          读入全部内容，如果给出参数，读出前size长度          |
| <f>.readline(size = <长度>)  |        读入一行内容，如果给出参数，读入该行前size长度        |
| <f>.readlines(hint = <行数>) | 读入文件所有行，以每行元素形成列表，如果给出参数hint，读入前hint行 |


### 文件的全文本操作：

**①：直接读取文件中的所有内容，当文件较大时，占用内存较大**
```python
fo = open("D:/Python/素材/Test.txt","r")
txt = fo.read()
fo.close()
```
**②：每次读取2个字节（可选择），占用内存较小**

```python
fo = open("D:/Python/素材/Test.txt","r")
txt = fo.read(2)
while txt != "":
    txt = fo.read(2)
fo.close()
```


### 文件的逐行操作：

**①：利用readlines()函数，一次性读入所有行，形成列表，但占有内存太大**
```python
fo = open("D:/Python/素材/Test.txt","r")
for line in fo.readlines():
    print(line)
fo.close()
```
**②：每次读入一行数据，占有内存较小**

```python
fo = open("D:/Python/素材/Test.txt","r")
for line in fo:
    print(line)
fo.close()
```
## 文件写入：

| 操作方法              | 描述                                                         |
| --------------------- | ------------------------------------------------------------ |
| <f>.write(s)          | 向文件写入一个字符串或字节流                                 |
| <f>.writelines(lines) | 将元素全字符串的列表写入文件                                 |
| <f>.seek(offset)      | 改变当前文件操作指针的位置，offset含义如下：0 - 文件开头；1 - 当前位置；2 - 文件结尾 |


**向文件后添加一行文字并输出添加后的文件：**

```python
fo = open("D:/Python/素材/Test.txt","a+")
ls = ["中国","美国","英国"]
fo.writelines(ls)
fo.seek(0)
for line in fo:
    print(line)
fo.close()
```
**实例：自动轨迹绘制**

```python
import turtle as t
f = open("D:/Python/素材/自动轨迹绘制.txt","r")
data = list()
for line in f:
    line.replace("\n","")
    data.append(list(map(eval,line.split(","))))
f.close()
t.setup(800,600,0,0)
t.title("自动轨迹绘制")
t.pensize(3)
t.pencolor("red")
t.hideturtle()
for i in range(len(data)):
    t.pencolor(data[i][3],data[i][4],data[i][5])
    t.fd(data[i][0])
    if data[i][1]:
        t.right(data[i][2])
    else:
        t.left(data[i][2])
t.done()
```
## 一维数据的格式化：
### 一维数据的表示：
**数据间有序：使用列表类型
数据间无序：使用集合类型
使用for循环进行遍历**
```python
#从空格分隔的文件中读入数据
txt = open(fname).read()
ls = txt.split()
f.close()
```
## 二维数据的格式化：
### 二维数据的存储：
**二维数据用二维列表表达：**
**列表中的每个元素对应一个新的列表，因而构成二维列表**
### CSV数据存储格式
**CSV:Comma-Separated Values**
**-国际通用的一二维数据存储格式，一般.csv扩展名
-每行一个一维数据，采用逗号分隔，无空行
-Excel和一般编辑软件都可以读入或另存为csv文件**