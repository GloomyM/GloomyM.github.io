---
title: WordCloud库
date: 2019-05-17 22:10:23
tags: Python
categories: 学习历程
---

## 简介
**wordcloud是优秀的第三方词云库**
**wordcloud库常规方法：
w = wordcloud.WordCloud()**

| 方法                | 描述                                 |
| ------------------- | ------------------------------------ |
| w.generate(txt)     | 向WordCloud对象w中加载文本txt        |
| w.to_file(filename) | 将慈云输出位图像文件，.png或.jpg格式 |

<!-- more -->

## 使用方式：

**词云绘制:
步骤1：配置对象参数
步骤2：加载词云文本
步骤3：输出词云文件**
**配置对象参数：**
**w = wordcloud.WordCloud(<参数>)**

| 参数             | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| width            | 指定词云对象生成图片的宽度，默认为400像素                    |
| heigth           | 指定词云对象生成图片的高度，默认为200像素                    |
| min_font_size    | 指定词云中字体的最小字号，默认4号                            |
| max_font_size    | 指定词云中字体的最大字号，根据高度自动调节                   |
| font_step        | 指定词云中字体字号的步进间隔，默认为1                        |
| font_path        | 指定字体文件的路径，默认为None，w = wordcloud.WordCloud(font_path = "msyh.ttc")表示微软雅黑 |
| max_words        | 指定词云显示的最大单词数量，默认为200                        |
| stop_words       | 指定词云的排除词列表，即不显示的单词列表                     |
| mask             | 指定词云形状，默认为长方形，需要imread函数                   |
| background_color | 指定词云图片的背景颜色，默认为黑色                           |