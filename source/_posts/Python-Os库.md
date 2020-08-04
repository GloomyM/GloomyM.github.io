---
title: Os库
date: 2019-05-17 07:06:38
tags: Python
categories: 学习历程
---

## 使用方式：

<!-- more -->

| 函数                      | 方法                                                    |
| ------------------------- | ------------------------------------------------------- |
| os.path.abspath(path)     | 返回path在当前系统中的绝对路径                          |
| os.path.normpath(path)    | 归一性path的表示形式，同意使用\\分隔路径                |
| os.path.relpath(path)     | 返回当前程序与文件之间的相对路径                        |
| os.path.dirname(path)     | 返回path中的目录名称                                    |
| os.path.basename(path)    | 返回path中最后的文件名称                                |
| os.path.join(path,paths)  | 组合path和paths，返回一个路径字符串                     |
| os.path.exists(path)      | 判断path对应文件或目录是否存在，返回True或False         |
| os.path.getatime(path)    | 返回path对应文件或目录上一次的访问时间                  |
| os.path.getmtime(path)    | 返回path对应文件或目录最后一次的修改时间                |
| os.path.getctime(path)    | 返回path对应文件或目录的创建时间                        |
| os.system(执行文件的路径) | 执行对应的文件                                          |
| os.listdir()              | 路径为空则os.list('.') 将当前目录下的文件名返回一个列表 |
| os.path.splitext()        | 分离后缀名                                              |
| os.rename(old,new)        | 更改文件名                                              |