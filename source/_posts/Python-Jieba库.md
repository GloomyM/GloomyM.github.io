---
title: Jieba库
date: 2019-05-17 22:11:23
tags: Python
---

## 简介：

**jieba是优秀的中文分词第三方库
-中文文本需要通过分词获得单个的词语
-jieba是优秀的中文分词第三方库，需要额外安装**

<!-- more -->

## Jieba分词原理：

**jieba分词依靠中文词库
-利用一个中文词库，确定汉字之间的关联概率
-汉字间概率大的组成词组，形成分词结果**

## Jieba分词的三种模式：
**-精确模式：把文本精确的切分开，不存在冗余
-全模式：把文本中所有可能的次元都扫描出来，有冗余
-搜索引擎模式：在精确模式基础上，对场次再次切分**

| 函数及方法                   | 描述                                               |
| ---------------------------- | -------------------------------------------------- |
| jieba.lcut(s)                | 精确某事，返回一个列表类型的分词结果               |
| jieba.lcut(s,cut_all = True) | 全模式，返回一个列表类型的分词结果，存在冗余       |
| jieba.lcut_for_searh(s)      | 搜索引擎模式，返回一个列表类型的分词结果，存在冗余 |
| jieba.add_word(w)            | 向分词词典增加新词w                                |


**实例1:**

```python
#中文文本词频统计--三国演义人物出场统计
import jieba as j
import os
def getText():  #打开文本
    txt = open("D:\Python\素材\THREEKINGDOMS.txt","r",encoding="utf-8").read()
    words = j.lcut(txt) #调用jieba库中的lcut函数进行分词
    return words        #返回一个列表，包含分词后的数据
words = getText()
excludes = {"将军","却说","荆州","二人","不可","不能","如此","军士","主公","如何","商议","军马","左右","引兵","次日","大喜","天下","东吴"\
    ,"于是","今日","不敢","魏兵","陛下","一人","都督","人马","不知"}
counts = dict() #新建一个字典
for word in words:
    if len(word) == 1:
        continue
    elif word == "诸葛亮" or word == "孔明曰":
        rword = "孔明"
    elif word == "关公" or word == "云长":
        rword = "关羽"
    elif word == "玄德" or word == "玄德曰":
        rword = "刘备"
    elif word == "孟德" or word == "丞相":
        rword = "曹操"
    else:
        rword = word
    counts[rword] = counts.get(rword,0) + 1     #对字典中键对应的值进行赋值
for word in excludes:
    del(counts[word])
items = list(counts.items())                        #将字典中的键值对放入序列items
items.sort(key=lambda x: x[1],reverse=True) #根据值进行排序，因为默认从小到大，所以在排序后反转
print("三国演义人物出场统计TOP10:")
for i in range(10):
    word,count = items[i]
    print("{:<10}{:>5}".format(word,count))
os.system('pause')
```
**实例2：**
```python
#英文文本词频统计--哈姆雷特
import os
def getText():
    txt = open("D:\Python\素材\HAMLET.txt","r").read()
    txt = txt.lower()
    for ch in '!"#$%&()*+,_-./:;<=>?@[\\]^_{|}~':
        txt = txt.replace(ch," ")
    return txt
hamletTxt = getText()
words = hamletTxt.split()
counts = dict()
for word in words:
    counts[word] = counts.get(word,0) + 1
items = list(counts.items())
items.sort(key=lambda x: x[1],reverse=True)
print("哈姆雷特词频统计:")
for i in range(10):
    word,count = items[i]
    print("{:<10}{:>5}".format(word,count))
os.system('pause')

```