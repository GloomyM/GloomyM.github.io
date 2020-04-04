---
title: PyDesigner+PyQt5+Pycharm配置
date: 2020-04-03 13:21:34
tags: PyQt5
---

## 简介：

由于QT Desginer 在创建窗体项目时会自动生成扩展名为.ui的文件，该文件需要转换为.py文件后才能被Python所识别，所以需要为QT Designer与Pycharm开发工具进行配置。

<!-- more -->

## 具体步骤：

进入Pycharm后点击左上角的File，在菜单中找到Settings，依次点击Tools,External Tools，如下图：

<img src="/images/Post-Img-1.png" style="zoom:80%;" />


（这里因为我已经提前完成安装，所以上面已经显示了两个插件）点击加号，在Program一栏添加designer的安装路径，其他内容按照下图填写最后点击OK：

<img src="/images/Post-Img-2.png" style="zoom:80%;" />

在配置PyQt5时同样点击加号，在Name一栏添加PyUic，在Program一栏添加Python的安装路径，Arguments一栏添加：

```
-m PyQt5.uic.pyuic $FileName$ -o $FileNameWithoutExtension$.py
```

Working directory一栏添加：

```
$FileDir$
```

最后点击OK

在配置qrcTopy时同样点击加号，在Name一栏添加QrcTopy在，Program一栏添加pyrcc5的安装路径，Arguments一栏添加：

```
$FileName$ -o $FileNameWithoutExtension$_rc.py
```

Working directory一栏添加：

```
$FileDir$
```

最后点击OK。

以上就是所有的配置步骤，完成配置后，就可以在Pycharm里创建自己的UI文件啦😝