---
title: Python常见问题处理
date: 2019-05-20 18:16:20
tags: Python
categories: 学习历程
---

## Python库安装失败：
**当安装Python中的某些库时，命令行执行`pip install 库名`经常会超时，为了解决这个问题，可以使用一些国内镜像，清华大学镜像：https://pypi.mirrors.ustc.edu.cn/simple/。**
#### 国内镜像使用方法：
```cmd
pip install 库名 --index https://pypi.mirrors.ustc.edu.cn/simple/
```
<!-- more -->

## 命令行要求Python升级失败：

**当命令行要求更新Python，但执行`python -m pip install --upgrade pip`后仍然显示更新失败，那么可以使用如下方法：
打开Python安装目录，找到Lib目录下的sit-packages文件夹，找到文件名为 `pip-版本号.dis-info`的文件并删除，然后在命令行重新执行`python -m pip install --upgrade pip`。
如果仍然提示安装失败，那么有可能是因为超时造成的，可以使用国内镜像安装，方法如下：
在命令行输入：`python -m pip install --upgrade pip -i https://pypi.douban.com/simple`，这里用的是豆瓣的国内镜像，经过上述两种方法便可以解决Python安装失败的问题**
## open函数打开文件报错:
**在使用open()函数打开.txt的文本文件时，如果打开的文件是中文格式，要使用encoding = "utf-8"，往往txt文件的保存编码是ANSI格式的，所以要在另存为时更改txt文件保存编码为UTF-8，这样才能保证不报错**
## Pystaller打包时Jieba库报错：
**在使用Jieba分词+Pyinstaller打包时经常会出现一些报错：**
**①错误提示：FileNotFoundError：No such file or directory
这是因为jieba库在运行时会去默认Python路径下去寻找dict.txt文件。而我们使用PyInstaller打包时，并没有将该dict.txt文件打包。
处理方法:
在代码前加入如下语句**
```python
import jieba
jieba.set_dictionary("./dict.txt")  #指定dict.txt加载路径，为了方便部署，使用相对路径。
jieba.initialize()                       #jieba库初始化。
```
**②错误提示：DLL load failed:1% 不是有效的Win32应用程序
这种情况一般是Win32和Python版本不一致造成的，可能下载的Win是32位的，Python是64位的，只要让两个一致即可，重新安装一般就可以解决**

持续更新中...