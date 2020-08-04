---
title: Python基本数据类型
date: 2019-05-13 09:10:32
tags: Python
categories:
  - 学习历程
  - Python基础
---

### 数字类型及操作：
#### 一、整数类型：
**可正可负，没有取值范围限制**
**pow(x,y)函数：** 
**计算x的y次方，这里与其他变成语言不同的是，pow(x,y)没有上限，在C++中除了不怎么常用的int128之外，long long 是最大的整数类型，但是long long最多可以计算到2的64次方，而在Python中，pow(2,100)结果为1267650600228229401496703205376，不受任何限制，想算多大就算多大。**
**四种进制表示形式：**
**①十进制
②二进制，以0b或者0B开头
③八进制，以0o或者0O开头
④十六进制，以0x或者0X开头**

<!-- more -->

#### 二、浮点类型：
**带有小数点以及小数的数字**
**round(x,d)函数：** 
**对x四舍五入，d是保留位数，例如：round(0.78,1)，对0.78四舍五入保留一位小数，显然结果是0.8，由于浮点数运算间经常出现不确定尾数，但这些尾数一般发生在10的-16次方左右，因此在计算或比较过程中经常使用round函数辅助。**
#### 三、复数类型：
**复数：** 
**z = a+bj的形式，a称为复数的实数部分，b称为复数的虚数部分，例如：z = 3 + 4j，我们使用z.real获得实部，z.imag获得虚部。
数值运算操作符。**
#### 基本数据运算操作符：
① x + y：加法 
② x - y：减法
③ x * y：乘法
④ x / y：除法，这里的除法与其他语言不同，并不是取整，而是计算出精确结果，10/3 = 3.333333...
⑤ x // y：整除，10 // 3 = 3
⑥ x % y：取模（取余），10 % 3 = 1
⑦ - x：x的相反数
⑧ x ** y：x的y次方，当y为小数是表示开方运算，例如，25 ** 0.5结果为5，功能与pow(x,y)一样

#### 数值运算函数：
**① abs(x)：表示x的绝对值
② divmod(x,y)：商余函数，(x // y , x % y)，同时输出商和余数，divmod(10,3)结果为(3,1)
③ pow(x,y)：表示x的y次方
④ pow(x,y,z)：表示x的y次方模z
⑤ round(x,d)：表示保留d为小数输出x，d省略时默认为0（取整）
⑥ max(x1,x2,x3,...,xn)：求出1-n所有数字中的最大值，n不限
⑦ min(x1,x2,x3,...,xn)：求出1-n所有数字中的最小值，n不限**
#### 数值转换函数：
**① int(x)：将x转换为整数，int(1.25)结果为1，int("123")结果为123（将字符串转换为整数）
② float(x)：作用与int(x)类似，将x转换为浮点数
③ complex(x)：将x转换为复数，complex(4)结果为(4+0j)**
#### 例题1:
**一年365天，初始状态为1.0，假如工作日进步1%，休息日退步1%，那么一年以后的水平是多少？**
```python
dayup = 1.0
dayfactor = 0.01
for i in range(365):
    if i % 7 in [6,0]:
        dayup *= 1 - dayfactor
    else:
        dayup *= 1 + dayfactor
print("结果为:{:.2f}".format(dayup))
```
#### 例题2：
**A一年365天每天进步1%，不停歇，B一年365天每周工作五天休息两天，休息日退步1%，B需要在工作日每天进步多少才能达到A的进步效果呢？**
```python
#法1：暴力枚举，并不准确
def dayUP(df):
    dayup = 1.0
    for i in range(365):
        if i % 7 in [0,6]:
            dayup *= 1 - 0.01
        else:
            dayup *= 1 + df
    return dayup
dayfactor = 0.01
while dayUP(dayfactor) < 37.78:
    dayfactor += 0.001
print("结果为:{:.4f}".format(dayfactor))
```
```python
# 法2：数学方法计算，可以得到更精确的值
dayup = 1.0
dayfactor = 0.01
result = dayup * pow(1 + dayfactor,365)
cnt = 0
for i in range(365):
    if i % 7 in [6,0]:
        dayup *= 1 - dayfactor
    else:
        cnt+=1
print("结果为:{:.4f}".format(pow(result/dayup,1/cnt)-1))
```
### 字符串类型及操作：
#### 字符串类型的表示：
**字符串由0个或多个字符组成的有序字符序列**

**-字符串由一对单引号或一对双引号表示仅表示单行字符串
-字符串由一堆三单引号或三双引号表示，可表示多行字符串
-字符串是字符的有序序列，可以对其中的字符进行索引
-字符串的序号，正向递增（从0开始），反向递减（从-1开始）**
#### 字符串切片的高级用法：
**使用[M:N:K]根据步长对字符串切片**
**-<字符串>[M:N]，M缺失表示至开头，N缺失表示至结尾，例如："12345678"，[:3]结果是"123"，[3:]结果为"45678"
-<字符串>[M:N:K]，根据步长对字符串进行切片，以M为起始点，K为步长，N-1为终止点，例如："12345678"，[0:6:2]的结果为"135"，如果我们想倒序输出字符串，那么可以这样[::-1]，字符串从开头到结尾，步长为-1（从后往前）**
#### 字符串操作符：
**①x + y：连接两个字符串x和y
②n * x 或 x * n：复制n次字符串x
③x in s：如果x是s的子串返回True否则返回False**
```python
#字符串操作符的简单应用
s1 = "12345678"
s2 = "123"
if s2 in s1:    #判断子串
    print("YES")
else:
    print("NO")
print(s2 + s1)  #连接2个字符串
print(s2*3)     #将字符串s2复制三次
```

#### 字符串处理函数：
**① len(s)：字符串s的长度，len("1234")结果为4
② str(s)：将任何类型的数据转换为字符串，str(1.5)结果为"1.5"，这与eval()评估函数类似，eval()函数是将最外侧的引号去掉后执行剩下的语句，str()函数相当于在最外侧加上一对引号
③ hex(x)：将整数x转换成其十六进制小写表示形式的字符串
④ oct(x)：将整数x转换成其八进制小写表示形式的字符串
⑤ chr(u)：u为Unicode编码返回对应字符，这里有一个有趣的实例，输出12个星座**

```python
for i in range(12):
    print(chr(9800 + i),end = "  ")
 # 这是输出的结果♈  ♉  ♊  ♋  ♌  ♍  ♎  ♏  ♐  ♑  ♒  ♓
```
**⑥ ord(x)：x为字符，返回其对应的Unicode编码**

#### 字符串的处理方法：
**① str.upper()或str.lower()：返回字符串str的副本，upper为全大写，lower为全小写
② str.split(sep)：返回一个列表，由str根据sep被分割的部分组成，"A,B,C".split(",")结果为['A','B','C']
③ str.count(sub)：返回子串sub在字符串str中出现的次数
④ str.replace(old,new)：返回字符串的副本，将str中的old子串替换为new子串，"number".replace("n","1")结果为1umber              
⑤ str.center(width,fillchar) 字符串str根据宽度width居中，filllchar可选，例如："python".center(20,"=")结果为"=======python======="
⑥ str.strip(chars)：从str中去掉在其左侧和右侧chars中列出的字符，例如"= python= ".strp(" =np")，取出字符串两侧的" ","=","n","p"，所以输出的结果为："ytho"
⑦ str.join(iter)：在iter变量除最后元素外的每一个元素后增加一个str，例如：","join("12345")结果为"1,2,3,4,5"**
#### 字符串类型格式化：
**我们把形如{}的叫做槽，在Python语言中，槽机制({})+format方法实现字符串类型的格式化**
**例如："第{}台计算机的排名是{}".format(1,2)，结果为：第1台计算机的排名是2，可以看到，第一个槽中对应的结果某人是format函数中的第一个变量然后依次向后。当然，如果想对应不同变量也是可以的，例如，想让第一个参数是2第二个参数是1，那么可以这样操作，第{1}台计算机的排名是{0}".format(1,2)，这个意思就是，让第一个槽对应后面变量的第2个参数，第二个槽对应第一个参数，所以结果为：第2台计算机的排名是1**
##### format()方法的格式控制：
**槽内部对格式化的配置方式：{<参数序号> : <格式控制标记>}**

<img src="/images/Post-Img-0.png" style="zoom:80%;" />

```python
print("{:=^20}".format("PYTHON"))
#字符串PYTHON以20个字符为宽度，居中对齐，剩余部分以=填充
```
```python
print("{:=>20}".format("PYTHON"))
#字符串PYTHON以20个字符为宽度，右对齐，剩余部分以=填充
```
```py
print("{:20}".format("PYTHON"))
#如果只设置宽度，那么默认左对齐，剩余部分以空格填充
```
```python
print("{:,.2f}".format(123456.789))
# 逗号为千位分隔符，.2f保留小数点后两位输出，结果为：123,456.79
```
### time库的使用:

#### time库介绍：
**Python标准库，time库包括三类函数：**
**-时间获取：time()，ctime()，gmtime()
-时间格式化：strftime()，strptime()
-程序计时：sleep()，perf_conuter()**

**time.time()函数：得到是从1970年一月一日0点到现在的一个以秒为单位的浮点数
time.ctime()函数：获取人类最易读的时间，包含年月日，星期，时间
time.gmtime()函数：获取一种计算机可处理的时间格式**

#### 时间格式化
**① strftime(tpl,ts)：tpl是格式化模板字符串，用来定义输出效果，ts是计算实际内部时间类型变量，例如：**
```py
import time
t = time.gmtime()
print(time.strftime("%Y-%M-%D %H:%M:%S",t))
```

| 格式化字符串 | 日期/时间说明 | 值范围           |
| ------------ | ------------- | ---------------- |
| %Y           | 年份          | 0000~9999        |
| %m           | 月份          | 01~12            |
| %B           | 月份名称      | January~December |
| %b           | 月份名称缩写  | Jan~Dec          |
| %d           | 日期          | 01~31            |
| %A           | 星期          | Monday~Sunday    |
| %a           | 星期缩写      | Mon~Sun          |
| %H           | 小时（24h制） | 00~23            |
| %I           | 小时（12h制） | 01~12            |
| %p           | 上/下午       | AM,PM            |
| %M           | 分钟          | 00~59            |
| %S           | 秒            | 00~59            |

**②strptime(str,tpl)：str是字符串形式的时间值，tpl是格式化模板字符串，用来定义输入效果**

#### 程序计时
**测量时间：perf_counter()
返回一个CPU级别的精确时间计数值，单位为秒，由于这个计数值的起点不确定，连续调用差值**
**例如：**
```python
import time as t
st = t.perf_counter()
cnt = 0
for i in range(10):
    cnt += 1
ed = t.perf_counter()
print("循环{}次运行的时间为:{}".format(cnt,ed-st))

```

**产生时间：sleep()
sleep(s)函数里的参数s代表休眠的时间，单位为秒，sleep(5)表示程序休眠五秒再执行
例如：**
```python
import time as t
def wait():
    t.sleep(5)
sum = 0
for i in range(1,11):
    sum += i
wait() #程序再休眠五秒后再输出最后的结果
print("1-10的和为{}".format(sum))
```
**实例1：**
```python
# 模拟文本进度条
import time as t
width = 10
print("{:-^15}".format("执行开始"))
for i in range(width):
    a = '*' * i
    b = '.' * (width - i)
    per = (i/width)*100
    print("{:^3.0f}%[{}->{}]".format(per,a,b))
    t.sleep(0.1)
print("{:-^15}".format("执行结束"))
```
**实例2：**
```python
#实现单行动态刷新
import time as t
for i in range(101):
    print("\r{:3}%".format(i) , end = "") # \r表示光标回到起始位置，end = ""表示不换行
    t.sleep(0.1)
```
**实例3：**
```python
#结合实例1和实例2实现动态刷新文本进度条功能
import time as t
width = 50
print("执行开始".center(width//2,"-"))
st = t.perf_counter()
for i in range(width+1):
    a = '*' * i
    b = '.' * (width - i)
    per = i / width * 100
    dur = t.perf_counter() - st
    print("\r{:^3.0f}%[{}->{}]{:.2f}s".format(per,a,b,dur) , end = "")
    t.sleep(0.1)
print("\n" + "执行结束".center(width//2,"-"))
```